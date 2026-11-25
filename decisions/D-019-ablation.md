# D-019 — Ablation: which signals actually help?
Date: 2026-11-25
Status: DONE. Results below (run inside marking_audit_v2_run.ipynb by the user)

## Why
D-018 showed the examiner's red ink is read badly (27%), so the page/red-ink flags fire on almost every
script. Question: do they help at all, or do they hide the strong rules and the AI second reader?

## Design
Sections 16b and 16c of prototype/marking_audit_v2.ipynb (marking_audit_v2_run.ipynb is left untouched;
checksum verified after the edit).
- Variants: full (as reported) | rules + AI | rules only | AI only.
- The SAME 30 random plans as section 15c, the same weights, NO new model calls (everything from the cache).
- Random tie-breaking, identical for every variant (rules only gives many ties at 0).
- Real-world pilot: rank of Student_10 / 11 / 12 under each variant (rank counted pessimistically for ties).

## Honesty rule
This analysis was ADDED AFTER seeing the results. It is reported next to the main H1 result (30.1% vs 20%),
never as a replacement. If a variant looks better, the claim is "the red-ink flags hurt in our setting,
because reading is weak", not "our system catches X%".

## Also changed
The H2 cost cell now uses the MEDIAN seconds per script (D-017 TODO done).

## Results (30 plans, same plans for every variant)
Error recall (share of planted errors caught):
| Budget | random | AI only | full (as reported) | rules + AI | rules only |
|---|---|---|---|---|---|
| 5% | 4% | 5.1% | 8.5% | 11.9% | 12.2% |
| 10% | 10% | 11.6% | 18.4% | 25.2% | 27.3% |
| 20% | 20% | 23.9% | 30.4% | **39.2%** | **41.1%** |
| 30% | 30% | 35.5% | 41.4% | **49.8%** | 48.2% |
| 50% | 50% | 53.9% | 60.9% | **66.7%** | 61.8% |
At 20%, the ranges over the 30 plans: AI only 8–43%, full 18–48%, rules + AI 22–55%, rules only 22–57%.
(Full = 30.4% here vs 30.1% in 15c; the only difference is the random tie-break.)

Real-world pilot, rank out of 50 (pessimistic for ties; top 10 = caught at a 20% budget):
| Real case | AI only | full | rules + AI | rules only |
|---|---|---|---|---|
| Student_10 (correct MCQs crossed, ~6 marks lost) | **10** | 14 | 11 | 50 (last) |
| Student_11 (Q34 counted twice) | 5 | 1 | 1 | 2 |
| Student_12 (section total wrong) | 12 | 2 | 2 | 2 |

H2 (median): 48 s per script -> Rs 0.83 per script vs Rs 35 for a human re-check (~42x cheaper),
~600 scripts per GPU per 8-hour day (single RTX 5060 Ti).

## What it means (and why)
1. The red-ink flags HURT: removing them lifts recall at 20% from 30% to 39% (about 2x random). Cause: red numbers
   are read correctly only 27% of the time, so these flags fire on every script. This confirms the main limitation (D-018).
2. "Rules only" looks best in the simulation (41%), but that's partly OUR DESIGN: 2 of the 6 planted error types
   (wrong total, over max) are exactly what the rules check. In the REAL pilot, rules only ranks Student_10 LAST (50/50),
   because rules can't see judgement errors. So rules only is not a good system; it only looks good on our error mix.
3. "AI only" is barely better than random in the simulation (24%). Cause: the AI second reader is wrong on ~30% of
   questions, and summed over ~35 questions every script gets a background of disagreement that hides a 1–2 mark
   planted error. But it is the ONLY signal that put Student_10 (a large, real, 6-mark loss) in the top 10.
4. Best balance: RULES + AI. ~2x random in the simulation, and in the real pilot it ranks the two arithmetic errors
   #1 and #2 and Student_10 at #11 (just outside a 20% budget, inside 30%).
## Conclusion we can state
With today's reading quality, the useful design is rules + AI second reader, WITHOUT the red-ink comparison.
The red-ink comparison becomes useful only once red-ink reading is fixed (bigger models, fine-tuning, cropping,
see D-016/D-018). This conclusion comes from a post-hoc analysis, so it's reported as such, next to the main result.
