# D-006 — The "AI audits human marking" concept already exists (UK). Repositioning what's ours.
Date: 2026-11-25
Status: DECIDED (user confirmed 2026-11-25)

## What we found
AQA (UK) trialled AI quality assurance of human marking in 2024. Ofqual has endorsed AI for
QA, not for marking (2026). See research/02. No Pakistani board does anything like it.
So the general concept is not new. Hiding this would be dishonest and easy to catch.

## Options explored
1. Ignore the UK work and present the idea as fully original. REJECTED: false, and checkable.
2. Drop the idea and pick another problem. REJECTED: the evidence for the problem is strong,
   and the UK work shows the direction is sound. Novelty doesn't need an untouched concept.
3. Cite the UK work openly as validation, and make our contribution what the UK work does
   NOT cover. CHOSEN (proposed).

## What is ours (proposed contribution)
1. Context: handwritten, bilingual (Urdu/English), low-resource boards that are partly still
   on paper, where most subjects will be hand-marked for 2–3 more years. UK work assumes
   mature OSM and typed or clean data.
2. Signal 1, needing no AI judgement: an internal-consistency audit of the examiner's OWN marks
   on a scanned script. Ticks vs awarded marks, unmarked questions, totals, marks over the
   maximum. This is the user's Physics case exactly ("everything ticked, half marks").
   It's objective, explainable, and works on paper scripts. It answers AQA's explainability concern.
3. Signal 2: an AI second reader that estimates per-question marks from the answer and the
   rubric, used only to rank risk, never to award marks.
4. Use the review budget boards ALREADY spend better: replace the RANDOM 20% review (FBISE)
   with a RISK-RANKED 20%. Same human effort, more wrong marks caught. This is measurable
   in the prototype, and it directly addresses AQA's finding that sampling doesn't fix
   individual marks.
5. Runs on-premise (student scripts are sensitive; there are millions of scripts). Links to Q3 (in-house GPU).

## Headline experiment this enables
With a fixed review budget (e.g. 20% of scripts), how many marking errors does random sampling
catch compared with our risk ranking? This is a clean, honest, falsifiable experiment.
