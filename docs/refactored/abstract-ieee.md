# DietSense: A Conversational Nutrition Agent for Taiwanese Meal Logging

## Abstract

Dietary self-monitoring is widely used in behavioral weight-management interventions, yet estimates of its effectiveness and adherence remain heterogeneous. The World Health Organization estimates that in 2024 approximately 2.6 billion adults worldwide were overweight, including 940 million adults living with obesity [4]. In Taiwan, the Health Promotion Administration reports that 51.3% of adults aged 18 years or older met the combined overweight-or-obesity criterion in its 2020–2024 National Nutrition and Health Survey [1]. A systematic review of 59 studies of behavioral weight-loss interventions found that dietary self-monitoring may support weight loss, while inconsistent adherence measures limit conclusions about how monitoring intensity relates to outcomes [2]. These findings motivate practical, evidence-aware meal logging, without implying that calorie tracking alone is a clinical intervention. This proposal will investigate whether a conversational system can reduce the effort of logging Taiwanese mixed dishes while producing traceable nutrition estimates under ambiguous food and portion descriptions. We propose DietSense, a Traditional Chinese domain-specific AI agent that uses a large language model to interpret intent and orchestrate tools, retrieves nutrient records from USDA FoodData Central [3] and candidate Taiwan food-composition and local-recipe sources, and delegates numeric estimation to deterministic calculations over retrieved values and explicit portion assumptions. The agent will request clarification when food identity or quantity is insufficiently specified and will report a plausible estimate range with its assumptions; such ranges will not be described as statistical confidence intervals unless calibrated. Domain guardrails will limit outputs to general informational support, communicate uncertainty, and avoid diagnosis or treatment. The planned evaluation will use 500 annotated Taiwanese meal descriptions, compare the system with a prespecified manual-search logging baseline, and measure absolute calorie error, accuracy within prespecified tolerance bands, logging time, task completion, source coverage, clarification frequency, and usability. A seven-day feasibility study with 20 adult participants is also planned, subject to finalized consent, privacy, and study procedures. Expected contributions include a conversational meal-logging workflow, a traceable retrieval-and-calculation pipeline, a documented evaluation dataset and protocol, and an uncertainty-aware interaction design. No experimental results are reported; performance targets in the source proposal remain candidate thresholds pending protocol validation.

## Index Terms

Conversational agents, dietary self-monitoring, nutrition informatics, food composition databases, portion estimation, uncertainty communication.

## References

[1] Taiwan Health Promotion Administration, “響應世界肥胖日　兩招啟動健康管理,” Mar. 4, 2026. https://www.hpa.gov.tw/5020/19885/n.

[2] M. Raber et al., “A systematic review of the use of dietary self-monitoring in behavioural weight loss interventions: delivery, intensity and effectiveness,” Public Health Nutrition, vol. 24, no. 17, pp. 5885–5913, 2021, doi: 10.1017/S136898002100358X.

[3] U.S. Department of Agriculture, Agricultural Research Service, “FoodData Central API Guide.” https://fdc.nal.usda.gov/api-guide/. Accessed Nov. 12, 2026.

[4] World Health Organization, “Obesity and overweight,” Fact sheet, updated Oct. 7, 2026. https://www.who.int/news-room/fact-sheets/detail/obesity-and-overweight. Data cited are 2024 estimates.
