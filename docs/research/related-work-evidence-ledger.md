# Related Work Evidence Ledger

## 驗證狀態定義

- **VERIFIED**：正式出版頁、PubMed/官方會議頁或官方機構文件直接支持該有限主張。
- **PARTIALLY VERIFIED**：來源支持部分技術/研究事實，但對特定語言、菜系、族群、效益或推廣範圍尚未驗證。
- **UNVERIFIED**：查核材料不足以支持該主張；不應以事實口吻使用。

本文的敘述性搜尋不是系統性回顧；狀態只說明目前列出的證據支持範圍，不代表對全領域做過窮盡檢索。

## Claim-level evidence

| ID | 精確主張 | 來源 / 作者 / 年 | DOI 或官方 URL | 狀態 | 證據與主要限制 | 使用位置 |
|---|---|---|---|---|---|---|
| RW-E01 | RAG 把參數化生成與非參數化檢索結合，並在知識密集型 NLP 任務評估。 | Lewis et al., NeurIPS 2020 | https://papers.nips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html | VERIFIED | 正式論文頁列方法、Wikipedia index 及 QA/事實任務；不支持營養準確率或零錯誤。 | related-work-ai §B; academic §2 |
| RW-E02 | ReAct 在通用任務中交錯語言模型推理及工具行動。 | Yao et al., ICLR 2023 | https://mlanthology.org/iclr/2023/yao2023iclr-react/ | VERIFIED | ICLR proceedings record 可查；非飲食 Agent 實驗，不驗證安全或營養功能。 | AI §E; academic §2 |
| RW-E03 | FoodBase 提供人工校訂食譜食品實體語料；curated corpus 為 1,000 recipes。 | Popovski et al., Database 2019 | https://doi.org/10.1093/database/baz121 | VERIFIED | 期刊 PDF/文章 metadata 支持題名、作者、年份及資料集；其語言、來源和標籤範圍不等於台灣餐點日誌。 | AI §A/C; table RW03 |
| RW-E04 | FoodNER 使用多個微調 BERT/BioBERT 模型處理食品 NER/標籤分類，報告 macro F1 約 73.39%–78.96%。 | Stojanov et al., JMIR 2021 | https://doi.org/10.2196/28229 ; https://www.jmir.org/2021/8/e28229 | VERIFIED | 正式期刊頁列 15 模型、FoodBase 資料、ontology 任務及結果；數值只適用論文特定類別/測試設定。 | AI §A/C; table RW04 |
| RW-E05 | Ogrinc 等人評估 ChatGPT-3.5/4 在 CafeteriaSA/FCD 的 food NER/NEL。 | Ogrinc, Koroušić Seljak & Eftimov, Frontiers in Nutrition 2024 | https://doi.org/10.3389/fnut.2024.1429259 | VERIFIED | 正式全文列語料及模型；摘要/食譜語料並非繁體中文日誌；不將結果推廣到營養估值。 | AI §A/C; table RW05 |
| RW-E06 | E.Care 研究包含 664 food concepts、468 recipes，並比較 food entity linking 方法。 | Feher et al., Information Processing & Management 2023 | https://doi.org/10.1016/j.ipm.2023.103463 | VERIFIED | 出版商搜尋結果提供完整題名、作者、卷期/文章編號、方法和結果；直接頁面抓取受 403 限制，故未超出可見摘要細述。語料資料不可公開。 | AI §A/C; table RW06 |
| RW-E07 | Nutrition5k 是約 5,000 道餐點的視覺/深度與營養標註資料集。 | Thames et al., CVPR 2021 | https://openaccess.thecvf.com/content/CVPR2021/html/Thames_Nutrition5k_Towards_Automatic_Nutritional_Understanding_of_Generic_Food_CVPR_2021_paper.html ; https://arxiv.org/abs/2103.03375 | VERIFIED | CVPR proceedings 搜尋頁摘要及資料集作者頁可核；CVF 詳細頁自動抓取回 403。來源為美國餐廳情境，不能宣稱台灣代表性。 | AI §D; academic §3; table RW07 |
| RW-E08 | DietAI24 將 MLLM、RAG、FNDDS 用於照片食物代碼/份量/營養估算，並在 ASA24/Nutrition5k 評估。 | Yan et al., Communications Medicine 2025 | https://doi.org/10.1038/s43856-025-01159-0 | VERIFIED | Nature 正式全文列方法、資料、基線和限制；其報告的效能只屬原資料/影像任務及方法，不能外推繁中台灣文字記錄。 | AI §B/D, synthesis; academic §§2,5; table RW08 |
| RW-E09 | 影像式飲食評估回顧納入 13 studies/606 participants，能量合併差異 WMD −179.32 kcal、I²=89%。 | Ho et al., Clinical Nutrition 2020 | https://doi.org/10.1016/j.clnu.2020.08.002 ; https://pubmed.ncbi.nlm.nih.gov/32839035/ | VERIFIED | PubMed摘要列分母、比較方法和數據；異質性高，不能套用成所有系統固定低報。 | AI §D; domain §C; academic §3; table RW09 |
| RW-E10 | 份量估算回顧檢視 334 studies、542 estimation elements，僅少數 validation studies 品質高。 | Amoutzopoulos et al., Nutrition Reviews 2020 | https://doi.org/10.1093/nutrit/nuz107 ; https://pubmed.ncbi.nlm.nih.gov/31999347/ | VERIFIED | PubMed摘要及正式 DOI 支持；方法及適用族群異質，不得聲稱所有工具無效。 | domain §C; academic §3; table RW10 |
| RW-E11 | Mifflin–St Jeor REE 方程源自 498 位健康成人的間接熱量測定資料。 | Mifflin et al., AJCN 1990 | https://doi.org/10.1093/ajcn/51.2.241 ; https://pubmed.ncbi.nlm.nih.gov/2305711/ | VERIFIED | PubMed全文摘要列樣本及公式；預測式不是個人測量，RE E 與 TDEE 概念不可混用。 | domain §D; academic §4; table RW11 |
| RW-E12 | 2023 National Academies DRI 能量報告更新 EER 並討論自陳能量攝取的系統性測量誤差。 | National Academies of Sciences, Engineering, and Medicine, 2023 | https://doi.org/10.17226/26818 | VERIFIED | 官方共識報告支持；適用美國/加拿大參照人群，不可取代台灣 HPA 指引。 | domain §D; academic §4; table RW12 |
| RW-E13 | Raber 回顧 59 項成人過重/肥胖行為減重介入研究，依從性量測不一致且使用—結果關聯分析有限。 | Raber et al., Public Health Nutrition 2021 | https://doi.org/10.1017/S136898002100358X ; https://pubmed.ncbi.nlm.nih.gov/34412727/ | VERIFIED | PubMed 摘要列研究數、形式和限制；不能證明指定 App 或 DietSense 的結果。 | domain §F; academic §4; table RW13 |
| RW-E14 | Hall 的動態能量失衡模型說明體重對能量變化隨時間反應，不宜將 kcal 轉換為固定線性體重變化。 | Hall et al., The Lancet 2011 | https://doi.org/10.1016/S0140-6736(11)60812-X | VERIFIED | 原研究以動態模型量化；非 DietSense 餐點評估或臨床個人預測驗證。 | domain §A; table RW14 |
| RW-E15 | DIETFITS 納入 609 名成人，未發現指定基因型/基線胰島素指標預測其低脂與低碳介入的 12 月減重差異。 | Gardner et al., JAMA 2018 | https://doi.org/10.1001/jama.2018.0245 | VERIFIED | 隨機試驗及指定 interaction 結果；不能推廣成「所有個人化營養均無效」。 | table RW15; cross-stage reference |
| RW-E16 | USDA FoodData Central 有食物組成資料與 Search/Details API；TFDA 維護台灣地區食品營養成分資料庫。 | USDA ARS / Taiwan FDA, official pages | https://fdc.nal.usda.gov/api-guide/ ; https://www.fda.gov.tw/tc/site.aspx?r=1647620244&sid=271 | VERIFIED | 官方頁支持 API/database 存在；未完成資料版本、授權、菜色欄位及實際 coverage audit。 | domain §B |
| RW-E17 | 台灣 HPA 有 DRIs/飲食指南官方資料，並在 2025 公告第九版 DRIs 草案預告資訊。 | Taiwan Health Promotion Administration, updated materials | https://www.hpa.gov.tw/Pages/Detail.aspx?feature=featurea13&kv=default&nodeid=4248&pid=12285 ; https://www.hpa.gov.tw/Pages/Detail.aspx?nodeid=5020&pid=19745&sid=20155 | VERIFIED | 官方頁支持第八版資源與第九版草案狀態；上線/核定版本應在實作前確認。 | domain §E |
| RW-E18 | Atwater 一般因子常用蛋白質/碳水/脂肪 4/4/9 kcal/g；法規也允許特定食品因子或其他合規方法。 | FDA eCFR / CFIA, official labelling guidance | https://www.ecfr.gov/current/title-21/section-101.9 ; https://inspection.canada.ca/en/food-labels/labelling/industry/nutrition-labelling/elements-within-nutrition-facts-table | VERIFIED | 官方標示規則說明能量換算方式；不代表任意營養日誌可無條件用通用 4/4/9 覆蓋資料庫原值。 | domain §A |
| RW-E19 | NICE NG69 將飲食失調評估/治療置於專業照護框架，飲食諮詢有多專業照護脈絡。 | NICE, NG69 (2017, updated 2020) | https://www.nice.org.uk/guidance/ng69/chapter/Recommendations | VERIFIED | 官方臨床指引；不能直接轉成 DietSense 自動診斷或風險分類演算法。 | domain §E |
| RW-E20 | 英語食譜/歐洲食品資源的研究結果可直接證明台灣繁體中文混合餐系統不存在或普遍不可用。 | 本次有限範圍搜尋無法支持 | 無 | UNVERIFIED | 語言、ontology、餐點類型和使用場景均不同；目前沒有完成繁中資料庫系統性搜尋。 | 已明確排除；research gap 限定為待測問題 |
| RW-E21 | DietSense 將以繁體中文解析、結構化檢索、確定性計算、來源追溯和有限澄清作為設計方案。 | DietSense proposal、DESIGN.md、Stage 3 docs | 專題內部文件，非外部 DOI | VERIFIED（僅作提案/設計描述） | 設計文件明列八模組、資料合約和 evaluation plan；不證明已實作或有效。 | all refactored documents |
| RW-E22 | DietSense 會降低記錄時間、提升準確度/依從性或確保安全。 | 尚未實驗 | 無 | UNVERIFIED | Stage 3 僅提出可評估的 future study；尚無實測或專業安全驗證。 | 不作結果主張；改列研究問題 |
| RW-E23 | 「全球第一」或「沒有任何系統整合 LLM/RAG/營養資料庫」。 | 本次搜尋；DietAI24 2025 已公開同類影像整合 | https://doi.org/10.1038/s43856-025-01159-0 | CONTRADICTED（寬泛的「LLM+RAG+food DB 從未整合」說法） | DietAI24 直接反例；但仍未作全面全領域檢索。 | 將新穎性限縮到任務情境和測試比較，不作 priority claim。 |

## Claim/source interpretive limits

1. 搜尋查核日期為 2026-11-12；索引、網頁和指南版本會更新，正式論文提交前需更新確認。
2. FoodBase/FoodNER/food linking 語料以英語食譜/特定 ontology 為主，不代表台灣口語食物知識。
3. RAG、Agent 和食品 NER 證據只支持其原始 NLP/資料任務；不支持 DietSense accuracy、安全性或減少使用者負擔的因果結論。
4. 可追溯來源與確定性運算提高可檢查性和重算性，不保證輸入份量/食品匹配與參照值為真。
5. 任何 DietSense 效益仍需按 `docs/design/evaluation-plan.md` 完成資料集、比較條件、倫理流程和預先註冊後驗證。

## 2026 年新增來源與收窄後主張

| ID | 精確主張 | 來源 / 作者 / 年 | DOI 或官方 URL | 狀態 | 證據與主要限制 | 使用位置 |
|---|---|---|---|---|---|---|
| RW-E24 | FoodMapper 研究以 ASA24-to-FooDB 及 NHANES-to-DFG2 資料比較 fuzzy matching、TF-IDF、embedding、LLM 與 hybrid mapping；hybrid 在兩個特定基準的 accuracy 分別為 90.7% 與 65.4%。 | Lemay et al., The Journal of Nutrition, 2026 | https://doi.org/10.1016/j.tjnut.2026.101678 | VERIFIED | PubMed/USDA ARS 正式紀錄支持研究設計與結果；NHANES 對應集僅 256 筆且 no-match 比例高。數值只適用原始映射基準。 | AI §A/綜合；academic §§1、5；table RW16 |
| RW-E25 | NutriRAG 使用飲食文字記錄檢索示例並以 GPT-4 分類，研究報告 micro-F1 82.24%。 | Zhou et al., JAMIA, 2026 | https://doi.org/10.1093/jamia/ocag003 | VERIFIED | PubMed 正式期刊紀錄支持；樣本為 77 位成人肥胖者既有試驗日誌，分類標籤結果不等同營養素估值或台灣菜 matching。 | AI §A；academic §1；table RW17 |
| RW-E26 | FoodyLLM 研究以約 225,000 組對齊 QA 訓練食品營養領域模型，評估食譜營養、標示分類和 entity linking 任務。 | Gjorgjevikj et al., Current Research in Food Science, 2026 | https://doi.org/10.1016/j.crfs.2026.101351 | VERIFIED | 正式期刊/PubMed 摘要支持模型和任務範圍；結果僅適用原文 benchmark，不能推論 DietSense 或每一任務均優於通用模型。 | AI §B/綜合；academic §1；table RW18 |
| RW-E27 | 文字查詢的 LLM 營養估值研究測試 194 種美國常見食品及四個模型，發現總體能量/巨量營養素一致度較佳，但微量營養素、混合菜及調味品變異較大。 | Lawabni et al., The Journal of Nutrition, 2026 | https://doi.org/10.1016/j.tjnut.2026.101712 | VERIFIED | PubMed/出版資料支持樣本及研究結論；NCC 比較、食品選取及個別 limits of agreement 限制外推，不能寫成可靠度保證。 | domain §C；academic §1；table RW19 |
| RW-E28 | 中國食物成分表比較研究測試 299 種中國食品、九個 LLM 並重複執行三次，報告不同營養項目和食品的估值差異。 | Cao et al., Frontiers in Nutrition, 2026 | https://doi.org/10.3389/fnut.2026.1952757 | VERIFIED | 正式期刊全文支持食品數、模型數及比較設計；中國標準食品名不能代表台灣複合餐或對話流程。該研究直接反駁「中文食品文字估值尚無研究」的寬泛說法。 | AI §A；domain §C；academic §1/5；table RW20 |
| RW-E29 | Diabot-GPT-4o 研究在台灣以 57 名年輕成人、714 張影像及三日秤重飲食紀錄驗證影像飲食評估。 | Chen et al., The American Journal of Clinical Nutrition, 2025 | https://doi.org/10.1016/j.ajcnut.2025.10.013 | VERIFIED | PubMed 正式出版摘要支持研究樣本和影像任務；並非文字飲食對話系統，樣本不代表一般台灣人口。寬泛的「台灣沒有 AI 飲食評估」主張已被此先例反駁。 | domain §D；academic §1/5；table RW21 |
| RW-E30 | 「文字映射、中文食品 LLM 估值、台灣 AI 飲食評估皆不存在」可作為 DietSense 新穎性主張。 | RW16–RW21 近期研究 | https://doi.org/10.1016/j.tjnut.2026.101678 ; https://doi.org/10.3389/fnut.2026.1952757 ; https://doi.org/10.1016/j.ajcnut.2025.10.013 | CONTRADICTED | RW16–RW20 證明文字映射/估值和中文食品研究已存在；RW21 是台灣影像評估先例。這些論文仍未直接驗證 DietSense 完整文字對話、台灣混合菜逐項來源追溯、澄清策略及指定 manual baseline。 | novelty 修正；related-work-academic §5 |
| RW-E31 | DietSense 的窄化研究機會是比較台灣繁體中文混合菜多輪文字記錄、澄清、逐值來源追溯與確定性計算的完整工作流程，並和固定手動搜尋輸入條件比較。 | Stage 3 evaluation plan + 本次相關文獻範圍 | 內部研究計畫；非外部效能證據 | PARTIALLY VERIFIED | 這是根據現有研究差異提出的可測研究問題；非全面系統性搜尋結果，不能稱全領域未解或全球首創。 | AI synthesis；academic §5；stage5-validation |
