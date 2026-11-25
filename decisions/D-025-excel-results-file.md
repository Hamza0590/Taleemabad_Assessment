# D-025 — Excel results file for the submission form
Date: 2026-11-26
Status: DONE
File: submission/Parakh_results.xlsx (8 sheets + README), built from prototype/outputs/*.csv.

## Sheets
1_Bakeoff, 2_H1_30_Plans (main result + chart), 3_H1_One_Plan (shown for honesty), 4_Error_Types (from notebook
section 15b, copied by hand), 5_Ablation (+ chart), 6_Real_Errors (budget is editable), 7_Pilot_All_50, 8_Cost.

## Choices
- Numbers copied from the output files are blue; calculated cells are formulas (black), so a reviewer can check them.
  Cost assumptions are yellow input cells: changing them recalculates the cost (D-021).
- 6_Real_Errors has an editable review budget: at 22% all three real errors are caught under rules + AI.
- 7_Pilot_All_50 ranks by sort order, while 6_Real_Errors counts ties pessimistically (Student_10 is 13 vs 14). Noted in both sheets.
- Checked: 120 formulas, 0 errors after LibreOffice recalculation; cost = Rs 0.83, 600 scripts/day, H1 30.1% vs 20%.
