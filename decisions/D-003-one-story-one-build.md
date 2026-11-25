# D-003 — Link A, B, C, F into one story, but build only one thing
Date: 2026-11-24
Status: DECIDED (user confirmed C on 2026-11-25)

## User's input
"A, C, B and F are linked and we can make a story out of it."

## Options explored
1. Build something for all four (tutor + guidance + marking audit + parent outreach).
2. Present four separate problems and pick one.
3. One causal story that connects all four, plus one build target.

## Proposed decision
Option 3.

## The thesis that links them (causal, not just thematic)
In a government school, the board exam is the ONLY real feedback signal the system has
about a student. Every other part depends on it:
- A (one teacher, 100 students): the teacher can't watch everyone, so marks are the only way
  to know who is falling behind.
- B (no guidance): counsellors, parents and students decide paths (MDCAT or not, which
  field) based mainly on board marks.
- F (parents see no return): parents judge whether school is "worth it" from results.
  Bad results, fair or not, push kids toward "open a shop after matric".
- C (broken marking): if that one signal is noisy or unfair, every decision built on top
  of it is wrong as well.
So C sits at the centre. It's the sensor the whole system reads, and nobody checks the sensor.

## Why not option 1
Four half-built tools in 2 days would be shallow. The challenge values depth, experiments
and documented failures over breadth.

## Why C is the build target (proposed)
- The most measurable: a tick/mark mismatch is either there or it isn't.
- Timely: Punjab boards are rolling out on-screen marking in 2026, so scanned scripts will exist.
- Buildable in 2 days with CV + VLM on scanned answer sheets.
- Fixing the sensor makes A, B and F better without building them.

## Rejected framings
- "AI grades the papers": crowded, and boards are reluctant to hand grading to AI.
  We audit human marking instead of replacing it.
