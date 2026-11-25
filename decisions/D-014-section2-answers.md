# D-014 — How we answer Section 2 (Q1–Q3)
Date: 2026-11-25
Status: PROPOSED (draft in submission/section2-ai-model-knowledge.md)

## Q1 choice: Claude Sonnet 5.5 as the main loop + Opus 5.5 for hard planning + a cheap model for sub-tasks;
open weights (Kimi K3.x / GLM-5.x / Qwen3.x 27B) when data can't leave the premises.
Why: the independent same-harness benchmark (vals.ai Terminal-Bench 4.0) puts the Claude models at the top,
with Sonnet within ~1 point of the leader at lower cost. Routing saves more than switching vendors.
Alternatives considered: GPT-6.1 Sol (best value; strong option if cost dominates), Gemini 4 (fastest per task,
leads some app-agent boards). Rejected as the DEFAULT because they're behind on the same-harness agentic
benchmark, not because they're bad.
Honesty note: the answer is written by Claude (an Anthropic model) recommending Claude. To reduce bias we used
an independent benchmark, showed the boards where Gemini and GPT lead, and made the real recommendation
"run your own eval". The user should judge this choice himself.

## Q2: expected cost = compute + P(error) x cost of error; shadow mode; use our 8B vs 4B bake-off as a live example.
## Q3: the in-house GPU product = the national-scale version of our prototype (keeps one story across the submission).
Alternative considered: a different product (e.g. an Urdu voice tutor). Rejected: it would split the
submission into unrelated pieces. The assessment says Q3 may be anything, but one connected story is stronger.

## Update 2026-11-25 (v2 of the draft)
- Added an overview table of the 8 model categories the assessment lists, each linked to where it fits in this
  project. Image/video generation: not for marking, only possible synthetic training data, which must be validated.
- Q2: placeholder replaced with a REAL example from our bake-off. Qwen3-VL-4B was both slower (15.6 vs 8.7 s/page)
  and much worse (40% vs 100% letters) than the 8B. "Smaller = cheaper" failed on our task.
- Q3: GPU sizing filled in from measured throughput (~300 pages/hour on one consumer GPU, single stream). ~80M pages
  -> ~265 consumer GPUs in a 6-week 24/7 window. Stated as an UPPER bound; batched data-centre serving untested.
- Q3 "build first": now reports the actual prototype results (D-018, D-019, D-021).
Status of the Q1 choice: APPROVED by the user (2026-11-25, "liked the section 2 draft"). v2 rewritten in simpler English at the user's request; content and numbers unchanged.
