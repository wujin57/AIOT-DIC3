# Literature Search Log — Stage 5

## 搜尋性質與日期

- **搜尋日期：** 2026-11-12（Asia/Taipei）。
- **方法：** 目標式、敘述性範圍搜尋；使用網路搜尋介面搭配 PubMed、ACL Anthology、出版商/會議論文頁及官方機構網域查詢，再開啟可取得的原始論文/摘要頁核對標題、作者、年份、出版資訊、DOI/URL及研究摘要。
- **非系統性回顧聲明：** 未事前登錄 protocol，未完整查詢或匯出所有資料庫結果，未做兩位審查者獨立篩選/偏差風險評估，也未建立 PRISMA 流程。因此本文稱「目標式文獻查核/敘述性回顧」，不稱 systematic review 或 exhaustive review。

## 實際可及來源與平台狀態

| 來源/入口 | 實際使用狀態 | 備註 |
|---|---|---|
| PubMed | 已搜尋並開啟既有 PubMed 紀錄，以及 2025–2026 DietAI / free-text mapping / NutriRAG / nutrient estimation / Diabot 等新近記錄。 | 可核對書目與摘要；部分研究全文未開放，因此定量和方法敘述限於可讀摘要/索引。 |
| ACL Anthology | 以 `site:aclanthology.org` 查詢 recipe NER；另查 ACL Anthology/論文頁。 | 搜尋到 recipe NER 研究；非全部 AI 技術都屬 ACL。 |
| CVF Open Access / CVPR | 搜尋 Nutrition5k CVPR 論文，官方 CVF 搜尋結果摘要和 arXiv 頁可讀。 | 開啟 CVF 詳細頁遇 HTTP 403；以官方索引摘要、arXiv metadata 和可取得論文資訊交叉核對。此為頁面抓取限制，不代表未有來源。 |
| NeurIPS Proceedings | 開啟 RAG 正式 proceedings abstract/PDF。 | 查核作者、任務、研究方法及論文結論。 |
| ICLR/ML Anthology | 開啟 ReAct proceedings record；另見 arXiv。 | 核對作者、年份及通用 Agent 任務範圍。 |
| JMIR | 開啟 FoodNER 正式期刊頁。 | 查核作者、方法、FoodBase 資料與報告結果。 |
| Frontiers in Nutrition | 開啟 Ogrinc 等人論文全文。 | 核對零樣本食品 NER/NEL 評估語料與出版資訊。 |
| Nature / Communications Medicine | 開啟 DietAI24 正式全文及出版記錄。 | 核對 2025 發表、MLLM+RAG+FNDDS、資料集及研究限制。 |
| Oxford / PubMed / White Rose | Amoutzopoulos 份量回顧之 PubMed、作者存檔頁。 | 查核回顧範圍及限制。 |
| ScienceDirect | Feher 等人 food entity linking 搜尋結果可讀；直接開啟出版商頁回傳 HTTP 403。 | 以搜尋結果呈現的出版頁 metadata/DOI 核對；已在 ledger 標示頁面抓取限制。 |
| National Academies Press | 開啟 2023 DRI for Energy 官方頁。 | 共識報告，非期刊研究。 |
| Taiwan HPA / TFDA | 開啟官方 DRI 頁、食物資料庫及相關指南頁。 | 核對資料來源存在及版本/族群適用限制；未逐筆盤點食品資料。 |
| FDA / CFIA / NICE | 查閱官方 Atwater/標示規則與飲食失調照護指南。 | 僅支持公式/通用標籤規則與專業安全邊界，不視為 DietSense 臨床驗證。 |
| IEEE Xplore / ACM Digital Library | **未直接搜尋其站內資料庫。** | 不宣稱已完成該兩庫的檢索；這是搜尋覆蓋限制，若需正式系統性回顧應補做。 |

## 實際執行的查詢（依序整理）

實際網路搜尋呼叫使用以下英文查詢或其網域限定版本；下列保留可重現的主要 query wording：

1. `site:pubmed.ncbi.nlm.nih.gov large language model dietary assessment food logging study nutrition 2024`
2. `site:aclanthology.org food named entity recognition nutrition dataset food extraction`
3. `Nutrition5k dataset dietary estimation CVPR 2021 paper official`
4. `site:pubmed.ncbi.nlm.nih.gov Mifflin St Jeor resting energy expenditure validation systematic review`
5. `Atwater general factors 4 9 4 energy calculation FDA nutrition labeling official`
6. `National Academies Dietary Reference Intakes energy equation EER adults official report 2005`
7. `USDA FoodData Central food composition data database official methods documentation`
8. `Dietary self monitoring behavioral weight loss systematic review adherence Raber 2021 PubMed`
9. `food named entity recognition food information extraction paper dataset food entity linking ACL Anthology`
10. `food named entity recognition recipe corpus peer reviewed FoodBase dataset food entity linking`
11. `ReAct Synergizing Reasoning and Acting in Language Models ICLR 2023 official proceedings`
12. `Mifflin St Jeor equation original study 1990 PubMed resting energy expenditure`
13. `Popovski Koroušić Seljak Eftimov FoodBase corpus new resource annotated food entities 2019 DOI`
14. `Ho Tseng Wu Validity image based dietary assessment methods systematic review meta-analysis 2020 13 studies 606 DOI`
15. `Amoutzopoulos Page Roberts portion size estimation dietary assessment systematic review 2020 DOI`
16. `National Academies 2023 Dietary Reference Intakes Energy report estimation limitations official`
17. `site:nature.com/articles/s43856-025-01159-0 DietAI24 authors 2025 RAG nutrition databases`
18. `site:hpa.gov.tw 國人膳食營養素參考攝取量 第八版 2025`
19. `site:hpa.gov.tw 每日飲食指南 台灣 國民健康署`
20. `NICE NG69 eating disorders recognition treatment dietary advice official guideline`

## 2026-11-12 追加查詢與篩選

因初稿完成後檢查到 2025–2026 直接相關研究，本日追加查詢並納入六項正式出版研究：

21. `"Evaluation of Large Language Models for Mapping Dietary Data to Food Databases" DOI authors 2026`
22. `"NutriRAG: unleashing the power of large language models for food identification and classification through retrieval methods" authors DOI 2026`
23. `"Large language models in food and nutrition science" FoodyLLM DOI authors 2026`
24. `"Text-based nutrient estimation by large language models" DOI authors`
25. `"Customized multimodal Diabot-GPT-4o" DOI authors Taiwan`
26. `"Text-based nutrient estimation" Chinese Food Composition Table LLM 2026 Frontiers`
27. `"Image-Based Dietary Assessment Using Multimodal Large Language Models" DOI authors SeeFood 2026`

新增核對平台包括 PubMed、USDA Agricultural Research Service、Oxford Academic/JAMIA、Elsevier、Frontiers in Nutrition 期刊全文與 AJCN/PubMed。SeeFood 在搜尋日查到的是 medRxiv 預印本，沒有以同儕審查研究納入主表或用於正式結論。追加研究讓研究缺口進一步縮窄；特別是文字型食品 mapping、文字營養估值、中國食品 LLM 評估與台灣影像評估均已有先例。

## 納入標準

1. 與 AI 之食品理解、食品 NER/NEL、RAG/Agent、影像飲食評估，或營養計算、份量估算、能量需求、自我監測直接相關。
2. 可確認標題、作者/機構、年份、期刊/會議/官方出版頁及 DOI 或官方 URL。
3. 優先納入同儕審查原始研究、系統性回顧、正式會議論文及官方共識/資料文件；基礎方法研究保留作理論脈絡。
4. 只有搜尋結果可讀時，須有正式 publication/DOI metadata 或可交叉核對的出版來源；不能單靠不明二手摘要給出數值結果。
5. 經典來源可超過近年範圍，用以支持基本概念或參考方程；避免只以「最新」取代來源品質。

## 排除標準

- 無法確認是否存在或出版資訊互相衝突、無 DOI/官方來源可查之提案暫定引用。
- 只有產品宣傳、社群貼文、未審核市場統計或沒有可重現研究設定的效能聲稱。
- 無關飲食評估任務，且未能支持本文具體主張的通用 AI 來源。
- 僅有預印本者不列入「同儕審查研究」計數；若後續使用須標註 preprint。本文主表 20 篇均能確認為正式期刊/會議研究；arXiv 僅作部分出版論文的替代可讀連結。

## 篩選與驗證流程

1. 由 Stage 5 任務列出五個 AI 主題與六個營養主題，並將 query 中的 food/dietary、entity linking/NER、RAG/agent、portion/image assessment、energy expenditure/self-monitoring 等詞組合搜尋。
2. 初篩標題、摘要、來源類型及與 DietSense 任務關聯；遇到相同研究的 arXiv/會議/期刊版本，優先引用正式版本並去重。
3. 核對正式出版頁或 PubMed/ACL/會議/機構資料的題名、作者、年份、卷期/頁碼/文章編號、DOI/URL；對定量結果回看摘要或全文中的原始分母、指標和不確定性。
4. 將每項主張連到 claim-level ledger，記錄驗證狀態、限定條件及 DietSense 不可外推之處。
5. Article Summary Table 只列已核實的 20 篇正式研究；共識報告與官方資料另列，不混入研究篇數。

## 覆蓋限制

- 搜尋不是系統性程序；未搜尋 IEEE Xplore、ACM DL 原生介面，未匯出完整檢索結果，也未計算 PRISMA flow。
- 查核以英文文獻為主；繁體中文、日韓及其他區域資料庫可能存在未納入研究。台灣混合料理和口語記錄之既有系統覆蓋不能據此宣稱不存在；且已找到台灣影像評估 Diabot 先例，研究缺口只限於本提案精確的文字對話流程與比較條件。
- 新近研究可能在搜尋索引中尚未完整收錄；FoodAI/LLM 研究變動快，投稿前需更新搜尋。
- 有些出版商頁面的自動抓取受到 403/頁面限制；本次以正式索引頁、PubMed、會議頁或 arXiv metadata 交叉核驗。全文無法取得時不作超出公開摘要/頁面可支持的細節推論。
- 本次沒有正式評估納入研究的偏差風險，也未按研究設計做 meta-analysis。
