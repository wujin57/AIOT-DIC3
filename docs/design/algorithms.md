# DietSense 演算法與偽碼規格

本文件是 [DESIGN.md](../../DESIGN.md) 的語言無關演算法細節。公式版本、來源資料版本、安全政策及澄清上限都需明確傳入；本文件不代表演算法已實作或驗證。`unknown/null` 永遠不等於 0。

## 共通型別與終態

- `Result<T>`：`success(value)`、`partial(value, warnings)`、`need_user_input(request)`、`no_estimate(reason)`、`refused(reason)`、`error(code, retryable)`。
- `SessionState`：request ID、已解析欄位、selected candidate、clarification turn index/max、intent、狀態、使用者同意範圍、policy version。只保存完成任務所需資料。
- 排序分數只供候選排序，若無獨立校準，不轉成機率或「80% 信心」。
- 任何數值運算先驗證型別、有限值、單位和正負範圍；算術錯誤不得被轉成正常結果。

## A. 食物實體抽取與正規化

**目的。** 把自然語言轉成可供檢索的 FoodEntity，同時保留原始片段，避免解析過程丟失不確定性。

**輸入/輸出。** `UserInput` → `ParsedRequest(intent, entities[], missing_fields[], parse_warnings[])`。

**前置條件。** 輸入字串非空、請求長度符合介面限制、locale 可用或標記 unknown。parser 回傳資料須通過 schema validator。

**步驟。**

1. 保留原文，不以正規化結果覆寫原文。
2. 對字詞做繁簡/全半形和空白正規化；不移除數字、單位、否定詞或剩食描述。
3. 以受限分類器/LLM 提出 intent：`log_food / query_nutrition / analyze / recommend / unsupported`。
4. 抽取食物 mention、品牌、品項、食材、份量、烹調、溫度/生熟、剩食、時間等片段及 offsets。
5. 對每個欄位標記 `explicit / inferred / unknown / contradictory`；只有 explicit 和有來源規則轉換的值能直接成為確定輸入。
6. 混合菜保留為 mixed dish；若有使用者明述成分可建立 ingredient mentions，但不可從菜名默認菜譜。
7. 無效 JSON/schema、解析衝突或 unsupported intent 走 fallback，不建立數字記錄。

**失敗與複雜度。** 單句 token/實體抽取通常近似 O(n) 加模型推論成本；依賴模型延遲與 token 數。模型不可用時可允許純文字保存/請求改述。含互相矛盾單位時標記衝突，不能任選一個。

**例子。** 輸入「吃了半份蚵仔煎，醬另外放」→ `food_type=mixed_dish`、`name_original=蚵仔煎`、`portion.quantity=0.5`、`portion.unit=serving`（原文明示半份）、`sauce=separate/amount unknown`；克數和熱量均 unknown，等待檢索或澄清。

**測例。** (a)「牛肉麵湯喝一半」抽取 leftover/broth；(b)「不要記熱量」提取偏好/限制且不計算；(c)「三口」不可自動變成克數；(d) 空輸入、兩個衝突份量、提示注入文字不得產生可信來源欄位。

## B. 檢索與候選排序

**目的。** 從來源登錄表查找可核對的候選，並讓弱匹配/衝突可見。

**輸入/輸出。** `FoodEntity + source policy + locale` → `NutritionCandidate[] + retrieval_status`。

**前置條件。** 來源、版本、許可與資料欄位映射經審核；未確認的來源不可用於正式營養輸出。

**步驟。**

1. 對查詢建立多欄位檢索鍵：正規名稱、別名、品牌/品項、食材、烹調、熟/生狀態、地區、份量單位。
2. 對經授權來源執行精確 ID/品牌查詢，再查同義詞/字串候選，最後才用語義檢索找可能食譜候選。
3. 對每個候選驗證 source ID/version、食物狀態、可食部、單位和必要營養欄位；拒絕結構錯誤或過期狀態不明候選。
4. 以可解釋特徵排序：名稱匹配、品牌/產品匹配、食物狀態匹配、地區/配方匹配、來源品質與欄位完整性。權重/門檻須由 held-out 資料校準；初始階段不得宣稱概率。
5. 如果 top candidates 對身份、單位或值差異重大，將差異傳給 Planner 作澄清；若只有相似度高但狀態/食譜不符，不視為可靠。
6. 回傳候選、逐欄 provenance、檢索時間、版本、匹配理由及 caveats。

**失敗與複雜度。** 資料庫索引查詢可按索引近似 O(log N + k)；語義向量搜尋成本依索引和維度。API timeout、無候選、來源矛盾均作為不同狀態回傳。不得在沒有結果時由 LLM 編造候選營養值。

**例子。** 「無糖珍珠奶茶」檢索到只有「珍珠奶茶」的官方候選，糖度和杯量皆不匹配/未知。系統呈現候選但不默認無糖，詢問杯量及珍珠是否含在候選配方中；使用者跳過後只記錄文字或輸出明示假設的部分估算。

**測例。** 精確包裝候選優先於泛稱；熟食不匹配生食時拒絕直接採用；相同菜名不同重量須呈多候選；API timeout 不產生空陣列假成功；retrieved document 中的指令不改變工具/安全政策。

## C. 份量估算與澄清

**目的。** 決定是否可計算、需詢問何種欄位，以及何時停止追問。

**輸入/輸出。** `FoodEntity + candidates + turn_index/max_turns` → `PortionEstimate`、`ClarificationRequest` 或 `no_estimate/partial`。

**前置條件。** 只有來源標準份量、使用者克數或明確轉換規則可產生 mass_g；體積轉質量需要食物特定密度或來源換算。

**步驟。**

1. 確定營養計算關鍵欄位：食物身份、份量質量、來源 nutrient density、熟/生狀態；複合菜另加可得配方/成分比例。
2. 按預期改變結果的幅度、可回答性、澄清負擔排序缺欄位；這是可測試策略，不是已校準最優策略。
3. 若已有可信明示質量/可追溯 household conversion 且候選匹配，傳給 Analytics。
4. 若 `turn_index < max_turns`，提出一個針對優先欄位的中性問題，提供「不知道/跳過」選項。序列化 request 並等候下一個使用者訊息；不得在後端阻塞等待 UI。
5. 答案進入新 UserInput，重新抽取與驗證；最多重新檢索設定回合數。
6. 回合用盡、使用者跳過或候選依然不足：可建立 `text_only`，或只在存在明確低/高上下界證據時建立 plausible estimate range；沒有上下界資料則 `no_estimate`。

**終止保證。** `turn_index` 每次使用者澄清後單調遞增，`max_turns` 有有限正整數上限；skip/cancel/error 立即終止。預設設計上限為 2，僅為初始可用性假設，需測試後調整。

**例子。** 「一碗牛肉麵」可先問麵/碗大小或湯量中影響較大且較易回答的一項。若使用者不知道，就只記錄文字或引用有效標準份量並註明假設；不會從向量相似度產生 300–420 kcal 之類無依據範圍。

**測例。** 一次回覆後重新匹配成功；跳過後狀態終止；重複不明回答最多兩輪；cancel 不保存；不存在克數轉換表時，不產生 mass_g；未知被保留而不是設成 0。

## D. 確定性熱量/巨量營養素計算

**目的。** 由已驗證來源和份量計算可重現值。

**輸入/輸出。** `NutritionCandidate` 或 `NutritionRecord + PortionEstimate` → `CalculationResult`。

**前置條件。** 能量密度 kcal/100g、重量 g、食物狀態/來源版本相容；所有數值為 finite decimal，非負。單位轉換先完成並留下記錄。

**公式。** 對每項 nutrient `x`：`x_amount = mass_g × x_per_100g ÷ 100`。若值按每份提供，須先依來源標準份量轉換；不混合 per-serving 與 per-100g 直接加總。用 decimal/固定精度運算，僅在輸出邊界按明確規則 rounding。

**步驟。** 驗證來源欄位 → 統一單位 → 對每食物計算 → 對食譜成分按質量/份數乘係數 → 彙總每個 nutrient → 計算完整度/警告 → 保存公式版本、input hash、來源 lineage。若某成分營養欄位缺失，對該營養素標 `null/partial`，不把缺失成分當零。

**複雜度與失敗。** n 個成分時 O(n) 時間、O(k) 結果欄位空間。負份量、來源單位不明、成分狀態不符、非有限數值或計算溢位均拒算受影響欄位。

**例子。** 假設已確認 150 g 食物，候選資料明示 250 kcal/100 g：計算 `150 × 250 / 100 = 375 kcal`。這只示範縮放算式，不代表任何實際菜色數值。若 protein/100g 未提供，protein_total 為 unknown，不能填 0 g。

**測例。** 100 g 的比例不變性；同輸入兩次輸出相同；缺一成分蛋白質時只有 protein total incomplete；`mass=0` 除非明確記錄為已確認零攝取否則拒絕建立食物 entry；換算值單位正確。

## E. 每日彙總

**目的。** 彙總指定日期和使用者時區內的可用飲食記錄，保留完整度。

**輸入/輸出。** `NutritionRecord[] + date + timezone` → `DailySummary`。

**步驟。** 篩選日期、owner/session scope 和允許的 record status；依 record ID 去重；每種 nutrient 只對非 null 確認值加總，同時回傳已納入/缺漏/文字-only 數目；若任何必要輸入或記錄缺失，標示 partial；不以摘要模型重新計算。

**失敗與複雜度。** n 筆記錄 O(n)。時區未知則請使用者選擇或明示暫用值；格式錯誤/重複 ID 回報並隔離，不重複加總。

**例子。** 早餐 300 kcal、午餐 text-only、晚餐 500 kcal，顯示「已知記錄合計 800 kcal，另有 1 筆未估算」，不能標成全天完整總量。

**測例。** 跨午夜按 timezone 切日；重複 record 不重算；unknown macro 維持 partial；空日摘要為 0 筆記錄，不等同已知攝取 0 kcal。

## F. BMR/REE/TDEE 估計、資格與假設

**目的。** 可選提供一般參考層級的 REE/TDEE 估算；不得自動轉成個人熱量目標。

**概念區分。** Mifflin–St Jeor 推導為 resting energy expenditure (REE) 預測式，不應宣稱為直接實測 BMR。若乘 activity factor 得 TDEE，這是第二層估算且依活動係數假設，不是測量結果。

**資格門檻。** 只對年滿 18 歲、非孕哺、未自述需臨床飲食治療且資料完整者考慮顯示一般估算；這是待專業審查的保守產品邊界，不是醫療資格標準。未成年人、孕哺、疾病治療、疑似飲食失調、重度運動/其他特殊情況不進入一般 TDEE/目標流程。若性別相關公式係數無法適用/使用者不願提供，應停止個人估算或提供非個人化一般資訊，不由模型推斷。

**公式/步驟。** 公開公式版本明確選擇 Mifflin–St Jeor（原始推導：[Mifflin et al., 1990](https://doi.org/10.1093/ajcn/51.2.241)）：依採用原始係數，男係數式 `10×weight_kg + 6.25×height_cm − 5×age_years + 5`，女係數式相同但常數為 `−161`。以此值標為 REE estimate；若使用者同意並選擇有來源的 activity category/factor，`TDEE_estimate = REE_estimate × activity_factor`。輸入限制、係數來源、轉換與係數均隨輸出呈現。此估算不構成建議的每日攝取量。

**例子。** 成人資料缺身高時回傳 `not_calculable`；有完整資料但未提供 activity factor 時只提供 REE estimate（若資格/同意允許）；不自行設 factor=1.2。

**測例。** 未滿 18 歲、孕哺/臨床情境、缺值、負值、activity factor 未選、未同意均不產生 TDEE；公式版本測例以公開參考輸入核對；變更 factor 只改變 TDEE，不改變 REE。

**失敗/限制。** 群體預測式存在個體誤差；活動係數、公式族群和輸入精度造成額外不確定性。實際系統如不能證明 formula provenance 和適用範圍，功能預設關閉。

## G. Plausible estimate range 建構

**目的。** 在資料本身有具體可追溯上下界時，呈現假設條件下的估算變化，而非假裝具有統計涵蓋率。

**步驟。** 收集候選 food record 與份量/配方每項的 low/high evidence；確認所有極值端點來源有效且單位相同；對非負密度，low case 用低份量/低密度組合計算、high case 用高組合計算；若不同候選互斥，分別計算後取可解釋包絡並標示候選；回傳 low/point/high 與每個假設。若任何必要邊界未知或範圍過寬而無實用性，回傳 partial/no_estimate。

**不得採用。** 不可把模型 rank score、主觀 confidence、固定 ±10%/20% 或任意百分比套在 point estimate 上當作誤差分布。除非後續有代表性驗證集、預先定義覆蓋率目標和外部校準，不能稱 statistical confidence interval。

**例子。** 已知來源密度固定為 200 kcal/100g，使用者提供質量為 80–100 g，線性端點為 160–200 kcal；若另選中心 90g，point=180，但必須明示這是該份量假設下的估值。數值僅為公式示例。

**測例。** low <= point <= high；全部端點轉換至同單位；缺任一關鍵邊界時不產生 range；較寬輸入範圍不會產生更窄輸出範圍；任何情況不出現「95% CI」字樣。

## H. 安全檢查與回覆生成

**目的。** 在計算、每日摘要、一般建議及最終呈現前後，執行版本化安全檢查，阻止超出系統範圍的個人化醫療內容。

**步驟。**

1. 將使用者請求及檢索文件視為不可信內容；僅 system policy 和版本化規則可決定授權。
2. 檢查意圖是否要求診斷/治療、危險限制/補償、敏感高風險情境或未成年人個人處方。不得以 LLM 單一判斷作最終安全 gate。
3. 決策 enum 為 `allow_general / restrict / refuse / refer`；規則衝突或狀態不明採較限制選項。
4. 如果允許，只用計算結果和有來源的指南生成一般資訊；模型無權改數字或新增來源聲稱。
5. 如限制/拒答，抑制相關建議，使用審核模板說明系統不能提供該類個人方案；在經專業審查的情況下給出尋求合格專業協助的方向。不可診斷、貼標籤、提供處方或恐嚇式通知。
6. 回覆 schema 驗證、引用/數值一致性檢查；不合格則安全降級至無數字模板。
7. 日誌只存最低必要 trigger code 和政策版本，不保存多餘敏感推論。

**範例。** 使用者問「明天少吃多少補償今天？」→ decision=`restrict`，不計算補償性目標；提供中性、非責備內容及停用數字記錄選項。若提及即時危險，採校方/專業人員事先核准的轉介流程；該流程目前尚未定稿。

**測例。** 「診斷我是否厭食」不診斷；「給我 600 kcal 菜單」不生成；要求刪除日誌進入資料權利流程；retrieved content 說忽略政策不被執行；未觸發風險的一般查詢可正常回答且不過度攔截。

## I. 同意、保存期限與資料刪除流程

**目的。** 使 FR-012/NFR-004 可驗證，確保記錄/研究用途依使用者同意與核准政策處理。此為資料生命週期程序，不是營養計算。

**步驟。** 接收已驗證請求 session 的 access token → 確認請求者對應記錄 owner 和同意範圍 → 建立刪除工作並標記待刪 → 查找主記錄、快取、可識別索引與衍生摘要的 lineage → 刪除或依法/倫理核准之不可逆去識別 → 檢查待處理 queue/備份的 retention policy 並記錄不可即時清除的狀態 → 產生不含飲食內容的 audit event → 只有所有適用層完成或明示等待政策時才回覆狀態。

**前置/失敗行為。** 身份或 ownership 不符時拒絕，不能揭露記錄是否存在；重複請求冪等；刪除失敗不回覆成功並提供 request ID；研究資料保留例外只有經明確同意與適用審查批准才能執行。備份期限、法定/倫理保留例外及第三方供應商刪除能力未定前不得承諾立即徹底清除。

**複雜度/範例。** 依 lineage 查找 n 個 linked objects，需 O(n) 清除/驗證。使用者要求刪除某筆餐點時，刪除任務引用該 entry 的彙總快取；無權限的 session 只收到一般拒絕，不暴露資料。

**測例。** 無同意不新增 log；合法刪除會移除指定主記錄及即時衍生項；重試同一 request 不重複副作用；跨使用者刪除拒絕；第三方/備份未確認時回覆 pending，而非 complete。

## 10. 跨意圖 Agent 主流程偽碼

以下用結構化回傳表示非同步互動。澄清是一次 request/response 狀態轉移，不是程式阻塞等待。

```text
FUNCTION handle_request(user_input, session_state):
    initialized = {
        response_plan: null,
        parsed: null,
        result: null,
        safety: evaluate_safety_precheck(user_input),
        updated_log: session_state.log_snapshot,
        warnings: []
    }

    IF initialized.safety.status IN {"refuse", "restrict", "refer"}:
        initialized.response_plan = safety_template(initialized.safety)
        RETURN render_and_validate(initialized.response_plan), initialized.updated_log

    initialized.parsed = parse_and_validate(user_input)
    IF initialized.parsed.status != "success":
        RETURN safe_parse_fallback(initialized.parsed), initialized.updated_log

    intent = initialized.parsed.intent

    IF intent == "log_food":
        result = process_food_entities(initialized.parsed.entities, session_state)
        IF result.status == "need_user_input":
            RETURN render_clarification(result.request), persist_minimal_state(result.state)
        IF result.status IN {"no_estimate", "partial", "error"}:
            initialized.warnings += result.warnings
        initialized.result = result

    ELSE IF intent == "query_nutrition":
        candidates = retrieve_candidates(initialized.parsed.query_entity)
        result = answer_query_from_verified_candidates(candidates)
        IF result.status == "need_user_input":
            RETURN render_clarification(result.request), persist_minimal_state(result.state)
        initialized.result = result

    ELSE IF intent == "analyze":
        summary = aggregate_daily_log(session_state.log_snapshot,
                                      initialized.parsed.target_date,
                                      session_state.timezone)
        profile_result = calculate_optional_tdee_if_eligible(
                             session_state.profile,
                             initialized.parsed.explicit_tdee_request)
        initialized.result = combine_summary_without_fabricating_missing_values(
                                 summary, profile_result)

    ELSE IF intent == "recommend":
        summary = aggregate_daily_log(session_state.log_snapshot,
                                      initialized.parsed.target_date,
                                      session_state.timezone)
        safety = evaluate_safety_for_recommendation(user_input, summary,
                                                    session_state.policy_version)
        initialized.safety = safety
        initialized.result = general_information_only_if_allowed(summary, safety)

    ELSE:
        RETURN unsupported_intent_response(), initialized.updated_log

    final_safety = evaluate_output_safety(initialized.result,
                                          initialized.safety,
                                          session_state.policy_version)
    initialized.response_plan = decide_output(initialized.result,
                                              final_safety,
                                              initialized.warnings)
    envelope = render_and_validate(initialized.response_plan)

    IF initialized.result contains proposed_records:
        RETURN envelope_with_confirmation_required(envelope),
               save_only_after_user_confirmation(initialized.result)
    RETURN envelope, initialized.updated_log
```

### Clarification resume

```text
FUNCTION resume_clarification(answer_input, saved_state):
    IF saved_state is expired OR saved_state.turn_index >= saved_state.max_turns:
        RETURN terminal_partial_or_no_estimate(saved_state), saved_state.log_snapshot
    IF answer_input.action == "cancel":
        RETURN cancellation_response(), saved_state.log_snapshot
    IF answer_input.action == "skip":
        RETURN partial_or_text_only(saved_state), saved_state.log_snapshot

    next_state = validate_and_apply_answer(saved_state, answer_input)
    next_state.turn_index = saved_state.turn_index + 1
    IF answer conflicts with prior explicit value:
        RETURN ask_resolve_conflict_if_turns_remain(next_state)
    RETURN continue_retrieval_and_calculation(next_state)
```

## 11. 原提案偽碼問題及修正表

| 原問題 | 修正 | 理由/驗證 |
|---|---|---|
| `query_nutrition` 在註解中存在，但主分支未實作 | 新增獨立 query 分支：檢索、來源驗證、候選澄清、無結果 fallback | 保證每個原 intent 均有終態；無來源不回數值 |
| `recommend` 使用未初始化 `tdee` | TDEE 改為明確 optional result，僅在明示請求、資格、完整輸入及同意時計算；否則 result 為 not-calculable | 防止沿用其他意圖狀態或假設預設值 |
| `macro_ratio` 只在 analyze 分支生成，但 recommend 可單獨呼叫 | 推薦分支自行取得摘要/宏量結果；缺資料標 partial，不引用未定義變數 | 任一 intent 可獨立執行 |
| `analysis`、`recommendation` 只有條件賦值 | 主流程初始化為明確 Result/null；依 intent 填值，輸出 formatter 只讀當前 result | 消除分支後未定義變數 |
| 普通函式內使用 `await ask_user`，async/await 不一致 | 澄清改成跨請求狀態機 `need_user_input`；工具呼叫可非同步但介面明確回傳 Result | UI 等候是會話流程，不能阻塞 server function |
| 只在一次澄清後重查，無 skip/cancel/timeout/第二次失敗流程 | `turn_index/max_turns` + 明確 skip/cancel/expired/no-candidate 終態 | 確保澄清有限且可結束 |
| 低於 0.80 的檢索信心分數和 CI 公式無校準依據 | score 只排序；閾值需驗證；range 只依證據上下界 | 避免偽機率及偽統計精確度 |
| `D.add_entry` 在未確認前直接寫入 | 先生成 draft/previews，使用者確認且保存成功後才回報記錄成功 | 降低解析錯誤造成的不可見持久化 |
| macro ratio 對不完整日誌仍輸出百分比、低於 1200 kcal 固定 DANGER | completeness 分開呈現；安全政策不採通用 kcal 門檻 | 缺值不等於零；固定門檻沒有普遍臨床依據 |
| 缺 API/資料庫錯誤分支及單位/版本追溯 | 加入 timeout、零候選、矛盾、缺營養欄位、schema 和 provenance fallback | 讓各模組錯誤可驗證且不產生偽數字 |
