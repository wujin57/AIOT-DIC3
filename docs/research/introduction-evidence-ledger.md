# Introduction Evidence Ledger

## Scope and status policy

本帳本追蹤 [introduction-af.md](../refactored/introduction-af.md) 與 [introduction-academic.md](../refactored/introduction-academic.md) 的主要外部事實主張及提案內部規劃。VERIFIED 只代表來源直接支持所列的有限主張，不代表來源支持更廣泛的推論。PARTIALLY VERIFIED 表示部分內容有來源支持，但外推、涵蓋或研究設計尚未驗證。UNVERIFIED 表示目前沒有足夠證據支持，該主張不應作為既定事實。此帳本不是系統性文獻回顧。

## Claim-level records

| ID | 精確主張（邊界化） | 來源／作者／日期 | DOI 或官方網址 | 狀態 | 支持證據 | 限制 | 使用位置 |
|---|---|---|---|---|---|---|---|
| I-01 | WHO 報告，2024 年全球約 26 億名成人過重，其中約 9.4 億名成人患有肥胖。 | World Health Organization，fact sheet 更新 2026-10-07；數據年 2024 | https://www.who.int/news-room/fact-sheets/detail/obesity-and-overweight | VERIFIED | WHO fact sheet 直接列出 2024 成人過重與肥胖估計。 | 全球統計不能說明台灣特定族群、飲食記錄工具效益或因果。 | A；Academic §1 |
| I-02 | 台灣國民健康署指出，2020–2024 年國民營養健康調查中，18 歲以上成人有 51.3% 達該署過重或肥胖標準。 | Taiwan Health Promotion Administration，2026-03-04 | https://www.hpa.gov.tw/5020/19885/n | VERIFIED | 官方頁面直接報告 51.3% 及調查期間。 | 依國民健康署定義與調查；不可與其他國家、年份或定義不一致的比率直接比較。 | A；Academic §1 |
| I-03 | 一項 59 項研究的回顧探討行為性減重介入中的飲食自我監測；依從性測量不一致，使用程度與結果關係未充分檢驗。 | M. Raber et al., *Public Health Nutrition*, 2021 | doi:10.1017/S136898002100358X; https://pubmed.ncbi.nlm.nih.gov/34412727/ | VERIFIED | 系統性回顧包含 59 項研究並討論監測強度、傳遞及成效。 | 研究介入、族群與依從性定義異質；不證明 DietSense 效益。 | A；Academic §1 |
| I-04 | 份量估算工具在設計、研究族群與驗證方式上多樣，適用性應依工具和情境判讀。 | B. Amoutzopoulos et al., *Nutrition Reviews*, 2020 | doi:10.1093/nutrit/nuz107; https://pubmed.ncbi.nlm.nih.gov/31999347/ | VERIFIED | 系統性回顧整理飲食評估中的份量工具及其優缺點。 | 不可推論所有工具都不準確，也沒有證明 DietSense 的份量估算效能。 | B、D；Academic §§2–3 |
| I-05 | 一項影像飲食評估方法回顧與統合分析納入 13 項研究、606 位參與者，合併能量估值相對參照方法呈低報，且研究間異質性高。 | D. K. N. Ho et al., *Clinical Nutrition*, 2020 | doi:10.1016/j.clnu.2020.08.002; https://pubmed.ncbi.nlm.nih.gov/32839035/ | VERIFIED | 回顧摘要報告研究數、參與者數、合併差異與高異質性。 | 此為研究集合的合併觀察，不能套用為每一影像方法、菜系或部署產品的固定誤差。 | D；Academic §2 |
| I-06 | USDA FoodData Central 提供 Food Search 與 Food Details API。 | USDA Agricultural Research Service，官方 API Guide（網頁版本日期未列） | https://fdc.nal.usda.gov/api-guide/ | VERIFIED | 官方文件說明搜尋與詳細資料端點。 | API 可用不等於資料符合台灣料理；API key、授權與版本仍須於實作前核對。 | B、D；Academic §2 |
| I-07 | 台灣 TFDA 維護台灣地區食品營養成分資料庫。 | Taiwan Food and Drug Administration，官方資料庫頁（網頁版本日期未列） | https://www.fda.gov.tw/tc/site.aspx?r=1647620244&sid=271 | VERIFIED | 官方頁面提供該資料庫入口。 | 資料庫存在不證明涵蓋所有台灣菜、店家配方或所有營養欄位；逐筆涵蓋率未盤點。 | B、D；Academic §2 |
| I-08 | RAG 原始研究在知識密集型 NLP 任務評估檢索與生成的結合。 | P. Lewis et al., NeurIPS 2020 | https://arxiv.org/abs/2005.11401; https://papers.nips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html | VERIFIED | 原始論文描述並評估知識密集型自然語言任務。 | 不支持其在營養資料、台灣食物匹配或 DietSense 的準確率，也不證明 RAG 可消除幻覺。 | B、D；Academic §2 |
| I-09 | Zeevi 等人研究特定研究參與者的餐後血糖反應個人化預測。 | D. Zeevi et al., *Cell*, 2015 | doi:10.1016/j.cell.2015.11.001; https://pubmed.ncbi.nlm.nih.gov/26590418/ | VERIFIED | 論文研究個人餐後血糖反應預測。 | 研究結果不等同一般熱量目標或臨床處方；不可直接外推至 DietSense。 | B、D；Academic §2 |
| I-10 | DIETFITS 隨機試驗納入 609 名成人；該試驗未發現其指定的基因型或基線胰島素分泌可預測低脂與低碳飲食 12 個月減重差異。 | C. D. Gardner et al., *JAMA*, 2018 | doi:10.1001/jama.2018.0245; https://pubmed.ncbi.nlm.nih.gov/29466592/ | VERIFIED | 試驗摘要報告樣本數、比較條件及交互作用分析結果。 | 限定於該試驗人群、介入和預先測試的交互作用，不否定所有個人化營養研究。 | B、D；Academic §2 |
| I-11 | 飲食記錄工具在資料來源、介面、份量輸入和功能上有差異；本稿不將單一限制推廣到全部產品。 | 本研究的範圍界定；個別產品需逐一查證 | 無單一來源 | PARTIALLY VERIFIED | 原 proposal 與相關工具文獻提供不同記錄方式的線索。 | 未完成指定商用產品的系統性產品比較；文字採條件式敘述，不把推測列為產品普遍事實。 | B、D；Academic §§2–3 |
| I-12 | 配方、烹調、食物狀態、份量與剩食可能影響餐點可對應的營養紀錄。 | 份量估算回顧 [4]、影像評估回顧 [5]；研究任務定義 | 同 I-04、I-05 | PARTIALLY VERIFIED | 份量估算與影像評估文獻顯示估量方法及參照存在限制；技術上亦需使食物/份量和營養基準對齊。 | 每項因素對特定台灣菜的影響幅度尚未測量；不得誤稱已完成在地菜色調查。 | B、C、D；Academic §§2–3 |
| I-13 | DietSense 擬以 LLM 解析意圖、檢索結構化營養資料、確定性計算、有限澄清、來源追溯及安全降級。 | 本提案原始 DOCX、Stage 3 `docs/design/architecture.md` 與 `algorithms.md` | 專題內部來源；無 DOI | VERIFIED（作為提案內容） | 以上文件明列八模組與對應資料流/演算法。 | 「提案已提出」不代表系統已實作或驗證有效。 | E；Academic §4 |
| I-14 | 計畫預計建立 500 筆資料、採固定手動搜尋輸入 baseline，並規劃 20 名成人、7 日可行性研究。 | Stage 3 `docs/design/evaluation-plan.md`；原始 proposal / presentation | 專題內部規劃；無 DOI | VERIFIED（作為計畫內容） | Stage 3 評估計畫明確將樣本與研究設計標為未來提案，尚須 protocol 定稿。 | 不是已收案或已得出的樣本；無代表性或統計 power 保證。 | F；Academic §4 |
| I-15 | DietSense 是「全球第一」或「首次」把 LLM、RAG、台灣營養資料庫與餐點追蹤整合的系統。 | 原 proposal 的新穎性表述；尚無系統性搜尋支持 | 無已驗證來源 | UNVERIFIED | 未找到足以支持全球首次的完整、可重現搜尋策略。 | 需要系統性資料庫/產品檢索及納入標準；重構稿已刪除此表述，改為可評估的設計主張。 | 原稿移除；E 的風險說明 |
| I-16 | 台灣所有混合料理均缺少營養資料、現有產品普遍無法處理台灣食物，或指定 app 一律有約 30% 誤差。 | 原 proposal 廣泛概括；無可核對的限定來源 | 無已驗證來源 | UNVERIFIED | 目前來源只證明資料庫/估算工具存在及某些研究限制，未支持全體產品或菜色的概括。 | 應做版本化候選覆蓋與產品任務基準；重構稿改為待測問題。 | 原稿移除；C、D 的範圍限制 |
| I-17 | 使用 DietSense 將使日誌時間縮短 60%、達到 >85% 落在 ±20% 誤差帶或 SUS >70。 | 原 proposal/PPT 候選目標 | 無實測資料 | UNVERIFIED（結果主張） | 這些數字僅出現在原提案候選目標，無實驗資料支持。 | Stage 3 已將其標示為待 pilot 與預註冊決定的門檻；不得寫成結果或保證。 | F；Academic §4 |
| I-18 | 營養估值應能由來源紀錄、份量與固定公式重算；未校準範圍不可稱為信賴區間。 | DietSense 提案設計要求；評估方法學 | 專題內部規格 | VERIFIED（作為設計要求） | Stage 3 資料合約、確定性算法及 evaluation plan 要求保留來源/版本、定義公式及區分 range coverage。 | 這是可追溯性與報告規範，不證明估值相對真值準確。 | E、F；Academic §§3–4 |
| I-19 | 原稿曾列 WHO 43%、台灣代謝症候群逾 25%、NT$3000 億成本、生產力損失、應用市場 US$6.8B/17.4% 成長、手動記錄 3.3 kg 效果、85% 30 日流失及 MyFitnessPal 約 30% 誤差等背景或限制主張。 | Original DOCX `期中Proposal_熱量AI_Agent.docx`，Introduction/Abstract；具體頁碼依原始版面 | 原文引用/資料口徑未能逐項確認 | UNVERIFIED（重構稿採用前） | 這些數字存在於原始提案，但目前無可完整核對、口徑一致且直接支持的來源鏈。 | 不等於證明其錯誤；因缺乏可追溯來源、年份/分母/定義或適用情境，重構稿未採用。 | 僅 change log 記錄移除 |
| I-20 | 對話介面會降低使用者負擔或提升資料完整性。 | DietSense 研究假設 | 待 Stage 3 protocol 與研究資料 | UNVERIFIED（尚待實驗） | 評估計畫設定記錄時間、完成率、澄清輪數等可檢驗結果。 | 不能由系統設計或相關技術存在推導出效益；需使用者研究。 | C、F；Academic §§3–4 |
| I-21 | 安全限制可避免飲食失調傷害、臨床風險或不當建議。 | 提案設計要求 | 尚待專業審查與安全評估 | UNVERIFIED（成效主張） | Stage 3 設計包含 SafetyDecision、限制/拒答及專業審查需求。 | 尚無安全案例測試、專業簽核或臨床驗證；緒論只表述為規劃的控制與評估。 | E、F；Academic §4 |

## Sources and reference metadata

| Ref. | 作者／機構、日期 | 完整題名與出版資訊 | DOI / URL |
|---|---|---|---|
| [1] | World Health Organization, updated 2026-10-07 | “Obesity and overweight,” fact sheet. | https://www.who.int/news-room/fact-sheets/detail/obesity-and-overweight |
| [2] | Taiwan Health Promotion Administration, 2026-03-04 | 〈響應世界肥胖日　兩招啟動健康管理〉. | https://www.hpa.gov.tw/5020/19885/n |
| [3] | M. Raber et al., 2021 | “A systematic review of the use of dietary self-monitoring in behavioural weight loss interventions: delivery, intensity and effectiveness,” *Public Health Nutrition*, 24(17), 5885–5913. | https://doi.org/10.1017/S136898002100358X ; https://pubmed.ncbi.nlm.nih.gov/34412727/ |
| [4] | B. Amoutzopoulos et al., 2020 | “Portion size estimation in dietary assessment: a systematic review of existing tools, their strengths and limitations,” *Nutrition Reviews*, 78(11), 885–900. | https://doi.org/10.1093/nutrit/nuz107 ; https://pubmed.ncbi.nlm.nih.gov/31999347/ |
| [5] | D. K. N. Ho et al., 2020 | “Validity of image-based dietary assessment methods: A systematic review and meta-analysis,” *Clinical Nutrition*, 39(10), 2945–2959. | https://doi.org/10.1016/j.clnu.2020.08.002 ; https://pubmed.ncbi.nlm.nih.gov/32839035/ |
| [6] | USDA Agricultural Research Service, web documentation, date not stated | “FoodData Central API Guide.” | https://fdc.nal.usda.gov/api-guide/ |
| [7] | Taiwan Food and Drug Administration, web database page, date not stated | “台灣地區食品營養成分資料庫.” | https://www.fda.gov.tw/tc/site.aspx?r=1647620244&sid=271 |
| [8] | P. Lewis et al., 2020 | “Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks,” *Advances in Neural Information Processing Systems*, 33, 9459–9474. | https://doi.org/10.48550/arXiv.2005.11401 ; https://arxiv.org/abs/2005.11401 |
| [9] | D. Zeevi et al., 2015 | “Personalized Nutrition by Prediction of Glycemic Responses,” *Cell*, 163(5), 1079–1094. | https://doi.org/10.1016/j.cell.2015.11.001 ; https://pubmed.ncbi.nlm.nih.gov/26590418/ |
| [10] | C. D. Gardner et al., 2018 | “Effect of Low-Fat vs Low-Carbohydrate Diet on 12-Month Weight Loss in Overweight Adults and the Association With Genotype Pattern or Insulin Secretion: The DIETFITS Randomized Clinical Trial,” *JAMA*, 319(7), 667–679. | https://doi.org/10.1001/jama.2018.0245 ; https://pubmed.ncbi.nlm.nih.gov/29466592/ |

## Source-document and extraction notes

五份 instructor-provided references 已於 Stage 0 擷取；原 Proposal DOCX 為主要專題來源，presentation 用於核對簡報中的設計與候選目標，assignment requirements 與 A2Z 範例作為結構要求。此階段未重新修改或轉換任何原始檔案。來源解析結果可協助文本查核，但本帳本只將外部官方/論文來源用於事實性公共主張；專題內部文件只證明「原提案/規格寫了什麼」，不能證明設計成效。
