# D-002 — Which problem to pursue
Date: 2026-11-24
Status: DECIDED. C (marking) chosen; see D-003, D-005

## Candidates (all from the user's own experience)

### A. One teacher, ~100 students, 8 subjects (attention scarcity)
- Story: in a government school, one teacher taught every matric subject to about 100 students.
  Only students who were already strong kept up.
- Assessment: very real, but how you *describe* the solution decides how generic it is.
  The obvious fix ("AI tutor") is the most common idea candidates will submit.
- Verdict: strong motivation. Risky as a headline unless we find an unusual angle.

### B. No guidance on pathways, interests or abilities
- Story: by the end of FSc he only knew "MDCAT → medical college". He didn't know about SAT,
  universities abroad or other routes, nobody guided him, and he reached FAST by luck.
- Assessment: real and personal. Career-guidance chatbots exist, though, and the hard part
  (finding out what a student is good at) is hard to show in 2 days.
- Verdict: possible. Medium differentiation.

### C. Unfair board exam marking, where rechecking was only recounting
- Story: in the FSc Part-I Physics paper, answers were ticked correct but marks were still
  cut. He applied for rechecking and was told "it's recounting, not rechecking".
  Examiners are paid per script, which rewards speed over accuracy.
- Evidence found (2026-11-24):
  - Until recently, Punjab board rechecking only checked mark totals and unmarked questions,
    not whether the marking was correct. BISE Lahore announced in Oct 2025 that it would
    move to re-marking. (TechJuice, ProPakistani)
  - 435 examiners were punished for wrong marking in BISE Rawalpindi's SSC 2024 exam. (Dawn)
  - Punjab boards are moving to on-screen marking (e-marking), with answer scripts scanned
    and checked on a screen: announced for 2026, starting with pilots. (Dawn Dec 2025,
    Tribune Oct 2026)
  - Pass rates in Rawalpindi board are low: Class 9 2026 was 37.56%, HSSC-I 2025 was 43.46%.
    (Tribune, Dawn). This matches what he had heard (~45% failing). The real figure is
    actually worse for Class 9.
- Why this is interesting: once scripts are scanned, every script exists as an image together
  with the marks the examiner gave. For the first time, *the marking itself* can be audited
  at scale, for example spotting tick/mark mismatches like his own case, or examiners who
  drift or rush. Almost nobody will think of this. It is high-stakes (merit lists, MDCAT
  aggregates), it is timely (the rollout is happening right now), and it fits the user's
  computer vision background.
- Verdict: strongest candidate so far. It still needs checking: what the OSM systems already
  do for quality control, and whether sample scripts can be obtained or simulated.

### D. Static slides and poor lecture delivery
- Story: teachers read static slides; engagement inside a 50–80 minute lecture helps only a little.
- Assessment: real, but "AI-generated interactive slides or animations" is one of the most
  common ideas, and there are many existing tools.
- Verdict: reject as the headline problem (generic, crowded).

### E. Cheating in exam halls, with one person watching 20 camera feeds
- Story: a single monitor watches a grid of 20 cameras, so the chance of catching anything is low.
- Assessment: real (BISE talks about a "zero tolerance" anti-cheating policy). But AI
  proctoring is a crowded, well-known space with privacy and ethics concerns, and the
  "watching students" angle may not suit an edtech company's values.
- Verdict: lean reject. Possibly useful as a sub-module of C (exam integrity), not the headline.

### F. Falling demand: parents see no return on education
- Story: his matric teacher said the top-scorer count dropped from 20–30 to about 10 per 100.
  Parents push kids into tuition without motivation, then blame teachers, and many think
  "start a shop after matric, since there are no jobs anyway".
- Assessment: probably the deepest root cause, and the most unusual insight. But it's a
  social and economic problem, hard to show with a working tech prototype in 2 days.
- Verdict: excellent material for the "why it matters" story. Not the build target.

## Recommendation (Claude)
C as the main problem, with A and F as the context explaining why fair assessment matters
so much when the system already filters students out early.
Final choice is the user's.
