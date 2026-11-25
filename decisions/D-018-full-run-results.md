# D-018 — Results of the full run (before the ablation)
Date: 2026-11-25
Status: RECORDED. Source: prototype/marking_audit_v2_run.ipynb (completed run, not to be edited) and prototype/outputs/.
Hardware: one consumer GPU, NVIDIA RTX 5060 Ti 16 GB (desktop), Ollama, qwen3-vl:8b-instruct.

## Reading (bake-off re-scored after the merge-bug fix, 5 scripts)
- Chosen: pipeline C (red-layer split) + qwen3-vl:8b-instruct.
- Student answers: MCQ letters 99%, questions found 95%.
- Examiner red numbers: 27.4% correct (29.0% before the merge fix; the fix also removed some readings that
  had been right by luck. Both numbers reported).
- Red-mark reading error used in the simulation noise: 72.6%.

## AI second reader (all 50 scripts)
- Exact agreement with the true mark: 70%. Mean absolute difference: 0.37 marks per question.

## H1 (planted errors)
- One plan (13 errors), 20% budget: ranked 53.8% vs random 20.3% (all scripts); 66.7% vs 18.6% without the
  uncertain students. Too few errors to trust: wide intervals, and at a 5% budget ranked caught 0%.
- MAIN RESULT, 30 random plans, 20% budget: ranked 30.1% (range 16.7–47.9%) vs random 20%.
  Ranked is better than random on average at EVERY budget (5–50%), about 1.5x at 20%,
  but not in every plan (the lower end is below random).
- By error type (one plan): arithmetic/copy errors caught (C1, C2, J3 1/1; C3 3/4). Judgement errors mostly
  missed (J1 0/1, J2 1/5).

## Real-world pilot (original teacher records, nothing planted)
- Student_11 (Q34 counted twice, 4/2): rank 1 of 50 (rule: mark > max).
- Student_12 (short-answer section total doesn't add up): rank 2.
- Student_10 (correct MCQs crossed out, recorded 2, true ~8): rank 13. The AI second reader computed
  8 vs recorded 2 (exactly right), but noisy flags on other scripts pushed it down. Missed at a 20% budget
  (top 10), caught at 30%.

## H2 (cost)
- ~60 s per script (mean, inflated by the D-017 incident; switching to the median).
- About Rs 1.04 per script (energy + hardware, our assumptions) vs Rs 35 for a human re-check. ~480 scripts
  per GPU per 8-hour day.

## MAIN LIMITATION (user's conclusion)
The examiner's RED INK (the per-question numbers and tick counts) is not read reliably (27%). This creates
false "page vs award list" and "tick count" flags on almost every script, which bury the real signals.
Everything else works: student reading (99%), the rule checks (they found the real errors at ranks 1–2), and
the AI second reader (it found Student_10's 6-mark loss).

## Hardware note (user)
These runs used ONE consumer GPU (RTX 5060 Ti, 16 GB) and an 8B model, and it already processes a script in
about a minute for about Rs 1. A state-level deployment would have far better hardware (data-centre GPUs).
What that changes, honestly:
- Speed and volume: clearly better (more GPUs, batched serving with vLLM).
- Accuracy: hardware alone doesn't fix reading. But it makes possible (1) much larger vision models (30B–70B+)
  that can't fit on 16 GB, and (2) fine-tuning a model on board scripts with red marks (see Q3). Those two are
  the most promising fixes for the red-ink problem, together with the cheap fixes in D-016 (fade less,
  red-number prompt, crop each red mark). Whether they work must be TESTED, not assumed.

## Next: ablation (user approved), see D-019
