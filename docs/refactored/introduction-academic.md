# DietSense 研究計畫緒論

## 1. 研究背景與動機

飲食監測是營養研究與部分行為體重管理介入採用的資料蒐集方式，但記錄本身並不等同於健康成效。世界衛生組織（WHO）估計，2024 年全球約有 26 億名成人過重，其中約 9.4 億名成人患有肥胖；台灣國民健康署依 2020–2024 年國民營養健康調查指出，18 歲以上成人中有 51.3% 達到該署的過重或肥胖標準 [1], [2]。這些資料提供本研究的公共衛生背景，不能單獨證明某項飲食記錄工具可預防或治療疾病。

飲食自我監測曾被納入成人過重或肥胖者的行為介入。一項涵蓋 59 項研究的系統性回顧指出，不同強度的飲食監測可能支持減重介入，但依從性指標不一致，且監測使用程度與結果之間的關係仍未充分分析 [3]。因此，本研究關注的問題不僅是能否產生熱量數字，也包括輸入流程是否可操作、估算依據能否追溯，以及資訊不足時能否清楚呈現不確定性。

## 2. 飲食記錄與 AI 技術背景

資料庫式飲食記錄通常要求使用者查找食物候選、選擇合適項目並輸入份量；實際流程會依產品、資料來源及介面而異。對複合餐點而言，名稱、配方、烹調方式、可食份量及剩食等資訊可能影響營養估算。份量估算工具的系統性回顧顯示，工具設計與驗證方式多樣，必須依個別工具及目標族群判讀其適用性 [4]。影像式飲食評估可提供外觀線索，但照片未必呈現被遮蔽的食材、油醬用量、食物深度或剩食。Ho 等人的系統性回顧與統合分析納入 13 項研究、606 位參與者，合併結果呈現能量攝取低報，研究間異質性高；此結果描述的是納入研究整體，不能套用為每個影像系統的固定誤差 [5]。

食品成分資料庫可支援營養資料檢索。USDA FoodData Central 提供 Food Search 與 Food Details API [6]；台灣食品藥物管理署亦維護台灣地區食品營養成分資料庫 [7]。資料庫的存在不代表每道店家料理、品牌品項或家庭食譜都能找到完全相符的紀錄。來源版本、食物狀態、份量基準及配方差異都可能限制候選資料的適用性。

大型語言模型（LLM）可用於解析自然語言餐點描述、辨識意圖及協調工具流程；檢索增強生成（RAG）則將外部來源檢索整合到生成流程。RAG 的原始研究在知識密集型自然語言任務上評估此架構 [8]，但並未驗證營養估算，也不表示檢索能自動排除錯誤來源。DietSense 因此規劃由 LLM 負責語言理解與流程協調，營養數值則由具來源依據的結構化紀錄提供，並由確定性分析模組依已確認的份量與營養密度計算。系統應保留來源、版本及計算假設，以便檢視和重算。

個人化營養研究的族群、結果指標與外推範圍亦須區分。Zeevi 等人研究特定族群的餐後血糖反應預測 [9]，並非一般熱量追蹤的個人處方證據。DIETFITS 隨機試驗納入 609 名成人，未發現其所測試的基因型或基線胰島素分泌能預測低脂與低碳飲食的 12 個月減重差異 [10]。本專題因此將第一階段範圍限定於飲食記錄、營養估算與一般資訊，不推論個人疾病、代謝因果或治療需求。

## 3. 問題界定與研究缺口

本研究聚焦於繁體中文台灣餐點描述中的食物匹配、份量表達及營養估算。例如，「吃了一碗加蛋的台式牛肉麵，湯喝一半」沒有明確重量或完整配方；若資料來源只有名稱相似、但食物狀態或份量基準不同的項目，系統不能只憑名稱輸出看似精確的數值。便當、夜市小吃、湯麵及家庭料理可用於檢驗這些互動與資料問題，但本研究尚未完成代表性資料盤點，不能宣稱所有台灣混合料理皆缺乏資料。

現有證據各自涵蓋飲食自我監測、份量工具、影像評估、結構化營養資料檢索及個人化營養等面向；本次資料查核並非系統性文獻回顧，也不足以證明特定功能在整個研究領域中缺席。據此，本計畫採取範圍明確且可驗證的研究問題：**對於繁體中文台灣混合料理描述，結合結構化營養資料檢索、針對性澄清、確定性計算與來源追溯的對話式系統，能否產生可檢視的估算？在預先定義的測試任務中，其估算誤差、來源追溯、記錄時間及任務完成表現為何，並如何與固定版本的手動搜尋與輸入流程比較？**

研究將分別衡量食物匹配、熱量與巨量營養素誤差、資料來源覆蓋、來源追溯率、澄清輪數、任務時間及完成情形。對話互動是否降低記錄負擔、估算是否適合日常追蹤，以及資料來源能涵蓋多少常見餐點，都屬待測問題而非既定結論。系統亦須具備無有效候選、份量資訊不足、來源衝突及安全限制等降級路徑。

## 4. 擬議方法與預期貢獻

DietSense 規劃為繁體中文領域 AI Agent，並延續原提案的八模組架構。流程將以對話理解抽取餐點欄位並保留原始描述；檢索模組查詢已登錄的營養資料來源，保存 source ID、版本及食物狀態；若食物身份或關鍵份量資訊不足，澄清模組提出有限次追問或採用明確的 fallback；Analytics Engine 僅在資料與單位通過檢查後，依確定性公式計算營養值；Domain Knowledge 與安全決策模組限定回應範圍，避免把記錄結果包裝成診斷或治療建議。只有在來源能支持上下界時，系統才可呈現合理估算範圍；未校準的範圍不得稱為統計信賴區間。安全政策和特殊情境文案仍須由營養及相關專業人員審查。

本計畫預期形成四項可評估成果：第一，建立預計 500 筆台灣餐點描述及參照標籤的資料集與標註流程，並揭露抽樣框和可評估比例，不主張其代表全台飲食；第二，提出可追溯的檢索—計算流程，以識別表現、營養誤差、來源追溯及重算一致性評估；第三，設計針對食物身份與份量缺漏的澄清及不確定性呈現機制，以澄清負擔、任務完成及估算範圍品質評估；第四，建立一般資訊與安全邊界的測試框架，並規劃 20 位成人、7 日的可行性使用研究。資料集規模、使用者人數及研究天數均為尚待 protocol、倫理審查及可行性確認的計畫條件，並非已完成工作或效能結果。

## 5. 研究計畫組織

後續研究計畫將先整理相關工作與營養領域證據，再說明 DietSense 的需求、八模組架構、資料合約、澄清及安全流程，接著提出資料集建立、比較基線、評估指標與使用者研究程序，最後討論倫理、隱私、研究限制及預期貢獻。各研究程序與候選門檻需在資料收集或招募開始前定稿；本緒論不報告任何尚未執行的實驗結果。

## 參考資料

[1] World Health Organization, “Obesity and overweight,” fact sheet, updated 2026-10-07. https://www.who.int/news-room/fact-sheets/detail/obesity-and-overweight.

[2] Taiwan Health Promotion Administration, 〈響應世界肥胖日　兩招啟動健康管理〉, 2026-03-04. https://www.hpa.gov.tw/5020/19885/n.

[3] M. Raber et al., “A systematic review of the use of dietary self-monitoring in behavioural weight loss interventions: delivery, intensity and effectiveness,” *Public Health Nutrition*, vol. 24, no. 17, pp. 5885–5913, 2021, doi:10.1017/S136898002100358X.

[4] B. Amoutzopoulos et al., “Portion size estimation in dietary assessment: a systematic review of existing tools, their strengths and limitations,” *Nutrition Reviews*, vol. 78, no. 11, pp. 885–900, 2020, doi:10.1093/nutrit/nuz107.

[5] D. K. N. Ho et al., “Validity of image-based dietary assessment methods: A systematic review and meta-analysis,” *Clinical Nutrition*, vol. 39, no. 10, pp. 2945–2959, 2020, doi:10.1016/j.clnu.2020.08.002.

[6] USDA Agricultural Research Service, “FoodData Central API Guide.” https://fdc.nal.usda.gov/api-guide/.

[7] Taiwan Food and Drug Administration, “台灣地區食品營養成分資料庫.” https://www.fda.gov.tw/tc/site.aspx?r=1647620244&sid=271.

[8] P. Lewis et al., “Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks,” *Advances in Neural Information Processing Systems*, vol. 33, pp. 9459–9474, 2020. https://arxiv.org/abs/2005.11401.

[9] D. Zeevi et al., “Personalized Nutrition by Prediction of Glycemic Responses,” *Cell*, vol. 163, no. 5, pp. 1079–1094, 2015, doi:10.1016/j.cell.2015.11.001.

[10] C. D. Gardner et al., “Effect of Low-Fat vs Low-Carbohydrate Diet on 12-Month Weight Loss in Overweight Adults and the Association With Genotype Pattern or Insulin Secretion: The DIETFITS Randomized Clinical Trial,” *JAMA*, vol. 319, no. 7, pp. 667–679, 2018, doi:10.1001/jama.2018.0245.
