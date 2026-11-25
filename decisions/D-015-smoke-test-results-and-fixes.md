# D-015 — Smoke test results (first real model run) and the fixes
Date: 2026-11-25
Status: DECIDED (fixes applied to the notebook)

## What we ran
Section 8b: every model/pipeline reads ONE page (Student_1, page 1: MCQ 1–20 + Q21; the teacher
ticked 12 MCQs, wrote "12" and "33" circled, and gave Q21 a red "2"). Scored by hand from the cache files.

## Results (1 page only, so this is indicative, NOT conclusive)
| Pipeline / model | Time | Found Q1–21 | MCQ letters | Tick/cross correct | Totals |
|---|---|---|---|---|---|
| A qwen3-vl:8b | 142s | EMPTY output | – | – | – |
| A qwen3-vl:4b | 84s | EMPTY output | – | – | – |
| A minicpm-v4.5 | 55s | yes | 20/20 | 9/20 | 33 |
| C qwen3-vl:8b | 123s | yes | 20/20 | 8/20 (but read Q21 = 2 correctly) | 33 |
| C qwen3-vl:4b | 152s | yes | 20/20 | red call EMPTY | – |
| C minicpm-v4.5 | 72s | yes | 20/20 | **18/20** | 33 |
| B glm-ocr | 157s | OCR text excellent; structuring step (qwen 4b) EMPTY | – | – | – |

## What we learned
1. FAILURE: the default Qwen3-VL tags returned empty text on the longer prompts (A, the red-layer call,
   structuring), after 80–140 s. Short prompts worked. Best explanation: the default tags are
   "thinking" variants. They use their output budget on hidden reasoning and never write the answer.
   (Not fully proven: the first version of the code didn't save the hidden-thinking text.)
2. BUG in our code: empty answers were cached and would have been reused. Fixed.
3. EVIDENCE FOR OUR ARCHITECTURE (C): with the SAME model (MiniCPM), reading the examiner's ticks
   went from 9/20 on the raw page to 18/20 on our red-layer image. Separating the red ink doubled accuracy
   on this page. One page only, so the bake-off must confirm it.
4. Reading student letters is easy: every model that answered got 20/20.
5. The section total "12" was missed by everyone. Only "33" was found.
6. GLM-OCR alone reads the handwriting very well (even marks crosses as "X"), but ignores ticks. Pipeline B
   failed only because its Qwen structuring step returned nothing.
7. Speed: 55–157 s per page is slow. 200 pages x ~70 s ≈ 4 hours for a full run.

## Fixes applied
- Use qwen3-vl:8b-instruct and qwen3-vl:4b-instruct (no hidden thinking). The structuring model is now
  qwen3-vl:4b-instruct.
- Never reuse an empty cached answer. Save diagnostics: stop reason, output tokens, hidden-thinking length.
- num_ctx 16384, num_predict 3000. Images shrunk to a 1400 px max side (speed).
- The smoke test prints diagnostics when a model returns nothing.

## Options considered for the Qwen problem
a) Drop Qwen and use only MiniCPM. REJECTED for now: the best handwriting evidence (OmniHandwritingOCR)
   is for Qwen3-VL-8B; it deserves a fair test.
b) Keep the thinking tags with a bigger output budget. REJECTED: much slower per page, and speed matters for H2.
c) Switch to the instruct tags. CHOSEN.

## Update — re-run after the fix (instruct tags), same page
| Pipeline / model | Time | MCQ letters | Tick/cross | Q21 red "2" read? |
|---|---|---|---|---|
| A qwen3-vl:8b-instruct | 18s | 20/20 | 19/20 | no |
| A qwen3-vl:4b-instruct | 23s | 20/20 | 18/20 | no |
| A minicpm-v4.5 | 55s | 20/20 | 9/20 | no |
| C qwen3-vl:8b-instruct | 19s | 20/20 | 18/20 | **yes** |
| C qwen3-vl:4b-instruct | 35s | 20/20 | **20/20** | no |
| C minicpm-v4.5 | 72s | 20/20 | 18/20 | no |
| B glm-ocr | 80s | found Q1–20 (missed Q21) | – | – |
- The fix worked: no hidden thinking (0 chars), and Qwen is now 3–8x faster than before.
- CORRECTION to the earlier claim: the red layer doubles tick accuracy for MiniCPM (9 -> 18), but NOT for
  Qwen 8B, which is already good on the raw page (19/20 raw vs 18/20 red layer). So "red-layer separation
  helps" depends on the model. The 5-script bake-off decides. We must not generalise from MiniCPM.
- Only C + qwen 8B read the examiner's per-question number (Q21 = 2). Reading the red NUMBERS is the key
  ability for short answers, and it's measured in the bake-off as red_mark_acc.
