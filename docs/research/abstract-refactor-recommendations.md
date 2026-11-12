# Abstract Refactor Recommendations — Evidence Recovery

## Original weaknesses

- The original proposal bundled public-health motivation, app-use claims, performance claims, proposed features, and expected outcomes without consistently distinguishing evidence from targets.
- Several statistics and article attributions were incomplete or did not clearly support the accompanying claim. Claims about app abandonment, doubled likelihood of meeting goals, medical costs, market growth, and broad system novelty were not suitable for reuse without source-level verification.
- The proposed method listed language-model and retrieval concepts alongside numeric nutrition calculations without a clear boundary between generated language and computed values.
- Heuristic estimate ranges were described as confidence intervals, although no statistical calibration procedure was specified.
- The original universal daily-calorie warning did not have a defined population-specific or expert-validated basis.
- Evaluation plans named a 500-item dataset, a manual tracker, 20 participants, seven days, and numerical targets, but those were plans rather than validated protocols or results.

## Corrected evidence

- The revised motivation uses the WHO's 2024 estimates (2.6 billion adults overweight, including 940 million living with obesity) and the Taiwan HPA's 2020–2024 survey statistic (51.3% of adults 18+ meeting the combined criterion). These claims are now tied to the respective official pages.
- The 59-study systematic review by Raber et al. replaces an unverified blanket effectiveness claim. The revised wording retains the review's caveats on inconsistent adherence measures and limited analysis of the relationship between monitoring use and outcomes.
- USDA FoodData Central is described only as a candidate source whose official API and data terms can be verified. It is not treated as a substitute for Taiwan-specific food-composition coverage.
- The evidence ledger distinguishes external findings, proposal statements, proposed design decisions, and untested plans. Only bounded claims directly supported by the public or official source are marked VERIFIED.

## Removed unsupported claims

The refactor removes the original proposal's unverified app-retention statistic, “twice as likely” outcome, cost and market-size statements, unsupported study-specific weight-loss result, and absolute novelty formulations such as “first” or “no existing system.” These are not asserted as false; they are excluded because the available cited record did not establish them. A systematic search and complete bibliographic review would be needed to restore any of them.

## Improved research gap

The abstract now asks a bounded, evaluable question: whether conversational retrieval, targeted clarification, and explicit nutrition calculations can produce traceable estimates for Taiwanese mixed-dish descriptions while reducing logging effort relative to a manual-search workflow. It does not claim that all existing products fail or that no prior system exists. This is a provisional task-level gap, not a completed field-wide novelty finding; a reproducible related-work search remains necessary.

## Improved method descriptions

- The LLM is assigned intent understanding and workflow orchestration; nutrient values are retrieved from identifiable records and calculations use deterministic rules over explicit portions and assumptions.
- Ambiguity triggers a clarification question; any remaining range is labeled a plausible estimate range, not a confidence interval absent calibration.
- The data source and method for Taiwan-specific foods are explicitly pending confirmation of source edition, access, nutrient fields, and data-use terms.
- Nutrition safety is expressed as a proposed boundary (general information, no diagnosis/treatment, communicate uncertainty, define escalation) rather than as a validated clinical protocol or universal calorie cutoff.
- Dataset size, baseline, measures, and user study remain future plans. The original numeric thresholds are retained only as unvalidated candidate acceptance thresholds.

## Remaining limitations

1. The literature search has not established the novelty or prevalence of the Taiwanese mixed-dish problem.
2. The specific Taiwan food-composition and recipe sources are not yet identified and checked for suitability or terms.
3. Dataset labels, sampling, annotation reliability, adjudication, and data split need a reproducible protocol.
4. Baseline selection, metric definitions, tolerance-band rationale, feasibility-study sample-size rationale, participant protections, and statistical analysis need review.
5. Safety requirements need authoritative guidance and qualified review.
6. The English IEEE-style abstract body is approximately 346 whitespace-separated words (excluding title, Index Terms, and references). Check the target course/conference limit and condense if it exceeds that limit. No wording has been cut during this evidence-recovery stage.
7. A–F and Chinese/English deliverables are substantively aligned, but the English abstract is an integrated abstract rather than visibly labeled A–F; this is appropriate if the deliverable requires IEEE form, and should be checked against the instructor's submission format.
