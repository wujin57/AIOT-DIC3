# Stage 6 需求與結構符合矩陣

狀態定義：**PASS** 表示本整合文件已具體覆蓋；**PARTIAL** 表示內容/驗證或提交產物仍有明確缺口；**NOT APPLICABLE** 表示為後續實作或期末交接而非本提案階段。矩陣只按教師提供的作業規範及 A2Z 範例判讀，不增加未明示要求。

| 來源要求 / 原提案位置 | 教師要求或 A2Z 對應 | 最終提案位置 | Supporting evidence | 狀態 / 說明 |
|---|---|---|---|---|
| 原提案 Abstract A–F | 作業規範：摘要 A–F；A2Z A–F | §2 摘要，含問題、方案、方法、規劃評估及預期貢獻 | `docs/refactored/abstract-zh.md`; `abstract-evidence-ledger.md` | PASS；全程以計畫語氣，不報結果 |
| 原提案 Introduction A–F | 作業規範緒論；A2Z G–L | §3.1–3.4 | `introduction-af.md`; `introduction-academic.md`; `introduction-evidence-ledger.md` | PASS；A2Z G–L 不是原 proposal A–F 的替代標籤，已並列映射 |
| 背景、動機與問題 | A2Z G–I | §3.1–3.3 | WHO/HPA/Raber 引文；Stage 4 ledger | PASS；公共統計不作系統效能證據 |
| 既有研究限制及研究缺口 | A2Z I–J、Related Work O | §3.3、§4.4 | Stage 5 verified literature; search log | PASS；採範圍性、非「首次」主張 |
| 研究目標、創新與貢獻 | A2Z K–L | §3.4、§8 | Stage 4/5 validated files | PASS；貢獻定位為待測工作流程 |
| Related Work AI Technology | 作業規範要求 AI 技術面 | §4.1 | `related-work-ai.md`; article table RW01–RW08, RW16–RW18 | PASS；涵蓋 RAG/Agent、NER/NEL、影像及文字 LLM |
| Related Work Nutrition Domain Knowledge | 作業規範要求營養領域面 | §4.2 | `related-work-domain.md`; refs [3]–[7], [24]–[28] | PASS；指出來源/族群/測量限制 |
| Article Summary Table | 作業規範；A2Z M | §4.3 表（20 項同儕審查研究） | `docs/research/article-summary-table.md` | PASS；詳細表另有支援檔，整合表保留限制及關聯 |
| Related Work 綜合、gap、方向 | A2Z N–O | §4.4 | `related-work-academic.md`; `related-work-evidence-ledger.md` | PASS；含 SWOT，未把範圍搜尋稱為系統回顧 |
| Five Core Mindsets | 作業規範 Deep Research | §5.1 | `docs/research/five-core-mindsets.md` | PASS；每項保留證據限制、設計含意和測試情境 |
| Three Professional Controversies | 作業規範 Deep Research | §5.2 | `docs/research/three-professional-controversies.md` | PASS；呈現兩側取捨與未決證據 |
| Ten Deep Understanding Questions | 作業規範 Deep Research；A2Z 問題設計 | §5.3 | `docs/research/ten-deep-questions.md` | PASS；保留 10 題主題、分析與可測試情境 |
| 八模組 AI Agent | 作業規範 Proposed Scheme；原提案 §五 | §6.1–6.3 | `DESIGN.md`; `docs/design/architecture.md` | PASS；恰為八個原概念模組，名稱一致 |
| 資料流、合約、來源、單位與信任邊界 | Stage 3 design requirements | §6.1–6.5 | `architecture.md`; `algorithms.md` | PASS；unknown ≠ 0，kcal/g/kcal per 100 g；來源版本明示 |
| Flowcharts | 作業規範要求架構/流程圖 | §6.1–6.2 Mermaid 圖 | `architecture.md` | PARTIAL；人工檢視完成，但 Mermaid parser 未安裝/未執行，語法 parser 驗證待補 |
| Pseudocode with line numbers | 作業規範要求 pseudocode | §6.4 | `docs/design/algorithms.md` | PASS；整合版含行號，並標註待實作規格 |
| Evaluation plan | 原提案 Proposed Scheme；Stage 3 | §7 | `docs/design/evaluation-plan.md` | PASS；500 筆、參照標籤、基線、指標、20×7 feasibility 全保留 |
| A2Z PA–PM Proposed Scheme | A2Z PA–PM | §6–7 | `architecture.md`; `algorithms.md`; `evaluation-plan.md` | PASS；結構標籤於本矩陣映射，不將範例當額外科學要求 |
| A2Z Q–V simulation/evaluation | A2Z Q–V | §7 | Stage 3 evaluation plan | PASS；計畫性 simulation/evaluation，不聲稱已執行 |
| A2Z W–Z conclusion | A2Z W–Z | §8–9 | Stage 1–5 evidence ledgers | PASS；預期貢獻、限制及未來工作 |
| References / IEEE numbering | 作業規範 References；Stage 6 unified bibliography | §10及 `reference-mapping.md` | Stage 1–5 verified reference lists | PARTIAL；編號與 crosswalk 固定；須完成正式 metadata 最後抽查 |
| 必交 Proposal document | 教師規範 proposal stage | `docs/final/DietSense-Final-Proposal.md` | Stage 0 inventory | PASS；Markdown 提案完成，未轉 PDF/DOCX |
| 必交 DESIGN.md | 教師規範要求 | 根目錄 `DESIGN.md`（原 Stage 3 文件） | 磁碟實存、Stage 3 validation | PASS；存在且未修改 |
| GitHub repository / GitHub link | 作業規範列作 proposal deliverable | workspace root | Local Git initialized on `main`; `origin` is `https://github.com/wujin57/AIOT-DIC3.git`; remote is empty and nothing is committed/pushed | PARTIAL；repository setup verified, but remote still has no project files pending commit/push approval |
| Proposal PPT | 作業規範 proposal deliverables | `references/DietSense_Proposal_Presentation.pptx` 是原始來源 | 原始 22 slides 已讀取 | PARTIAL；原簡報存在，未產製/QA 最終整合版 PPT |
| README | Stage 6 submission prep | 根目錄 `README.md` | 本次新增 | PASS；明示是 proposal，無 app 指引 |
| Final handover source code/data/results/video | 規範中屬期末成果/交接 | checklist 明列為未完成後續項 | assignment PDF pp. 3–4 | NOT APPLICABLE to this proposal-only stage；未虛構產物 |

## 原提案與 A2Z 的關係

教師規範與原提案採「Abstract、Introduction、Related Work、Deep Research、Proposed Scheme、References」；A2Z 範例則把研究敘事分成 A–F、G–L、M–O、PA–PM、Q–V、W–Z。此整合稿保留教師明列的 Deep Research 三項及八模組設計，同時用 A2Z 作章節內映射。A2Z 是結構示例，不覆蓋或刪除教師明訂的內容；RQ–V 以本計畫評估方法涵蓋，未宣稱有已完成模擬。
