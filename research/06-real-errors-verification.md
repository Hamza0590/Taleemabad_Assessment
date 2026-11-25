# Research 06 — Verifying the REAL inconsistencies against the marked pages
Date: 2026-11-25. Method: render the marked PDF pages, compare by eye with answerkey.txt, with
the teacher's own marking on other scripts, and with the CSV. Images are in data/verify/.

## CONFIRMED
### R1 — Student_10: correct MCQ answers crossed out (under-marking)
- The page clearly shows the student wrote 13 B, 14 C, 16 C, 17 B, 18 C, 19 B. All six match
  the official key, and the SAME teacher ticked these same answers on Student_1's script.
- On Student_10's script the teacher put a red CROSS on each of them, and wrote "2" as the MCQ total.
- Using the key (and the teacher's own marking elsewhere), the MCQ score should be ~8. Recorded: 2.
- Impact: ~6 marks lost out of 50 (12% of the paper), on objective MCQs, with no ambiguity.
- This is the same kind of error as the user's own Physics paper: correct work, marks taken
  away, and a recount wouldn't catch it because the totals are arithmetically consistent.
  Evidence: data/verify/s10_mcq_hi.png
### R2 — Student_11: one answer counted twice (over-marking, over the maximum)
- Q34 (2 marks max) is written in two parts: page 4 (Classifier 1) and continued on page 5
  (Classifier 2, 3). The teacher wrote a "2" next to BOTH parts, so the CSV records 4.0 for a
  2-mark question, and it's included in the total.
- Impact: +2 marks over-credited. Our rule "mark exceeds the question maximum" catches it with no AI at all.
  Evidence: data/verify/s11_all.png
### R3 — Published key vs teacher's key, Q1
- The key file says B. The teacher ticked D on Student_1 (and allowing D explains 19 more students' totals).
  Either the teacher marked with a different key or the published key is wrong. Either way, one
  key line affected many students. (Q1's options: B "little or no autocorrelation" is the
  textbook assumption, so the teacher accepting D looks like the error.)

## NOT YET VERIFIED (montage resolution too low to be sure)
Students 2, 8, 25, 26, 29, 32, 34, 35, 38, 41, 46, 48, 49 (recorded MCQ total vs CSV choices).
First look: some seem to be CSV transcription differences (e.g. Student_48 skipped some MCQs,
and the teacher's 6 ticks match the recorded 6, so the CSV choice columns are the problem), not marking errors.
-> These must NOT be claimed as marking errors. Plan: re-check at higher resolution, or let the
   pipeline process them and then hand-check its flags (which is itself a good test).
Also open: Student_12 (section sum 21 vs recorded 19), Student_20 "NM", Student_43 "NC".

## What we can honestly say now
"In a public dataset described as cross-verified, simple consistency checks plus a look at the
pages confirmed at least 2 real marking errors (one student under-marked by ~6/50, one
over-marked by +2 through double counting) and one answer-key mismatch affecting a large part of
the class. More flagged cases are still under review."
