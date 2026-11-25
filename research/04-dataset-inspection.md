# Research 04 — First inspection of the dataset (Mendeley sf3kvjwknt)
Date: 2026-11-25. Scripts used: quick python checks on the CSVs, plus looking at rendered pages of Student_1.

## What's inside
- 50 scripts, 4 pages each (A4), plus the same 50 marked by the teacher.
- Question.txt (35 questions), answerkey.txt (MCQ letters + short-answer key points),
  Teacher_manual_marks_Anonymized.csv (MCQ choices Q1–20, marks Q21–35, section totals, total).
- README says CSV totals were "cross-verified" against the marked PDFs.

## How the teacher marks (seen on Student_1)
- RED pen. A tick or cross next to every MCQ. Marks for each short answer written in red
  (e.g. "2", "1") near the answer. Section total ("12") and grand total ("33") written and circled.
- Students write in blue/black. -> Separating red ink from student ink should work (supports P4).
- Students answer the short questions OUT OF ORDER (page 2 goes 26, 28, 25, 34, 27, 30).
  -> Fixed boxes per question (our earlier plan) DON'T exist here. We must find the question
  numbers in the handwriting. This makes it closer to real Pakistani answer books, which is good for realism.

## REAL inconsistencies already in the data (before we plant anything)
1. Answer key vs teacher, Q1: the published key says B. Student_1 wrote D and the teacher TICKED it.
   Assuming the teacher accepted D for Q1 explains the recorded MCQ total for 19 more students.
   -> The teacher seems to have used a different key for Q1 than the published one. That's a
   systematic, item-level error type: one wrong key line affects many students at once.
2. Even after allowing D for Q1, 14 students have a recorded MCQ total that doesn't match their
   recorded choices (e.g. Student_10: choices give 8, recorded 2; Student_48: 9 vs 6;
   Student_34: 11 vs 13; Student_46: 15 vs 17).
   Cause unknown until we look at the pages: the choice transcription could be wrong, or the
   marking/tally could be wrong.
3. Student_11: Q34 recorded as 4.0 on a 2-mark question (over the maximum), and it's counted in the total.
4. Student_12: short-answer items add up to 21, but the recorded section total is 19.
5. Unusual codes: "NC" (Student_12 Q21, Student_43 Q30), "NM" (Student_20 Q32, not documented in README).

=> Even in a dataset whose README says it was cross-verified, a simple consistency check finds
issues in a large share of the 50 scripts. This is real-world evidence for our consistency audit.
NOT yet verified against the page images. Must check before claiming them as marking errors.

## Privacy problem in the dataset
- Student_MCQ.csv contains what look like REAL student names next to real IDs, and file.txt lists
  real IDs. The README says the data was anonymised.
- Our rule: never load, copy, quote or publish Student_MCQ.csv or file.txt. Use only the
  anonymised CSV and the Student_N PDFs. Mention this responsibly in the write-up (no names).
