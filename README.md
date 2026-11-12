# DietSense — Project Proposal

**GitHub repository:** [wujin57/AIOT-DIC3](https://github.com/wujin57/AIOT-DIC3) (default branch: `main`)

DietSense is an academic proposal for a conversational, Traditional Chinese domain AI agent that would help record and estimate daily calorie intake from Taiwanese meal descriptions. This repository contains research and design documentation only. **A working application has not been implemented, and no experiments or user studies have been conducted.**

## Research scope

The proposal studies whether structured nutrition-data retrieval, bounded clarification, deterministic nutrient calculation, source traceability, and explicit uncertainty handling can support auditable logging of Taiwanese mixed dishes. The proposed evaluation includes a planned 500-item food-description dataset, a fixed manual-search baseline, and a 20-participant, seven-day feasibility study. The study is prospective and does not claim clinical effectiveness.

## Main documents

- [Final integrated proposal](docs/final/DietSense-Final-Proposal.md)
- [Requirements compliance matrix](docs/final/requirements-compliance-matrix.md)
- [Reference mapping](docs/final/reference-mapping.md)
- [Submission checklist](docs/final/submission-checklist.md)
- [Stage 6 final validation](docs/reviews/stage6-final-validation.md)
- [DESIGN.md](DESIGN.md)

## Architecture overview

The proposed design retains eight conceptual modules: user interface, conversation manager, LLM planner, retrieval, Analytics Engine, Domain Knowledge, database, and API Gateway. The LLM handles language and workflow planning; a deterministic calculation module handles numeric outputs using retrieved, versioned nutrition records. Unknown nutrients remain unknown rather than being treated as zero. Safety, privacy, and source governance are design proposals, not implemented controls.

Detailed supporting material is in `docs/design/` (architecture, algorithms, evaluation plan), `docs/research/` (evidence ledgers, literature records and Deep Research), `docs/refactored/` (Stages 1, 4 and 5 academic sections), and `docs/reviews/` (stage-specific validation and change logs). Instructor-provided documents remain in the local `references/` directory and are excluded from version control until redistribution permission is confirmed.

## Known limitations

The proposal's dataset, baselines, sample size and candidate thresholds remain prospective. Literature search was scope-based rather than a systematic review. Food-source coverage, recipe licensing, reference-label reliability, ethics review, protocol details and expert review remain to be completed. Mermaid diagrams were manually inspected but not parser-validated. Final reference metadata requires a final publisher-record spot-check. This handover is prepared for the `main` branch; no commit or push has been made.

## How to review

Start with the final proposal, then use the compliance matrix to trace instructor and A2Z requirements. The reference mapping translates stage-local IDs to the final numbered bibliography. The checklist distinguishes proposal-stage deliverables from later final-handover requirements. No installation or execution instructions are provided because there is no application to run.
