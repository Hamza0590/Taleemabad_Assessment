# Decision Log — Taleemabad "Future of Education" Challenge

Rule for this project: every decision is written down here. That includes what we chose,
what we rejected and why, what we explored, and what failed.
Nothing gets decided without an entry here.

Each entry has a number, a date and a status (OPEN / DECIDED / REVERSED).
Entries are never deleted. If we change our mind, we add a new entry that reverses the old one
and say why.

## Index
| # | Date | Decision | Status |
|---|------|----------|--------|
| D-001 | 2026-11-24 | Stay in the education domain, but source the problem from personal observation instead of asking AI for ideas | DECIDED |
| D-002 | 2026-11-24 | Which problem to pursue (6 candidates from lived experience). Resolved by D-003 and D-005: C chosen | DECIDED |
| D-003 | 2026-11-24 | One causal story linking A, B, C, F; build only C (marking audit) | DECIDED |
| D-004 | 2026-11-25 | Add an AI second reader that audits every script on top of e-marking (not AI grading, not a new OSM) | DECIDED |
| D-005 | 2026-11-25 | Story focuses on marking only; A, B, F parked (partially reverses D-003) | DECIDED |
| D-006 | 2026-11-25 | AI marking QA exists in UK; cite it, and claim the Pakistan-specific contribution (consistency audit + risk-ranked review) | DECIDED |
| D-007 | 2026-11-25 | H1: risk-ranked beats random review at fixed 20% budget (decided); H2: cost per script (proposed) | DECIDED / PROPOSED |
| D-008 | 2026-11-25 | Public dataset instead of own collection; primary = Mendeley sf3kvjwknt (50 handwritten exams + key + teacher marks); any English paper with a key | DECIDED |
| D-009 | 2026-11-25 | Run all models locally (privacy, cost, Q3) | DECIDED |
| D-010 | 2026-11-25 | Dataset findings: VLM reads page layout (no fixed boxes); verify real inconsistencies, then plant errors; never use the file with real names | DECIDED |
| D-011 | 2026-11-25 | Architecture: red-ink separation + VLM (vs end-to-end VLM baseline); model chosen by a 5-page bake-off; Ollama | DECIDED |
| D-012 | 2026-11-25 | Report dataset issues transparently as pre-existing (not ours), kept separate from planted errors; Q1 = official key B | DECIDED |
| D-013 | 2026-11-25 | Experiment design: page + award-list views, noise calibrated from bake-off, 6 error types, 30 random plans, fixed risk weights | DECIDED |
| D-014 | 2026-11-25 | Section 2: Q1 Sonnet 5.5 + routing (open weights if data must stay); Q2 cost-of-error framing; Q3 = national-scale version of our audit | DECIDED |
| D-015 | 2026-11-25 | Smoke test: default Qwen tags returned EMPTY (hidden thinking) -> instruct tags; empty-cache bug fixed; red-layer doubled tick accuracy (9/20 -> 18/20, MiniCPM, 1 page) | DECIDED |
| D-016 | 2026-11-25 | Bake-off: student reading solved (~99%), examiner red numbers only 29% best (C + Qwen 8B); failure breakdown; decided: accept for now, merge bug fixed | DECIDED |
| D-017 | 2026-11-25 | Incident: full run 12x slow (Ollama queue/bad state), fixed by restart; use median time for H2 | RESOLVED |
| D-018 | 2026-11-25 | Full-run results: H1 ~1.5x (30.1% vs 20% at 20% budget, 30 plans); real errors ranked #1, #2, #13; main limitation = red-ink reading (27%); single consumer GPU | RECORDED |
| D-019 | 2026-11-25 | Ablation (post-hoc, reported next to the main result): full vs rules+AI vs rules only vs AI only, same 30 plans; H2 uses median | DONE: red-ink flags hurt (30%->39% when removed); rules + AI best balance; rules only misses Student_10 |
| D-020 | 2026-11-25 | Submission: text-area cover note + links (GitHub, slides), PDF report, demo video, Excel of results; no Vercel deployment; front end last; .md per section, PDF on request | DECIDED |
| D-021 | 2026-11-25 | Cost per script is an ESTIMATE: measured 48 s median + assumptions (180 W, Rs 60/kWh, Rs 450k PC, 3-yr life) = Rs 0.83 vs Rs 35 human re-check | DECIDED |
| D-022 | 2026-11-25 | Source correction: the 20% random-review e-marking report is BISE Peshawar (2023), not FBISE; all report headlines verified | CORRECTED |
| D-023 | 2026-11-25 | Q1 gets my own local model-selection experience (agentic course project: qwen3-coder:30b chosen by a pre-set smoke test) | DECIDED |
| D-024 | 2026-11-26 | Title: "Parakh: Risk-Ranked Auditing of Board Exam Marking with Local AI"; system named Parakh | DECIDED |
| D-025 | 2026-11-26 | Excel results file (submission/Parakh_results.xlsx): 8 sheets, formulas for derived numbers, editable cost assumptions | DONE |
| D-026 | 2026-11-26 | GitHub repo (parakh-repo/): only the _run notebook (old versions archived, not deleted), outputs + model cache, decisions, research, report, Excel; dataset/page images/name files excluded; MIT licence | DECIDED |
| D-027 | 2026-11-26 | Cover note for the form text area (submission/cover-note.md): story, 30.1% vs 20% headline (39.2% shown as post-hoc ablation), limitation stated, links; also corrects D-020 on the cache | DRAFT |
| D-028 | 2026-11-26 | No video (optional field); 14-slide self-explanatory deck instead, same honesty rules as the report | DECIDED |

Research notes live in ../research/

## Open items (to discuss later)
- Implementation problems of our system (user's reminder, 2026-11-25): to be discussed fully in the implementation phase. Known so far: handwriting reading accuracy, false-flag rate, no access to real board scripts.
- Implementation problems listed in research/03 (P1–P11). Decisions to follow as D-008+.
