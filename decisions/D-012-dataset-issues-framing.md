# D-012 — How we present the dataset's problems in the write-up
Date: 2026-11-25
Status: DECIDED (user)

## Decision
We state clearly that we used a public dataset (Mendeley sf3kvjwknt, CC BY 4.0), and that the
issues we found ALREADY EXIST in that dataset. They were not created by us:
- marking inconsistencies (Student_10 under-marked, Student_11 double-counted Q34)
- the Q1 answer-key mismatch (official key B, but the teacher accepted D)
- unverified mismatches between recorded MCQ choices and totals
- real student names in Student_MCQ.csv despite the "anonymised" claim (we didn't use the file)

## Why
- Honesty and traceability: a reader must be able to tell the dataset's original errors apart
  from the errors WE PLANT for the H1 experiment.
- It also strengthens the story: real errors existed in data described as "cross-verified".

## Options considered
1. Silently clean the data and not mention it. REJECTED: hides a real finding and looks dishonest.
2. Present the dataset errors as our "detections" without saying they were pre-existing. REJECTED: misleading.
3. Report them transparently as pre-existing, and kept separate from planted errors. CHOSEN.

## Baseline rule (for H1 ground truth)
- MCQ truth = official key (Q1 = B only) applied to the student's choices.
- Students whose recorded choices are still unverified against the page (13 students) are marked
  "baseline uncertain". The H1 results are reported with and without them (sensitivity check).
- Every correction is listed in data/baseline_fixes.csv with the reason and evidence image.

## Optional, nice to do
Politely tell the dataset author about the privacy issue in Student_MCQ.csv (responsible disclosure).
