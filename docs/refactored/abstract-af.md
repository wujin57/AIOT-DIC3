# DietSense Abstract A–F Refactor

## Evidence basis and scope

The two requested Stage 1A working documents, docs/research/abstract-evidence-ledger.md and docs/research/abstract-refactor-recommendations.md, were not present in the workspace. This refactor therefore uses the original proposal and assignment documents, plus the public sources listed below that were checked for this draft. The Taiwan food-composition source and the proposed local-recipe collection still need a precise edition, URL, and data-use review before implementation.

This is a research proposal. The dataset, prototype, user study, and performance outcomes described below are planned work, not completed experiments.

## A. Attention Getter — Motivation

The public-health context makes practical nutrition support consequential. The World Health Organization reports that in 2024 approximately 2.6 billion adults worldwide were overweight, including 940 million adults living with obesity [1]. Taiwan’s Health Promotion Administration reports that 51.3% of adults aged 18 or older met its combined overweight-or-obesity criterion in the 2020–2024 National Nutrition and Health Survey [2]. Dietary self-monitoring is used in behavioral weight-loss interventions: a systematic review of 59 studies found that most studies using either higher- or lower-intensity dietary self-monitoring reported statistically significant weight loss in intervention groups compared with controls. The review also found inconsistent adherence measures and limited analysis of how monitoring use relates to weight loss, so the evidence does not justify treating logging as uniformly effective [3]. These findings motivate an accessible, evidence-aware way to record meals while keeping estimates and their limitations visible.

## B. But — Problem and Scoped Research Gap

Food logging requires a person to identify a matching food, describe its quantity, and account for preparation and ingredients. A short description such as “one bowl of beef noodle soup” does not uniquely specify portion weight, recipe, oil, or broth consumption; Taiwanese mixed dishes therefore present a concrete test case for retrieval and portion reasoning. The project’s current source materials identify these as design challenges, but the evidence gathered for this abstract does not establish that all existing trackers fail on them or that no prior system combines the relevant capabilities.

The defensible research question is narrower: **Can a conversational system that retrieves nutrition records, asks targeted clarification questions, and computes estimates from explicit portion and source assumptions produce auditable estimates for Taiwanese mixed-dish descriptions while reducing meal-logging effort relative to manual search and entry?** This frames a measurable evaluation problem without claiming global novelty. A systematic literature search is still required before making a stronger field-wide research-gap claim.

## C. Cure — Proposed Solution

DietSense is proposed as a Traditional Chinese, domain-specific nutrition AI agent for meal logging and intake review. It will coordinate language understanding, source retrieval, deterministic nutrition calculations, and safety rules. The language model will interpret the request and choose a supported workflow; it will not be treated as the authority for nutrient values or as a clinician. The system will return a sourced estimate, relevant assumptions, and a follow-up question or limitation when available information is insufficient.

## D. Development — Proposed Method

The planned pipeline will classify user intent and extract foods, portion descriptions, preparation details, and meal context. A retrieval layer will search USDA FoodData Central [4] and, subject to source/version verification, a Taiwan food-composition source and a curated local-recipe collection. Retrieved records will retain their identifiers and nutrient fields. A deterministic analytics component will calculate calories and selected macronutrients from the retrieved values and an explicit portion estimate; the language model will not generate those numeric values from memory.

When food identity or quantity is ambiguous, the agent will ask a targeted clarification question. If uncertainty remains, it will show a plausible estimate range with the assumptions that produced it. That range will not be called a statistical confidence interval unless calibration is demonstrated. Nutrition-domain guardrails will constrain the system to general informational support, communicate limitations, avoid diagnosis or treatment, and route potentially unsafe requests to appropriate professional support. Specific safety rules and thresholds remain to be defined with authoritative guidance and qualified review; the original proposal’s fixed daily-calorie cutoff is not adopted as a universal rule.

## E. Experiments — Planned Evaluation

The team plans to construct a dataset of 500 Traditional Chinese descriptions of Taiwanese meals, with reference nutrition values and documented portion or recipe assumptions. The annotation protocol, reference-value procedure, adjudication process, and dataset split will be specified before evaluation. The primary baseline will be a manual-search-and-entry workflow in a fixed nutrition-tracking application, selected and documented before the study.

Planned measures include absolute calorie error and the proportion of estimates within prespecified ±10% and ±20% bands, meal-logging time, task completion, clarification frequency, source coverage, and System Usability Scale (SUS) scores. A feasibility user study is planned with 20 adult participants over seven days, comparing DietSense with the manual workflow. Recruitment, consent, privacy safeguards, study procedures, and analysis methods must be finalized and reviewed before data collection. These are prospective plans; no participants have been studied and no results are available.

## F. Findings — Expected Contributions

The intended contributions are (1) a conversational agent workflow for Traditional Chinese meal logging, (2) a traceable retrieval-and-calculation pipeline for nutrition estimates, (3) a documented dataset and evaluation protocol for Taiwanese mixed-dish descriptions, and (4) an uncertainty-aware interaction and safety design. The proposal does not claim that any target has been achieved. The original targets of more than 85% of estimates within ±20%, 60% shorter logging time, and SUS above 70 are retained only as unvalidated candidate acceptance thresholds; they should be confirmed or revised after the reference-label protocol and a feasibility pilot are established.

## Evidence references

1. World Health Organization, “Obesity and overweight,” fact sheet, updated October 7, 2026. https://www.who.int/news-room/fact-sheets/detail/obesity-and-overweight. The cited figures refer to 2024 estimates.
2. Taiwan Health Promotion Administration, “響應世界肥胖日　兩招啟動健康管理,” March 4, 2026. https://www.hpa.gov.tw/5020/19885/n. Reports the 51.3% estimate from the 2020–2024 National Nutrition and Health Survey.
3. M. Raber et al., “A systematic review of the use of dietary self-monitoring in behavioural weight loss interventions: delivery, intensity and effectiveness,” Public Health Nutrition, vol. 24, no. 17, pp. 5885–5913, 2021, doi: 10.1017/S136898002100358X. PubMed record: https://pubmed.ncbi.nlm.nih.gov/34412727/.
4. U.S. Department of Agriculture, Agricultural Research Service, “FoodData Central API Guide.” https://fdc.nal.usda.gov/api-guide/. The guide documents API access and data terms; it does not establish suitability of the proposed Taiwan-specific sources.

## Project-source references

- Original project direction and proposed methods: references/期中Proposal_熱量AI_Agent.docx, “一、Abstract 摘要” and “五、Proposed Scheme / Proposed Design.”
- Required proposal content and evaluation framing: references/期末專題提案作業規範 (1).pdf, pp. 1–3.
- A–F outline: references/A2Z outline example(1).pdf, p. 1.
