# Stage 5 Related Work Change Log

## 原稿主題與重構策略

原提案及簡報規劃涵蓋 LLM、RAG、Food NER、多模態辨識、Agent、能量平衡、BMR/TDEE、宏量營養素、份量估算、台灣飲食指南及 Article Summary Table。其暫定文獻表/引用有部分無法由原始來源核對，且多項設計假設容易被誤述為現有方法普遍缺陷或 DietSense 已證實優勢。本階段保留研究方向與八模組意圖，依正式論文/官方頁重建 evidence base；原始 DOCX/PPTX 未修改。

## 主要修訂

| 主題 | 原稿預期/問題 | Stage 5 處理 |
|---|---|---|
| LLM + 食物文字理解 | 把一般 LLM 對話能力視作 food understanding 的充分證據。 | 納入 FoodBase、FoodNER、Ogrinc food NER/NEL 與 Feher entity-linking 研究；分開 NER、entity linking 和營養估值。 |
| RAG | 說明 RAG 可檢索外部資料，但易把其一般 NLP 結果外推為營養正確。 | 以 Lewis 2020 限定通用方法證據；納入 DietAI24 2025 作為直接相關工作，明確承認 MLLM+RAG+nutrition DB 已有影像飲食研究。 |
| Novelty/研究缺口 | 原簡報稱能力碎片化並暗示整合方案未有先例。 | 不主張「首創」或「無既有系統」；把 gap 縮至繁體中文、台灣混合餐文字描述、有限澄清與固定手動輸入比較的待測任務。 |
| Food NER/NEL | 原文列 NER 為元件，未區分標註語料、實體辨識與營養資料庫匹配。 | 加入食品本體與資料庫概念連結研究，說明英語食譜/歐洲語意資源不能直接代表台灣口語餐記。 |
| 影像營養估值 | 簡化為照片辨識方便但看不到隱藏成分。 | 加入 Nutrition5k、Ho meta-analysis 和 DietAI24；結果依資料集/參照/異質性限定，不說所有影像系統有相同誤差。 |
| 份量 | 原稿將日常份量不確定性概括而未比較驗證。 | 加入 542 種工具的系統性回顧與驗證品質限制；將 range 限定為有來源上下界而非無校準信賴區間。 |
| 能量需求/安全 | 原稿混用 BMR/REE/TDEE，並列固定 <1200 kcal 門檻。 | 以 Mifflin–St Jeor 原始研究和 National Academies 2023 說明估算範圍；移除固定通用熱量安全門檻，採專業審查的保守邊界。 |
| 宏量營養素 | 使用 4/4/9 作通用精確計算。 | 保留作一般 Atwater 近似，說明資料庫/標示可能用特定係數；優先遵循來源值與定義。 |
| 指南版本 | 引用台灣飲食指南/DRI 未固定版本。 | 核對 HPA 第八版頁面及第九版草案預告，明列實作前必須確認最新核定版本。 |
| 依從性/健康結果 | 由數位記錄推導 App 留存率或健康效果。 | 用 Raber 59-study review 限定飲食自我監測研究結果；依從性測量仍多樣，不能推論 DietSense 效益。 |
| Article Summary Table | 原始表的暫定文獻需核實書目與實驗設定。 | 建立 20 篇正式研究逐篇比較，含方法、領域知識、資料集、主要結果、限制與專題相關性；官方共識文件另列且不計篇數。 |

## 移除或降級的主張

- 移除「AI/RAG/營養資料庫整合為全球首創」及「目前沒有任何系統做整合」；DietAI24 2025 已構成直接反例；後續亦納入 FoodMapper、NutriRAG、FoodyLLM、文字型 LLM 營養估值、中國食品文字估值，以及台灣 Diabot-GPT-4o 影像評估。研究缺口因此縮至台灣繁體中文混合餐的多輪文字日誌、澄清、逐值來源與指定手動對照，並明確不宣稱台灣尚無 AI 飲食評估。
- 將「現有手動工具都繁瑣」「所有影像 App 都不能處理份量」「台灣資料庫覆蓋不足」改為需明確產品/版本或逐筆資料盤點的研究問題。
- 不把 RAG、ReAct 或 LLM 通用基準說成食物匹配/營養計算的準確率。
- 不把 4/4/9 換算或 deterministic calculation 說成準確保證；精確性受 food match、portion、source label 和公式版本影響。
- 將 TDEE、使用者依從性、SUS、任務時間、營養誤差及安全輸出表現保留為未來研究評估，不宣稱已達成。
- 不將飲食失調指南改造成模型診斷器；改列專業照護界線和待審查安全規則。

## 尚未完成的證據工作

本次搜尋不是系統性回顧；未直接搜尋 IEEE Xplore/ACM DL 原生介面，且中文與東亞食物文獻可能漏收。資料來源的台灣菜覆蓋、使用條款和版本亦未逐筆稽核。故重構提供可辯護、可測的 provisional research gap，不宣稱全領域新穎性。完整查詢與頁面限制見 [literature-search-log.md](../research/literature-search-log.md)。
