# Stage 4 — Introduction Refactor Validation

## 結果摘要

**Stage 4 文件要求：PASS。** 本階段完成五份指定文件並檢查引用一致性、A–F/A2Z 對應、proposal tense、階段範圍與跨階段相容性。文獻缺口尚未經系統性回顧、台灣食物資料覆蓋尚未盤點、設計與安全成效尚未測試，均屬已明確標示的後續研究限制；Stage 4 要求的是在證據不足時限定主張並揭露限制，故不因此將文件交付判為未完成。

## 交付文件

| 路徑 | 用途 | 狀態 |
|---|---|---|
| `docs/refactored/introduction-af.md` | 詳細 A–F 重構與 A2Z G–L 對照 | 完成 |
| `docs/refactored/introduction-academic.md` | 連貫學術章節版緒論及參考資料 | 完成 |
| `docs/research/introduction-evidence-ledger.md` | claim-level 證據、狀態、來源及限制 | 完成 |
| `docs/reviews/introduction-change-log.md` | 原稿與重構差異及移除主張紀錄 | 完成 |
| `docs/reviews/stage4-validation.md` | 本驗證報告 | 完成 |

## A–F 及 A2Z 覆蓋檢查

| 要求 | 驗證結果 | 證據／備註 |
|---|---|---|
| A Attention Getter | PASS | 引入有來源的全球及台灣統計，並限制推論。 |
| B Background | PASS | 說明飲食監測、資料庫、份量工具、影像、LLM/RAG 與個人化證據。 |
| C Problem | PASS | 提出繁體中文混合餐描述下可測的研究問題，不把研究缺口說成已證明的全領域缺失。 |
| D Existing Limitations | PASS | 按方法類別說明限制與適用條件，並標示證據邊界。 |
| E Innovation | PASS | 保留八模組設計，說明澄清、資料來源、確定性計算及範圍/安全要求；無 first-ever 主張。 |
| F Contributions | PASS | 四項預期貢獻連結到問題、系統元件和擬議評估；成果均以未來式描述。 |
| A2Z G–L | PASS | 詳細版明列 G General、H However、I In Literature、J Judgement、K Keypoint、L List Organization 的對照。 |

## 證據驗證與引用一致性

- 兩個 Introduction 引用均為 [1]–[10]，編號與各自參考資料清單一一對應；evidence ledger 對照相同編號，並另列主張 ID、發布資訊、狀態和限制。
- WHO 與台灣 HPA 統計採官方頁面數字；飲食監測、份量估算、影像評估及 RAG 主張均限制於文獻研究所支持的範圍。FoodData Central 和 TFDA 只被描述為可用資料庫/API，不推導其涵蓋所有台灣菜。
- 個人化營養研究只用來界定外推限制；沒有把餐後血糖結果說成一般熱量處方。
- 內部文件只用來確認「專題計畫或設計內容」，沒有被當作實驗效能的外部證據。
- 原 proposal 中缺少可追溯來源的統計、產品錯誤率、留存率、成本/市場數字及 first-ever 宣稱均未在重構正文當成事實。其「UNVERIFIED」意為本次查核不足以採用，不等同證明數值為假。

## 跨文件一致性與實驗語氣

| 項目 | 結果 | 檢查內容 |
|---|---|---|
| Abstract 一致性 | PASS | 公衛統計、研究問題、RAG 限制、確定性計算與未來研究語氣和 Stage 1 Abstract 相符。 |
| Stage 2 深度研究 | PASS | 將不確定份量、資料覆蓋、可追溯性及安全風險表述為待查核/測試問題，未把爭議立場寫成已定論。 |
| Stage 3 設計 | PASS | 沿用八模組架構、有限澄清、source/version provenance、確定性 Analytics、一般資訊範圍和 fallback。 |
| Evaluation plan | PASS | 500 筆、固定手動搜尋輸入 baseline、20 位成人 × 7 日均稱為規劃；候選門檻未稱為結果。 |
| 實驗/結果語氣 | PASS | 沒有聲稱已招募、收集資料、取得準確率、縮時、SUS 或臨床效果。 |
| 統計與估算範圍 | PASS | 未校準 plausible range 不稱為信賴區間；人口統計不作成效因果證據。 |

## 尚待處理事項

1. **文獻缺口：** Stage 4 的來源查核不是系統性回顧；正式定稿前仍需制定資料庫、搜尋式、納入排除標準及更新日期，確認台灣語言/混合菜任務的既有系統與相關基準。
2. **資料覆蓋：** 尚未逐筆盤點 TFDA、USDA、食譜或商用資料源對目標菜色、版本、營養欄位及授權條款的覆蓋。
3. **參照值與 protocol：** 500 筆資料集的抽樣比例、標註流程、參照品質、baseline 版本、主要 outcome 及分析計畫仍需 pilot 後預註冊。
4. **安全與倫理：** 安全測試內容、專業審核、IRB/校方程序、資料保留與第三方模型條款尚未核准或驗證；因此不能宣稱臨床安全。
5. **學術格式：** 參考資料目前具 DOI/官方網址，但投稿或繳交前應依課程要求統一 IEEE 標點、斜體及引用樣式，並確認網頁存取日期政策。

## 階段範圍檢查

本階段只新增上述 Stage 4 五份文件。未修改原始 DOCX/PPTX/PDF、Stage 1–3 文件或 Related Work；未使用或初始化 OpenSpec；未安裝套件；未實作應用；未建立 Git commit 或 push。故文件範圍檢查 **PASS**。

## Mandatory self-validation

完成一輪自我驗證：五份文件均存在且非空；兩種緒論版本均包含全部 [1]–[10] 引用編號；本地 Markdown 連結均解析至存在的檔案；A–F、G–L、claim statuses 及交付章節均存在；未發現重複長段落或過時的「缺少 Stage 1 文件」敘述。引用對照與跨階段資料點以人工複核；沒有發現需在 Stage 4 範圍內進行的修正，因此不需要第二、第三輪。原始文件與前階段檔案由本階段只讀取、未寫入；工作目錄不是 Git repository，故沒有以 Git diff 驗證未修改狀態。

## 最終判定

**PASS — Stage 4 所有文件交付及規定的驗證均完成。** field-wide 新穎性、資料覆蓋、正式研究 protocol 與安全/倫理審查仍屬後續研究限制，不是本階段未完成的文件項目。本報告結束於 Stage 4，不代表開始 Stage 5。
