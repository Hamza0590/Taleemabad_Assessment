# D-004 — If e-marking is already coming, what do we add?
Date: 2026-11-25
Status: DECIDED (direction); feasibility still to be tested

## User's challenge
"You said this framework is already being implemented. Then what do we add?"

## Research done (2026-11-25)
What on-screen marking (OSM) DOES fix:
- Clerical errors: the system adds up the marks itself (Ofqual blog), so the old
  "recounting" problem largely goes away.
- Anonymity (QR codes, the examiner can't see whose paper it is), logistics, tracking,
  examiner identity checks and time limits (Dawn; Tribune Oct 2026).

What OSM does NOT fix by itself: whether the examiner's *judgement* was right.
- Internationally, the quality check on judgement is "seeding": a few pre-marked scripts are
  hidden in each examiner's pile and their marks are compared with the principal examiner's
  (Cambridge, IB, Ofqual). AQA-style sampling checks small samples per examiner.
- That covers a SAMPLE of an examiner's work, not the live script of every student.
- Pakistan reports so far mention scanning, secure IDs, face verification, time limits and
  central monitoring. No public mention of seeding or double marking (not verified as
  absent, only not reported).
- FBISE: a head examiner told Dawn that under e-marking the head examiner's role in
  checking sub-examiners became limited (Dawn). So quality checking may get WEAKER
  in the move to e-marking.
- Per-script pay plus time limits still reward speed.

## Options explored for what we add
1. AI grades the scripts instead of examiners. REJECTED: boards explicitly keep humans
   grading (CBSE FAQ: "No, examiners evaluate"), it's crowded, and handwritten
   free-response grading isn't reliable enough to replace humans.
2. Build our own OSM platform. REJECTED: this is what the boards are already buying or building.
3. An AI second reader / auditor that sits on top of OSM. It checks EVERY live script
   (not a seed sample), estimates a mark for each question from the answer and the marking
   scheme, and flags only big human–AI disagreements for a senior examiner. It also uses the
   logs OSM produces (time per script, mark distribution per examiner) to spot rushing or
   drifting examiners. CHOSEN.

## Why option 3
- Seeding asks "is this examiner good on average?". We ask "is THIS student's mark right?".
  That is the question the user's Physics paper raised.
- The AI doesn't award marks, so it fits board policy and only redirects human attention.
- It only becomes possible now, because e-marking is producing scanned scripts.

## Known risks to test (will log results)
- Can a VLM/OCR read handwritten FSc physics answers well enough? Unknown. This is the
  first experiment.
- False flags: if too many get flagged, senior examiners stop trusting the tool.
- No access to real board scripts: we'll have to simulate them (to decide in a later entry).
