# Abstract A–F Refactor Change Log

## Scope and source status

The refactor uses the original DietSense proposal DOCX as the primary project source, the instructor's assignment requirements and A2Z outline as structural references, and externally verified public sources for supporting evidence.

During the initial Abstract refactoring (Stage 1B), the two required Stage 1A research documents were unavailable. They were subsequently recovered in Stage 1C:

- `docs/research/abstract-evidence-ledger.md`
- `docs/research/abstract-refactor-recommendations.md`

These documents now provide evidence traceability, verification status, recommended corrections, and outstanding research limitations.

The original DOCX and PPTX remain unchanged. No experiments have been conducted, and no experimental findings are claimed.

## Main changes

| Topic | Original proposal | Refactored treatment |
|---|---|---|
| Public-health statistics | Abstract and Introduction combine several figures, including global obesity, Taiwan prevalence, medical costs, tracking persistence, and outcome claims. | Uses two dated, attributable statistics: WHO’s 2024 global estimates and HPA’s 2020–2024 Taiwan survey result. Removed the unsupported medical-cost and tracking-retention figures from the abstracts. |
| Dietary self-monitoring evidence | States that tracking doubles the chance of meeting weight-management goals and that only 15% continue beyond 30 days, attributed to an incomplete or uncertain reference. | Replaces these with a qualified synthesis of Raber et al.’s 59-study systematic review: monitoring may support weight loss, but adherence measurement and monitoring-use comparisons are limited. |
| Existing-system limitations | Broadly asserts that current apps cannot understand everyday language, handle mixed dishes, or support Taiwanese food. | Reframes these as project challenges and a testable task. Does not claim that all existing systems fail or that no prior system exists. |
| Research gap | Claims that no system integrates conversational AI, Taiwan-local food data, uncertainty, and personal TDEE tracking. | Defines a scoped evaluation question about traceable estimates and logging effort for Taiwanese mixed-dish descriptions. A stronger field-wide novelty claim is deferred until systematic literature searching. |
| Method clarity | Lists LLM, RAG, NER, TDEE/BMR, and confidence intervals together, without consistently separating language-model coordination from numeric calculation. | Assigns intent understanding and orchestration to the LLM; retrieval to the data layer; and numeric estimation to deterministic calculations over retrieved values and explicit portion assumptions. |
| Uncertainty language | Calls heuristic ranges “confidence intervals.” | Uses “plausible estimate range” and states that statistical confidence intervals require calibration. |
| Safety | Includes a universal <1,200 kcal/day alert in the original proposed design. | Does not retain a universal cutoff in the abstracts. Calls for general informational support, no diagnosis or treatment, visible limitations, and safety rules validated against authoritative guidance and expert review. |
| Evaluation | Proposes 500 records, MyFitnessPal manual entry, 20 participants for 7 days, and targets of >85% within ±20%, 60% faster logging, SUS >70. | Keeps the dataset and feasibility-study plan prospective; defines measurable outcomes and a prespecified manual-search baseline. Moves original numeric targets to unvalidated candidate thresholds, not expected or measured results. |
| Expected contributions | Mixes functionality with quantitative performance targets. | Separates intended artifacts and capabilities from performance outcomes. No target is presented as achieved. |

## Evidence used

1. WHO, “Obesity and overweight,” updated Oct. 7, 2026. The revised text uses the page’s 2024 estimates: 2.6 billion adults overweight, including 940 million living with obesity. Source: https://www.who.int/news-room/fact-sheets/detail/obesity-and-overweight.
2. Taiwan Health Promotion Administration, “響應世界肥胖日　兩招啟動健康管理,” Mar. 4, 2026. Reports that 51.3% of adults aged 18+ met the combined overweight-or-obesity criterion in the 2020–2024 National Nutrition and Health Survey. Source: https://www.hpa.gov.tw/5020/19885/n.
3. M. Raber et al., Public Health Nutrition, 24(17), 5885–5913 (2021), doi: 10.1017/S136898002100358X. The abstract uses the review’s cautious conclusion about possible benefit and limitations in adherence measurement. PubMed: https://pubmed.ncbi.nlm.nih.gov/34412727/.
4. USDA FoodData Central API Guide. Used only to confirm the proposed retrieval source and its API model; actual integration, API key handling, and chosen Taiwan data source remain future implementation decisions. Source: https://fdc.nal.usda.gov/api-guide/.

## Claims removed or deferred for verification

- The 85% 30-day abandonment figure and the cited “updated data” attribution to Helander et al. were removed. The original reference title concerns breaks in daily self-weighing and weight gain; its support for app abandonment was not established.
- The “twice as likely” tracking outcome, global chronic-disease death share, Taiwan medical-cost estimates, app-market size and growth, Van Horn 3.3 kg result, and unverified study-specific performance numbers were not reused.
- “First integration,” “no existing system,” and similar absolute novelty language was removed pending a documented literature-search method and verified article records.
- The original article-summary rows and provisional citations were not treated as verified evidence. The bibliographic mismatches identified in the Stage 0 audit remain to be resolved in Related Work.
- The exact Taiwan food-composition database edition, access endpoint, data license/terms, and local-recipe reference procedure need verification before the method is finalized.

## Limitations and next review points

- The Stage 1A evidence ledger and recommendation files were absent during the initial refactor; they were recovered and validated in Stage 1C.
- The public-health evidence above supports the motivation, not the effectiveness of DietSense.
- The literature search was not systematic; the research gap remains deliberately scoped and provisional.
- The 500-item dataset, manual baseline, 20-person study, and seven-day duration are inherited proposal plans, not validated study designs. Annotation reliability, sample-size rationale, consent, privacy, and statistical analysis need separate review.
- The original proposal’s performance thresholds have not been justified by pilot data or reference-label uncertainty.
