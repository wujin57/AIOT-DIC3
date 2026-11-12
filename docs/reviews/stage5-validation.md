# Stage 5 — Related Work Validation

## 判定摘要

**整體：PASS（文件與必要查核要求完成）。** 八份指定文件均已建立；20 篇同儕審查研究及 1 份共識報告的書目和有限主張已核對；AI 五個主題、營養六個主題、文章比較表與 A2Z M–O 均有覆蓋；跨階段差異已處理為明確的研究定位，而非靜默修改前階段文件。搜尋非系統性、地區資料涵蓋及未來實證結果屬已揭露的研究限制，不是本階段文件缺陷。

## 交付文件盤點

| 文件 | 內容 | 狀態 |
|---|---|---|
| `docs/refactored/related-work-ai.md` | AI 五主題 Related Work | 完成 |
| `docs/refactored/related-work-domain.md` | 營養領域六主題 Related Work | 完成 |
| `docs/refactored/related-work-academic.md` | 統整式學術章節，非前兩文件直接拼接 | 完成 |
| `docs/research/article-summary-table.md` | 20 篇研究及 1 份共識報告的比較表/書目，另列官方參照資料 | 完成 |
| `docs/research/literature-search-log.md` | 搜尋日期、實際查詢、平台狀態、準則與限制 | 完成 |
| `docs/research/related-work-evidence-ledger.md` | claim-level 支持、狀態、來源與限制 | 完成 |
| `docs/reviews/related-work-change-log.md` | 原稿對照、修訂、刪除與降級主張 | 完成 |
| `docs/reviews/stage5-validation.md` | 本階段驗證與最終判定 | 完成 |

## 文獻核實與 Article Summary Table 稽核

- 表格共 **20 篇正式期刊或會議研究**及 1 份報告：基礎 AI/資訊抽取/Agent/影像研究 RW01–RW08，營養/份量/代謝/自我監測研究 RW09–RW11、RW13–RW15，直接文字映射/營養 LLM 及台灣影像研究 RW16–RW21；其中 RW08、RW16–RW21 等跨越 AI 與營養領域，分類有重疊。National Academies 2023 共識報告（RW12）及官方指南/資料源另列，不計入同儕審查篇數。
- 每個研究列均具正式題名、作者/年份、問題、方法、領域資料、資料集/證據類型、有限研究發現、限制及與 DietSense 關聯。
- 對不使用 AI 的系統性回顧、隨機試驗、預測方程及數學模型，AI Method 明確寫為 Not applicable，而非虛構模型方法。
- Quantitative results 在表中只保留原論文可核對的指標/分母，例如 Ho 13 studies/606 participants、WMD −179.32 kcal/I²=89%，以及 FoodNER 的模型報告區間；不推論 DietSense 效能。
- 預印本連結只用於部分已正式發表論文的替代閱讀；主表所列研究均可核實正式出版/會議資訊。RAG/Agent 通用任務結果與營養任務分開陳述。
- DietAI24 2025 已確認 MLLM+RAG+FNDDS 的照片估值框架；追加核對亦納入 FoodMapper、NutriRAG、FoodyLLM、兩項文字型營養估值研究及台灣 Diabot 影像評估。原稿可能造成的「首度整合」「文字映射尚未研究」或「台灣尚無 AI 飲食評估」主張均已撤下。

## 搜尋協定覆蓋

**PASS（依敘述性範圍搜尋承諾）；不宣稱系統性回顧。** 搜尋紀錄列明 2026-11-12 日期、27 條實際查詢、納入/排除、篩選/核實步驟、PubMed/ACL/CVF/NeurIPS/ICLR/JMIR/Frontiers/Nature/National Academies/HPA/TFDA/FDA/NICE 等實際入口與限制。已明確說明未直接檢索 IEEE Xplore/ACM Digital Library 原生介面，亦未做雙人 screening/PRISMA 或偏差評估。

## AI 與營養研究覆蓋

| 任務要求 | 驗證結果 | 對應 |
|---|---|---|
| A. LLM dietary understanding | PASS | Food NER/NEL、ChatGPT zero-shot linking、FoodMapper 文字映射與 NutriRAG 飲食日誌分類；區分抽取/分類/映射和營養數值。 |
| B. RAG | PASS | Lewis et al. 基礎 RAG；DietAI24 照片營養資料檢索、NutriRAG 文字分類及 FoodyLLM 領域模型，分別限定任務。 |
| C. Food NER / extraction | PASS | FoodBase、FoodNER、E.Care entity linking、Cafeteria 語料。 |
| D. Image/multimodal assessment | PASS | Nutrition5k、Ho meta-analysis、DietAI24 及台灣 Diabot 影像先例；不將影像成果外推至文字任務。 |
| E. Agent tool use | PASS | ReAct 通用工具使用並明確限定不作營養證據。 |
| Energy/macronutrient calculation | PASS | 動態能量平衡、來源密度縮放、Atwater 因子/標示規則與限制。 |
| Food composition databases | PASS | USDA FDC、TFDA 官方入口；coverage 尚未被誇稱。 |
| Portion estimation | PASS | Amoutzopoulos review 及影像評估限制。 |
| REE/TDEE | PASS | Mifflin–St Jeor 原始公式、NASEM 2023 EER 與適用界線。 |
| Guidance/safety | PASS | HPA DRI/指南及版本狀態、NICE 專業照護界線。 |
| Self-monitoring/adherence | PASS | Raber 59-study review 與依從性量測限制。 |

## Research gap 與 A2Z M–O

- **M Mainstream Approaches：PASS。** 學術章節按食品實體/連結、RAG/Agent、影像、營養資料/份量、REE 與飲食監測分類主流方法。
- **N Obstacles and Limitations：PASS。** 評估語言與食物文化外推、份量和視覺測量誤差、資料庫版本/coverage、個人預測誤差、自陳誤差及研究設計限制。
- **O Opportunity / Research Gap：PASS。** 研究機會限定為在已存在的文字映射、文字營養估值、領域模型及台灣影像研究之上，檢驗台灣繁體中文混合菜多輪文字記錄的 food matching、澄清、逐值來源追溯與確定性計算，並與固定手動搜尋輸入比較誤差、時間、完成率與澄清負擔；不聲稱文字研究或台灣 AI 飲食評估不存在，也不聲稱 field-wide novelty。

## 跨階段一致性

| 維度 | 結果 | 核對結論 |
|---|---|---|
| Stage 1 Abstract / Stage 4 Introduction | PASS | 保留對話式繁中飲食記錄、來源依據估算、不確定性表達及前瞻研究語氣。 |
| Stage 2 Deep Research | PASS | 對份量、資料覆蓋、個人化、安全與依從性爭議保持未定論並列證據限制。 |
| Stage 3 DESIGN.md / architecture | PASS | 對齊八模組、LLM 協調、結構資料 retrieval、deterministic Analytics、有限澄清、安全 gate 和 provenance；不新增主架構。 |
| Nutrition equations | PASS | REE 與 TDEE 分清；公式為一般估算，不轉成處方；計算需保留 source/formula version。 |
| Data-source assumptions | PASS | USDA/TFDA 僅作候選來源；使用授權、版本及台灣菜覆蓋待 implementation audit。 |
| Evaluation plan | PASS | 500 筆、固定 manual baseline、20 人 × 7 日均為計畫；不稱已完成或代表性樣本。 |
| Safety/expected contributions | PASS | 不診斷、不宣稱臨床安全或療效；未來貢獻不寫成結果。 |
| Research novelty | PASS | 承認 DietAI24 直接先例；Novelty 限於待研究任務與比較。 |

## 自我驗證及修正

已完成三輪自我驗證。第一輪發現並修正 `related-work-change-log.md` 的搜尋紀錄相對連結；第二輪確認原八份文件的非空狀態、引用鍵及章節覆蓋；第三輪加入 2025–2026 研究後，重新核對比較表共 20 篇正式研究、RW01–RW21 含一份共識報告、全部書目鍵對應、相對 Markdown 連結有效，並檢查長段落重複與表格行數。另將 FooDB 的 9,910 條目與 NHANES-to-DFG2 的 256 條目清楚標示為資料庫規模，不誤作配對測試樣本數。**研究內容修正：** 新納入 FoodMapper、NutriRAG、FoodyLLM、文字型 LLM 營養估值、中國食品估值及台灣 Diabot；把新穎性改限於具體任務比較。SeeFood 僅見 medRxiv 預印本，仍排除於同儕審查篇數。原提案中的 <1200 kcal/day 通用門檻仍不採用；無證據的產品普遍缺陷說法亦已移除。對頁面存取受限的來源，使用可讀正式 metadata/摘要交叉核驗並註明限制。

## 未解限制

1. 本次非系統性搜尋，未直接檢索 IEEE Xplore/ACM DL、未做 PRISMA、雙人篩選或偏差評估；不得稱 systematic review。
2. 中文及東亞語言文獻可能漏收；台灣混合菜與繁體中文對話任務的既有基準仍需專門搜尋。
3. TFDA/USDA/食譜來源逐筆 food coverage、資料版本、使用授權及菜色候選品質尚未盤點。
4. DietSense 尚未實作或測試；估算誤差、使用時間、可用性、依從性和安全表現均未知。
5. HPA 第九版 DRIs 的核定/適用狀態與安全規則需於設計凍結前由官方來源及專業人員確認。

## 最終評估

**PASS — Stage 5 八份交付文件完成；20 篇同儕審查研究與一份共識報告列入比較表，六項 2025–2026 新近研究已加入證據鏈並修正研究缺口。** 上述限制已明確記錄為搜尋範圍與未來研究事項；不構成未交付文件或偽造證據。Stage 5 到此停止，不開始 Stage 6。
