# D-016 — Bake-off results and the red-number reading problem
Date: 2026-11-25
Status: DECIDED (user, 2026-11-25): option (a), accept the current reading accuracy and move on; only the free merge-bug fix applied

## Bake-off (5 scripts: Students 1, 5, 14, 10, 11), section 9
| Pipeline | Model | Coverage | MCQ letters | Red-number acc (short answers) | s/page |
|---|---|---|---|---|---|
| A | qwen3-vl:8b-instruct | 0.957 | 1.00 | 0.129 | 8.7 |
| A | qwen3-vl:4b-instruct | 0.583 | 0.40 | 0.113 | 15.6 |
| A | minicpm-v4.5 | 0.969 | 0.97 | 0.161 | 10.9 |
| C | qwen3-vl:8b-instruct | 0.957 | 0.99 | **0.290** | 12.2 |
| C | qwen3-vl:4b-instruct | 0.957 | 0.99 | 0.194 | 28.8 |
| C | minicpm-v4.5 | 0.982 | 0.99 | 0.113 | 13.4 |
| B | glm-ocr | 0.595 | 0.97 | n/a (cannot see red) | 27.8 |
(The s/page for the first configs is a bit low, because page 1 came from the smoke-test cache.)

Findings:
- Reading the STUDENT is solved: letters 97–100% for every model except qwen 4B on raw pages.
- Reading the EXAMINER's red numbers is the hard problem: best is 29% (C + Qwen 8B).
- Red layer (C) helps Qwen: 8B 13% -> 29%, 4B 11% -> 19%. It does NOT help MiniCPM (16% -> 11%).
- Rule winner (section 10): C + qwen3-vl:8b-instruct (letters + red = 1.28; next best is 1.18).

## Why red-number reading fails (C + Qwen 8B, 62 short-answer marks)
| Failure | Count | Share |
|---|---|---|
| correct | 18 | 29% |
| question not found in the red layer | 20 | 32% |
| question found, but no number returned | 17 | 27% |
| wrong number | 7 | 11% |
Examples: Student_1 Q21 was reported on 3 pages (2+2+2 = 6, true 2): duplicate readings get summed.
Student_5 Q21 was read as 26 (two marks merged into one number).

## Diagnosis
1. The red layer fades the student's writing to light grey (205), which also fades the QUESTION NUMBERS,
   so the model can't tell which question a red mark belongs to (32%).
2. Our merge code keeps red readings for questions the student layer didn't find on that page, so the
   model's guesses on other pages get added -> duplicates (our bug).
3. The prompt asks for ticks AND numbers. The model often reports only the tick (27%).

## Options
a) Accept 29% and go on. The simulation then adds ~71% reading noise to page marks, so the page-vs-list
   checks become mostly noise and H1 relies on the strong flags + AI disagreement. Honest, but weak.
b) Quick fixes (~30 min, re-test C + Qwen 8B only on the 5 scripts, ~5 min run):
   - fade the student ink less (keep question numbers readable)
   - keep a red mark only if the student layer found that question on the SAME page (fixes duplicates,
     still sums true continuations like Student_11 Q34)
   - a prompt that asks specifically for the red NUMBER per question
   PROPOSED.
c) Crop every red blob (connected components) and read each digit separately, then match it to the nearest
   question by position. Probably the most accurate, but needs positions (more code, more risk). Keep as future
   work / Q3, unless (b) fails badly.

## Decision (user)
"From 13% to 29% is good, but obviously not that good. Within this short span we can only go this far."
-> Option (a): keep C + qwen3-vl:8b-instruct as it is and continue to the full run. Options (b) (lighter fade,
   red-number prompt) and (c) (crop each red mark and read it by position) become "what I'd do with another week"
   in the submission.
-> Exception: the duplicate-merge bug (#2) is fixed now, because it's OUR code error, needs no new model calls
   (it only changes how cached answers are combined), and leaving a known bug in would be wrong.
   The bake-off is re-scored from the cache after the fix. Both numbers (before/after the fix) are kept here.
## Consequence to state in the report
With ~29% red-number accuracy, the simulated page reading gets ~71% noise, so the page-vs-list checks
are weak. H1 then rests mostly on the strong flags (over max, totals) and the AI second reader. If H1 still holds,
that's a conservative result; if not, this is the first thing to improve.
