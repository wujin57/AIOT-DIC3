# DietSense 緒論 A–F 重構稿

## A. Attention Getter — 研究動機

飲食監測是營養研究與部分行為體重管理介入會採用的資料蒐集方式，但記錄本身並不等同於健康成效。世界衛生組織（WHO）估計，2024 年全球約有 26 億名成人過重，其中約 9.4 億名成人患有肥胖；台灣國民健康署依 2020–2024 年國民營養健康調查指出，18 歲以上成人中有 51.3% 達到該署的過重或肥胖標準 [1], [2]。這些統計說明營養資訊與飲食記錄具有公共衛生背景，但不能推導出某一熱量追蹤工具可預防或治療疾病。

飲食自我監測也曾被納入成人過重或肥胖者的行為介入。一項系統性回顧涵蓋 59 項研究，指出不同強度的飲食監測可能支持減重介入；然而，各研究的依從性量測方式不一，監測使用程度與結果之間的關係也未充分分析 [3]。因此，研究問題不只是能否輸出一個熱量數字，還包括記錄流程是否可操作、結果能否追溯，以及不確定性是否被清楚表達。

## B. Background — 領域與技術背景

傳統飲食記錄可透過紙本、網站或手機工具完成；使用資料庫的工作流程通常涉及查找食物候選、選擇合適品項及輸入份量。不同產品介面、資料來源與功能並不相同，因此不能假設所有工具都有相同的負擔或限制。對由多項食材組成的餐點，食物名稱、配方、烹調方式、可食份量及剩食都可能影響可計算的營養資料。份量輔助工具的系統性回顧發現，相關工具的設計與驗證方式多樣，應按工具及目標族群個別評估 [4]。

食品成分資料庫提供可檢索的營養紀錄。例如，USDA FoodData Central 提供 Food Search 和 Food Details API，可查詢其不同類型的美國食品資料 [6]；台灣食品藥物管理署亦維護台灣地區食品營養成分資料庫 [7]。資料庫存在不代表每道店家料理、品牌版本或家庭食譜均有一筆完全相符的紀錄。來源的食物狀態、營養分析方式、份量基準和版本若與實際餐點不一致，計算結果仍可能不適用。

自然語言處理與大型語言模型（LLM）可協助解析餐點描述、辨識意圖和提出澄清問題；檢索增強生成（RAG）則可把外部文件或資料項目納入模型的回應流程。RAG 的原始研究在知識密集型 NLP 任務中評估檢索與生成的整合 [8]，但該研究沒有驗證營養資料正確性，也不表示檢索能自動消除錯誤。DietSense 因而把 LLM 限定在語言理解與流程協調：營養值須來自可核對的資料來源，熱量和巨量營養素由確定性計算模組根據已確認的份量與營養密度計算，並保留來源及假設。

個人營養研究也必須限定所支持的結果。Zeevi 等人研究的是特定族群的餐後血糖反應及其預測 [9]；DIETFITS 隨機試驗納入 609 名成人，未發現該研究測試的基因型或基線胰島素分泌能預測低脂與低碳飲食的 12 個月減重差異 [10]。這些研究不能直接支持 DietSense 的個人熱量目標，也提醒本專題不可把一般食物記錄包裝成臨床個人化處方。

## C. Problem — 研究問題

DietSense 聚焦於繁體中文餐點描述的食物匹配、份量表達與營養估算。像「吃了一碗加蛋的台式牛肉麵，湯喝一半」這類描述，可能沒有明確重量或完整配方；若來源資料只有名稱相似但食物狀態、配方或份量基準不同的項目，系統不能只憑名稱輸出精確數字。台灣便當、夜市小吃、湯麵和家庭料理可作為檢驗這類資料與互動問題的情境，但本研究尚未完成代表性資料盤點，不能宣稱所有台灣混合菜都缺乏資料。

本計畫的核心研究問題為：**對於繁體中文台灣混合料理描述，結合結構化營養資料檢索、針對性澄清、確定性計算及來源追溯的對話式系統，能否產生可檢視的估算，並在預先定義的測試任務中相較於固定版本的手動搜尋與輸入流程，呈現何種估算誤差、來源追溯、記錄時間與任務完成表現？**

此問題包含可觀察的任務結果，也包含待驗證假設。可觀察結果包括 food-match 是否符合參照標籤、營養估算與參照值的差異、來源是否可追溯、完成任務所需時間及澄清輪數。至於對話是否降低負擔、估算是否足以支援日常追蹤，以及台灣資料源能覆蓋多少常見餐點，須由資料集與使用者研究回答，不能在緒論中預先當成結論。

## D. Existing Limitations — 現有方法與證據限制

**手動搜尋與輸入。** 使用者在資料庫式流程中可能需要搜尋候選食物並指定份量；這提供直接選擇和人工修正的機會，但遇到複合菜、別名或不確定份量時，仍需自行決定使用哪筆資料。各產品的工作流程和資料庫不同，本研究不主張所有飲食記錄工具都具有相同問題，也未取得足以比較特定商用應用程式的獨立效能資料。

**影像辨識及份量估算。** 照片可提供食物外觀資訊，卻不一定呈現被遮蔽的成分、油醬用量、碗中深度或實際剩食。Ho 等人的影像飲食評估系統性回顧與統合分析納入 13 項研究、606 位參與者；相對參照方法，合併結果顯示能量攝取平均低報，研究間異質性高 [5]。這是對納入方法及研究情境的整體觀察，不代表每個影像系統或每種食物都會以相同方向或幅度出錯。影像辨識正確率也不應直接視為份量或熱量估算準確率。

**語言模型數值與 RAG 限制。** LLM 可以提出自然語言解析或工具調用方案，但語句流暢不等於數值有來源。若模型直接從參數記憶回答餐點營養值，使用者和研究者可能無法重算該數字；若檢索到的是弱匹配、過期或不同熟食狀態，RAG 也可能把不適用來源帶入回答。這是本專題要以資料合約、確定性計算和來源追溯控制的設計風險，不是本研究已量化的現有模型錯誤率。RAG 的通用 NLP 證據不能替代營養任務基準測試 [8]。

**資料覆蓋與食譜差異。** USDA FoodData Central 與台灣 TFDA 食品營養資料庫提供不同範圍的資料 [6], [7]，但資料庫中的標準食品、包裝標示或官方分析值不必然等於特定店家或家庭料理。配方、份量、生熟狀態和烹調方法可能造成差異；本計畫須逐筆核對資料來源與使用條款，並以抽樣方式評估候選覆蓋，不能把「資料庫可查詢」等同「已涵蓋台灣所有料理」。

**份量不確定性及可追溯性。** 份量估算工具的證據因工具及驗證程序而異 [4]；影像方法亦呈現方法間異質性 [5]。如果輸出沒有呈現採用的食物候選、份量假設、來源欄位與公式，讀者就難以審核或重算該筆估算。這裡提出的是 DietSense 的設計要求；目前沒有完成對市售系統來源追溯功能的全面比較，因此不把來源追溯不足說成所有既有系統的共同缺點。

**個人化建議。** 以人口公式或一般指南作為個人處方可能超出資料支持範圍。既有個人化研究有特定研究族群和結果，且並非所有預設個人特徵都能識別更適合的飲食；例如 DIETFITS 對其指定的基因型與胰島素交互作用未發現顯著差異 [10]。DietSense 的第一研究範圍因此是記錄、估算和一般資訊，不推論個人疾病、代謝因果或治療需求。

綜合而言，現有方法並非沒有用途：資料庫查詢可提供可追溯候選，影像可協助取得外觀線索，LLM/RAG 可支援語言互動和外部資料查找。需要檢驗的是，如何在台灣混合餐點的模糊描述下，將這些能力組合成有明示資料來源、份量假設、失敗路徑與安全界線的任務流程；目前證據尚不足以將這描述為全領域已證明的研究缺口。

## E. Innovation — 擬議設計重點

本研究的設計主張不是「首次」整合某些技術，而是提出一套可被逐項評估的 DietSense 工作流程：

1. 以對話理解使用者意圖和餐點欄位，並保留原始描述，讓使用者可修正抽取結果。
2. 從已登錄的營養資料來源檢索結構化候選，逐筆保留來源 ID、版本、營養欄位及食物狀態。
3. 將份量處理與營養計算分開：在食物匹配或關鍵份量缺失時提出有限次澄清；數字則由確定性 Analytics Engine 計算，而非交由 LLM 自由生成。
4. 僅在來源或份量具可說明上下界時提供 plausible estimate range，並列出假設；未校準範圍不稱為統計信賴區間。
5. 由 Domain Knowledge 與 Decision/Recommendation 模組限制為一般資訊型回應，對危險或超出範圍的個人化要求採限制/拒答；政策仍須由營養與心理健康專業人員審查。

這些設計分工對應 Stage 3 的原提案八模組，而非新增與原專題無關的系統架構。其效益必須由估算誤差、資料可追溯性、澄清負擔、任務時間、完成率及安全測試結果檢驗。

## F. Contributions — 預期研究貢獻

本提案預期形成以下四項可評估貢獻；每項均是未來工作，並非已完成成果：

| 預期貢獻 | 對應問題 | 設計元件 | 擬議評估證據 |
|---|---|---|---|
| 1. 建立繁體中文台灣餐點描述與參照營養標籤的研究資料集及標註流程 | 複合餐描述、份量與配方標籤不易直接比較 | 分層抽樣、來源/食譜/份量記錄、雙人標註及專業裁決 | 預計 500 筆資料；報告類別覆蓋、標註一致性、參照值來源及可評估比例，不將其宣稱為全台代表樣本。 |
| 2. 提出八模組下可追溯的檢索—計算工作流程 | 相似食物候選和不同來源欄位可能使估值難以重算 | Retrieval provenance、source/version mapping、確定性 Analytics | 以 food identification、kcal/macronutrient error、source traceability 及固定輸入重算一致性評估。 |
| 3. 設計並測試針對食物身份/份量缺漏的澄清與不確定性輸出 | 自然語言餐點描述可能未提供足夠欄位 | 有限澄清狀態機、skip/fallback、evidence-bounded plausible estimate range | 量測澄清輪數、任務完成/放棄、時間、range width/coverage 及錯誤接受率。 |
| 4. 提出一般資訊與安全邊界的評估框架 | 飲食記錄與個人化建議不可被誤作醫療決策 | 版本化 SafetyDecision、拒答/限制回應、資料最小化流程 | 以專業審查的安全測試案例、unsafe completion、來源/政策一致性及 20 人、7 日可行性研究作初步檢視；不宣稱臨床安全或健康療效。 |

計畫中的 500 筆資料集、固定手動搜尋/輸入 baseline、餐點誤差與記錄時間指標，以及 20 位成人、7 日可行性研究，均依 Stage 3 評估計畫執行前另行定稿。原提案的 >85% ±20% 誤差帶、縮短 60% 記錄時間和 SUS >70 僅是候選目標，尚非結果或承諾。

## A–F 與 A2Z G–L 對照

| A–F 段落 | A2Z 功能 | 對應方式 |
|---|---|---|
| A Attention Getter + B Background | G General | 先以公衛資料和監測研究說明重要性，再交代記錄、資料庫及 AI 技術背景。 |
| C Problem + D Existing Limitations | H However | 從具體任務困難導入現有方法限制；使用條件化證據，避免把差異說成普遍失效。 |
| B Background + D Existing Limitations | I In Literature | 依資料庫/人工記錄、份量工具與影像方法、LLM/RAG 及個人化研究等類別摘要相關證據；不是完整 Related Work 系統回顧。 |
| D Existing Limitations + C Problem | J Judgement | 比較方法適用範圍和限制，指出目前可以下的結論及尚待驗證的問題。 |
| E Innovation + F Contributions | K Keypoint | 提出八模組內的設計整合和四項可評估預期貢獻，不宣稱 field-wide first。 |
| Academic Introduction 結尾之文件結構段 | L List Organization | 說明 proposal 後續章節安排；僅描述規劃中的 Related Work、Deep Research、Proposed Design 與 Evaluation，不宣稱尚未完成章節已完成。 |

## 引用資料

完整 claim-level evidence、驗證狀態、作者/機構、出版年、DOI/官方網址及限制見 [Introduction Evidence Ledger](../research/introduction-evidence-ledger.md)。

1. World Health Organization, “Obesity and overweight,” fact sheet, updated 2026-10-07. https://www.who.int/news-room/fact-sheets/detail/obesity-and-overweight.
2. Taiwan Health Promotion Administration, 〈響應世界肥胖日　兩招啟動健康管理〉, 2026-03-04. https://www.hpa.gov.tw/5020/19885/n.
3. M. Raber et al., “A systematic review of the use of dietary self-monitoring in behavioural weight loss interventions: delivery, intensity and effectiveness,” *Public Health Nutrition*, 24(17), 5885–5913, 2021. doi:10.1017/S136898002100358X.
4. B. Amoutzopoulos et al., “Portion size estimation in dietary assessment: a systematic review of existing tools, their strengths and limitations,” *Nutrition Reviews*, 78(11), 885–900, 2020. doi:10.1093/nutrit/nuz107.
5. D. K. N. Ho et al., “Validity of image-based dietary assessment methods: A systematic review and meta-analysis,” *Clinical Nutrition*, 39(10), 2945–2959, 2020. doi:10.1016/j.clnu.2020.08.002.
6. USDA Agricultural Research Service, “FoodData Central API Guide,” https://fdc.nal.usda.gov/api-guide/.
7. Taiwan Food and Drug Administration, “台灣地區食品營養成分資料庫,” https://www.fda.gov.tw/tc/site.aspx?r=1647620244&sid=271.
8. P. Lewis et al., “Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks,” *Advances in Neural Information Processing Systems*, 33, 9459–9474, 2020. https://arxiv.org/abs/2005.11401.
9. D. Zeevi et al., “Personalized Nutrition by Prediction of Glycemic Responses,” *Cell*, 163(5), 1079–1094, 2015. doi:10.1016/j.cell.2015.11.001.
10. C. D. Gardner et al., “Effect of Low-Fat vs Low-Carbohydrate Diet on 12-Month Weight Loss in Overweight Adults and the Association With Genotype Pattern or Insulin Secretion: The DIETFITS Randomized Clinical Trial,” *JAMA*, 319(7), 667–679, 2018. doi:10.1001/jama.2018.0245.
