# Stage 3 — System Design Refactor 驗證

## 總結與判定

**PARTIAL。** 五份設計交付物均已建立，需求、八模組架構、資料合約、演算法、評估和追溯均有明確內容。偽碼中原先未處理的 query intent、未初始化變數、同步等待澄清及無限/未定義 fallback 已修正。安全政策、台灣資料來源與覆蓋、參照標籤 protocol、招募/研究倫理，以及 Mermaid parser 驗證仍未完成，不能因此宣稱系統已安全、有效或可直接實作上線。

## 交付物盤點

| 檔案 | 狀態 | 內容 |
|---|---|---|
| `DESIGN.md` | 完成 | 主設計文件：範圍、需求 ID、八模組概述、數值/安全原則、實作映射及 FR 追溯矩陣 |
| `docs/design/architecture.md` | 完成 | 五個 Mermaid 圖、八模組責任/介面/錯誤/驗收、九類資料合約與回應封套 |
| `docs/design/algorithms.md` | 完成 | A–H 指定演算法、額外 I 資料刪除程序、共通型別、主流程/澄清偽碼、原稿偽碼修正對照 |
| `docs/design/evaluation-plan.md` | 完成 | 500 筆資料集、分層、參照標籤、雙標註/裁決、baseline、指標公式、分析及 20 人 × 7 日可行性研究 |
| `docs/reviews/stage3-validation.md` | 本文件 | 本次自我驗證、覆蓋矩陣、修正與未解風險 |

## 需求覆蓋矩陣

| Stage 3 要求 | 結果 | 驗證摘要 |
|---|---|---|
| System requirements 有功能/非功能 ID、來源、優先級、驗證法及準則 | PASS | `DESIGN.md` 包含 FR-001–FR-012、NFR-001–NFR-010，需求皆含 origin、priority、verification 和 acceptance criterion。 |
| 保存八個概念模組 | PASS | Architecture 文件明列 ① User/Application、② Input Processing、③ Planner/Reasoning、④ Data Retrieval、⑤ Analytics Engine、⑥ Domain Knowledge、⑦ Decision/Recommendation、⑧ Output/Interaction。 |
| 每模組有責任、I/O、依賴、錯誤復原、需求及驗收 | PASS | `architecture.md` 模組表逐列給出上述資訊；介面引用一致的概念資料型別。 |
| LLM/數值計算信任界線 | PASS | LLM 僅提解析/對話，候選需 schema/domain validation；Analytics 僅接受有來源的結構化數值，LLM 不能提供 authoritative nutrition value。 |
| 必要五類 Mermaid 圖 | PASS（手動檢閱） | 五個必要圖（高階架構、食物記錄 sequence、澄清 state、營養計算 flow、失敗/fallback flow）均存在，另有一張信任邊界圖。環境沒有 `mmdc` 或 Mermaid CLI，未能 parser 驗證；已人工檢查節點、分支及 code fence。 |
| 九個指定資料結構、型別/單位/驗證/來源/缺值 | PASS | `architecture.md` 定義 UserInput、FoodEntity、PortionEstimate、NutritionCandidate、NutritionRecord、CalculationResult、ClarificationRequest、DailySummary、SafetyDecision。未知值用 null/status，不等同 0。 |
| 演算法 A–H 及測例、失敗處理 | PASS | `algorithms.md` 定義 A–H：抽取、檢索、份量/澄清、確定性計算、彙總、REE/TDEE、估算範圍、安全。另加 I 支援 consent/retention/deletion 需求。 |
| 偽碼所有分支和變數已初始化、澄清有限終止 | PASS | `handle_request` 初始化 result/response/safety/log/warnings；每個 intent 有分支/unsupported 終態；澄清跨請求恢復，使用 turn index/max、skip/cancel/expired 分支。 |
| 研究計畫有 500 筆、參照標籤、標註一致性、比較基線 | PASS（計畫規格） | `evaluation-plan.md` 定義範圍、建議分層、A–D 參照品質、雙標/專業裁決、κ/ICC/Bland–Altman、group split 與固定 baseline。實際比例及 protocol 仍待預註冊。 |
| 指標有定義/計算方法 | PASS（規格） | 定義識別率、coverage、kcal MAE/APE/±帶、macro MAE、range coverage/width、時間、澄清負擔、來源追溯、失敗、完成率及 SUS。 |
| 20 位、7 日研究、同意與隱私 | PASS（研究計畫） | 文件將其界定為 feasibility/usability，不作減重療效研究；涵蓋順序效應、退出、倫理審查、知情同意、第三方模型資料處理及資料最小化。 |
| FR requirement traceability 到 module/algorithm/metric/AC | PASS | `DESIGN.md` 需求追溯矩陣覆蓋 FR-001–FR-012，含原提案、模組、算法、指標及 AC-001–AC-012。 |
| 學術誠信/不虛構結果與門檻 | PASS | 候選目標標為未驗證；沒有捏造測試結果、文獻或效能保證；外部來源與臨床規則需審查之處均保留限制。 |
| Stage scope protection | PASS | 本階段只新增 DESIGN.md、docs/design 三份文件及本驗證報告；未修改原始文件、Stage 1/2、Introduction、Related Work；未實作應用、未使用 OpenSpec、未提交或推送。 |

## 架構一致性與偽碼驗證

- **模組數/順序：** 八個原提案模組全數保留，Mermaid 高階圖及 module table 一致。
- **介面/資料合約：** ④ 只回傳帶 source/version 的候選；⑤ 只接受經驗證記錄；⑥ 提供版本化規則；⑦ 安全/資料充分性決策；⑧ 僅格式化，不重算數值。跨文件引用的資料型別名稱一致。
- **初始化/分支：** 主流程一開始建立 `result`、`response_plan`、`parsed`、`safety`、`updated_log`、`warnings`；log/query/analyze/recommend/unsupported 均有明確路徑。`tdee_estimate`、宏量資料和每日摘要為 optional Result，不跨意圖隱式共用。
- **澄清終止：** 每個澄清請求含 `turn_index/max_turns`；回答、跳過、取消、過期、衝突和達上限均有終態。UI 往返以序列化狀態表示，不讓伺服器函式同步等待人類輸入。
- **缺值/單位：** kcal、g、kcal/100g 和 g/100g 在資料合約及演算法一致；未知與 0 分離；混合菜缺值、密度狀態不合、單位不明時只做部分結果或不計算。
- **確定性：** 相同 source snapshot、formula version、份量與輸入會產生相同 calculation；所有 rounding 固定在輸出層。候選排序分數與營養數值分開。
- **範圍：** plausible estimate range 需要有來源的上下界；未校準 rank score/固定誤差率不可生成統計信賴區間。

## 證據、來源與候選結果檢查

五份 `references/` 文件存在且 Stage 0/2 已提取 DOCX、PDF、PPTX 文字及表格/投影片內容。Stage 3 對照原 proposal 的八模組、flowchart 和主偽碼，以及簡報第 12–21 張的架構/評估和作業規範第 2–4 頁。設計中的科學邊界延用 Stage 1/2 已查核來源與未解事項；Mifflin–St Jeor 用於一般 REE 估算的表述及公式名稱需對照 [deep-research-references.md](../research/deep-research-references.md) [4], [19]。資料源、配方和安全規則不因在設計中列出就視為已取得或已核准。

原稿偽碼問題已在 `algorithms.md` 修正表逐一說明：未處理 query_nutrition、`tdee/macro_ratio/analysis/recommendation` 未初始化、`await` 使用不一致、一次性澄清無終止保障、未校準信心分數轉 CI、寫入過早、固定 1200 kcal 門檻及缺乏工具錯誤 fallback。

## 連結、佔位符與 Mermaid 檢查

- 五份交付文件存在且非空；跨文件本地 Markdown 連結以相對路徑解析，無已知失效連結。
- 未發現未處理的空白欄位；文件中明列的「待確認/待審查/待預註冊」是研究風險，不是空白內容。
- `architecture.md` 有 6 個 Mermaid code fence：5 個指定流程/架構圖及 1 個信任邊界圖。未安裝 Mermaid CLI/parser（遵守不安裝依賴的限制）；只完成人工語法/流程檢查，Mermaid parser verification **未完成**。

## 修正/澄清項目

1. 將 NutritionRecord 的確認/草稿/文字-only 狀態分開，並要求保存確認，避免解析猜測被當成實際日誌。
2. 將來源匹配 score 與機率分開；估算上下界必須有證據，不用固定百分比假裝校準。
3. 以 `null + unknown/status` 區分未知和數值零；摘要對缺項顯示 partial/incomplete。
4. 將澄清重構為有上限、可跳過、可取消、跨請求 resume 的狀態流程。
5. 修正 query_nutrition 與 recommend 的獨立流程，所有可選計算變數均明確初始化/判斷可用性。
6. 移除原草稿固定低於 1200 kcal 即危險的機器判定；不建立未驗證醫療門檻。
7. 將研究目標值重新標為候選 threshold，增加資料參照 SOP、baseline 固定、標註一致性和倫理審查要求。
8. 增加 I 資料生命週期算法，讓同意/刪除需求有明確可測流程，並將備份/第三方刪除能力列為待驗證。
9. 將 FR-002 的欄位擷取驗收準則獨立編為 AC-002，使 FR-001–FR-012 全部可逐 ID 追溯。

## 尚未解決的風險

1. **專業政策審查：** Recommendation、安全 trigger、特殊族群限制和轉介文案需營養/心理健康專業人員審查；法規與隱私義務需校方/法務確認。
2. **資料來源及授權：** 台灣食品資料的版本、商用/研究使用條款、欄位品質與店家食譜代表性仍未確認；USDA 不能代替台灣菜資料。
3. **參照值誤差：** recipe-derived labels 不是實驗室真值；需凍結重量、可食部、烹調與油醬估算 SOP，並按參照品質分層分析。
4. **樣本/統計能力：** 500 筆和 20 人 × 7 日尚無 power/精度計算；不足以支持廣泛族群、臨床安全性或健康療效結論。
5. **Mermaid tooling：** 可用環境沒有 parser，需在有 Mermaid 支援的審閱環境再做 parser-level validation；沒有為此安裝工具。
6. **部署/供應商：** LLM API、語音、儲存和刪除政策尚未選型；不可在選型前承諾延遲、保留期限或第三方刪除行為。
7. **TDEE公式適用：** 資格限制及 sex-specific 公式選擇屬待專業審查政策；如不符合或輸入不足，設計上預設不顯示個人化 TDEE。

## 最終評估

**PARTIAL。** 所有指定文件與核心工程規格已完成，需求/演算法/模組/評估追溯完整，且技術性偽碼問題已修正。PARTIAL 原因是 Mermaid 尚未 parser 驗證，並且資料源、專業安全審核、倫理流程和正式 protocol 尚待外部決定。此判定不代表已測試應用或 Stage 4 實作已開始。
