# D-013 — How the experiment (simulation + audit) is built
Date: 2026-11-25
Status: DECIDED (implemented in prototype/marking_audit.ipynb; user asked for one notebook with clear headings)

## 1. Two views of the examiner's record
- page marks (what the examiner wrote on the script) and award list (what got copied into the
  result system) plus the total. These mirror the real process: marking centre -> award list.
- Options considered: (a) plant errors by editing the page IMAGES (painting fake ticks/marks):
  REJECTED, too slow and unrealistic-looking in 2 days. (b) Plant on the award list only:
  REJECTED, then every error is trivially "page vs list" and judgement errors can't exist.
  (c) Simulate both views from the clean truth: CHOSEN. Judgement errors change BOTH views
  (the examiner wrote the wrong mark on the paper), so only the AI second reader can catch them.

## 2. Keeping the simulation honest
- The page marks the audit "sees" get random reading noise at the error rate MEASURED in the
  bake-off. So the simulated page reading is never more perfect than our real reader.
- The AI second reader's estimates are REAL model outputs on the REAL pages (not simulated).
- The error plan is random (seeded), saved as planted_errors_SEALED.json before the audit,
  and the audit function never reads it.

## 3. Error types: C1 copy, C2 total, C3 over-max, J1 under-credit, J2 over-credit, J3 unmarked
Rates: 30% of scripts get 1 error, 10% get 2. ASSUMPTION: no board publishes real rates.
Results are averaged over 30 different random plans (section 15c), because one plan only
plants ~13 errors and is too noisy.

## 4. Risk score
risk = 10 x strong flags (over max, total mismatch) + 3 x flags (page vs list, answered but
unmarked) + AI disagreement (sum of |AI estimate - recorded mark|).
Weights chosen by hand, NOT tuned on results (tuning on the same 50 scripts would be overfitting).
Fixed before seeing any real results.

## 5. Evaluation
Error recall at budgets of 5–50%. Random = 2,000 shuffles; ranked = bootstrap CI.
Reported with and without the 14 "uncertain" students. Plus a real-world pilot on the ORIGINAL records.

## 6. Dry run (2026-11-25)
The whole notebook was run end-to-end with a FAKE model (answers made up from the CSV plus noise)
to catch code bugs before the real models were ready. All 21 code cells ran.
Bug found and fixed: division by zero in the cost cell when time = 0; also switched to the
non-deprecated `import pymupdf`. Fake-model numbers are meaningless and NOT reported.

## AI assistance note (needed for Section 3 of the submission)
Claude wrote the notebook code from the design we agreed in D-004..D-013. The user decided the
problem, the scope, the dataset policy, local-only compute, the Q1 policy, the dataset-issues
framing and the one-notebook format. The user must read and be able to explain every cell.
