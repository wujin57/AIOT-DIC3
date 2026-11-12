# Stage 6 統一參考文獻映射

Final proposal uses one stable IEEE-style numbering sequence in `DietSense-Final-Proposal.md` §10. Earlier stage files keep their original local reference numbering. This table maps stage IDs to final IDs; it does not rewrite their source files.

| Final ID | Source / record | Prior-stage IDs mapped |
|---|---|---|
| [1] | WHO obesity and overweight fact sheet (2024 estimate; 2026 update) | Abstract A–F [1]; Abstract ZH [1]; Introduction [1] |
| [2] | Taiwan HPA 2026 World Obesity Day release | Abstract A–F [2]; Abstract ZH [2]; Introduction [2] |
| [3] | Raber et al. 2021 self-monitoring systematic review | Abstract A–F [3]; Abstract ZH [3]; Introduction [3]; Stage 2 [11]; Stage 5 RW13 |
| [4] | USDA FoodData Central API guide | Abstract A–F [4]; Abstract ZH [4]; Introduction [6]; Stage 5 D1 |
| [5] | Amoutzopoulos et al. portion-size review | Introduction [4]; Stage 2 [2]; Stage 5 RW10 |
| [6] | Ho et al. image assessment meta-analysis | Introduction [5]; Stage 2 [3]; Stage 5 RW09 |
| [7] | Taiwan TFDA food composition database | Introduction [7]; Stage 2 [18]; Stage 5 D1 |
| [8] | Lewis et al. RAG | Introduction [8]; Stage 2 [14]; Stage 5 RW01 |
| [9] | Zeevi et al. personalized glycemic response | Introduction [9]; Stage 2 [7] |
| [10] | Gardner et al. DIETFITS | Introduction [10]; Stage 2 [8]; Stage 5 RW15 |
| [11] | Popovski et al. FoodBase corpus | Stage 5 RW03 |
| [12] | Stojanov et al. food NER | Stage 5 RW04 |
| [13] | Feher et al. food entity linking | Stage 5 RW06 |
| [14] | Ogrinc et al. zero-shot food NER/NEL | Stage 5 RW05 |
| [15] | Yao et al. ReAct | Stage 2 [14]; Stage 5 RW02 |
| [16] | Thames et al. Nutrition5k | Stage 5 RW07 |
| [17] | Yan et al. DietAI24 | Stage 5 RW08 |
| [18] | Lemay et al. FoodMapper | Stage 5 RW16 |
| [19] | Zhou et al. NutriRAG | Stage 5 RW17 |
| [20] | Gjorgjevikj et al. FoodyLLM | Stage 5 RW18 |
| [21] | Lawabni et al. text-based nutrient estimates | Stage 5 RW19 |
| [22] | Cao et al. Chinese food nutrient estimates | Stage 5 RW20 |
| [23] | Chen et al. Taiwan Diabot-GPT-4o | Stage 5 RW21 |
| [24] | FDA nutrition-label regulation / CFIA guidance | Stage 5 D3 |
| [25] | Mifflin et al. REE equation | Stage 2 [4]; Stage 5 RW11 |
| [26] | National Academies 2023 Energy DRI | Stage 5 RW12 |
| [27] | Taiwan HPA DRIs, eighth edition official materials | Stage 2 [15]; Stage 5 D2 |
| [28] | Hall et al. ultra-processed diet trial | Stage 2 [9] |
| [29] | Stage 5 literature search log (project method record, not scientific paper) | Stage 5 search log |
| [30] | Hall et al. dynamic energy imbalance model | Stage 2 [1] |
| [31] | Hill et al. stress/eating systematic review | Stage 2 [10] |
| [32] | Roth et al. weight-related self-monitoring/eating-disorder review | Stage 2 [12] |
| [33] | Anderberg et al. diet/fitness apps and disordered-eating review | Stage 2 [13] |
| [34] | O’Neill et al. athlete REE equation review | Stage 2 [5] |
| [35] | Cioffi et al. older-adult REE review | Stage 2 [6] |
| [36] | Cunningham FFM/REE equation | Stage 2 [19] |
| [37] | NASEM/IOM 2005 DRI/AMDR report | Stage 2 [16] |
| [38] | NICE eating-disorder guideline NG69 | Stage 2 [17]; Stage 5 D4 |

## Citation integrity notes

- Stage 2 local numbering begins with Hall dynamic energy [1], while Stage 1/4 numbering begins with public-health sources; the crosswalk prevents confusing equal numbers across files.
- Stage 1 Abstract A–F / Chinese abstract local references [1]–[4] map in order to final [1]–[4]. The IEEE English abstract uses a different local order: its [1] HPA→final [2], [2] Raber→final [3], [3] USDA→final [4], [4] WHO→final [1]. Stage 4 Introduction [1]–[10] maps in order to final [1]–[10].
- Full Stage 2 crosswalk: local [1]→final [30], [2]→[5], [3]→[6], [4]→[25], [5]→[34], [6]→[35], [7]→[9], [8]→[10], [9]→[28], [10]→[31], [11]→[3], [12]→[32], [13]→[33], [14]→[8], [15]→[27], [16]→[37], [17]→[38], [18]→[7], [19]→[36]. Stage 3 source IDs D1–D4 map to [4]/[7], [27], [24], and [38], respectively.
- Stage 5 article IDs RW01–RW21 are retained as identifiers. RW12 is a consensus report, not one of the 20 peer-reviewed papers; RW13–RW21 are papers. The final Article Summary Table still contains 20 papers and excludes RW12.
- Official sources are not classified as peer-reviewed articles. Stage search log [28] is a project record, not external evidence.
- Cite [27] (Taiwan DRIs) only as general population reference guidance and verify current formally adopted edition before any future implementation.
- Bibliographic records for references [11]–[14], [16]–[28], [30]–[38] were transcribed from Stage 5/Stage 2 verified lists. Final submission should spot-check author lists, title, publication type and DOI on the publisher or official record. Reference [1] is an official fact sheet; its page update date and underlying statistic year are distinct.
