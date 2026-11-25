# D-010 — How we handle what we found in the dataset
Date: 2026-11-25
Status: DECIDED (user approved 2026-11-25)

## Findings (details in research/04)
a) Teacher marks in red, with per-question marks and circled totals, which suits red-ink separation.
b) Students answer out of order, so we need question-number detection, not fixed boxes.
c) The data ALREADY contains inconsistencies: a key mismatch on Q1, 14 MCQ total mismatches,
   a 4/2 mark, a section-sum mismatch, and undocumented codes.
d) One file contains real student names (privacy).

## Decision 1: layout (finding b)
Options:
 1. Fixed boxes, as planned in research/03 P4. NOT POSSIBLE, because the data doesn't have them.
 2. Let the VLM read the whole page and return {question number: answer text, red marks}. CHOSEN (proposed).
 3. Train a detector for question numbers. REJECTED: no labels and no time.
Why 2: one model call per page, and VLMs read handwritten numbers well. Its errors get measured.
Reverses the fixed-box recommendation in research/03 P4.

## Decision 2: the natural inconsistencies (finding c)
Options:
 A. Ignore them and treat the CSV as the truth. REJECTED: we'd be planting errors on top of
    unknown real errors, which corrupts the ground truth.
 B. Verify each one by looking at the page images, fix the baseline (the "clean truth"),
    THEN plant errors with the random plan. Separately, report the real ones as a mini real-world
    pilot: "our audit found N real issues in a dataset that claimed to be cross-verified". CHOSEN (proposed).
 C. Remove the affected students. REJECTED: that throws away the most interesting cases and
    shrinks an already small dataset.
Why B: a clean baseline for H1, plus a REAL result, which is stronger than planted errors alone.
Risk: our own manual verification can be wrong too. We log each case with a page reference.

## Decision 3: privacy (finding d)
Never use, copy or publish Student_MCQ.csv or file.txt. No names in any output. DECIDED
(non-negotiable).

## Update 2026-11-25 — first verification results (research/06)
Confirmed: R1 Student_10 under-marked by ~6 (correct MCQs crossed), R2 Student_11 Q34 counted
twice (4/2), R3 Q1 key mismatch. 13 cases are still unverified and are not claimed.
Baseline fix: for clean ground truth, use key-based MCQ scores and cap Q34 for Student_11 at the
teacher's single award (2). Record every fix in data/baseline_fixes.csv (to create).
Q1 handling: DECIDED (user, 2026-11-25): official key B only. The teacher accepting D is reported as a key-mismatch finding.
