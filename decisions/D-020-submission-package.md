# D-020 — What we submit, and where it goes in the form
Date: 2026-11-25
Status: DECIDED (user, 2026-11-25). Work order 1–8 as listed; a small front end (review-queue screen) is added LAST, if time allows. Each section is written as its own .md file first; the PDF is made only when the user says so.

## The form (seen by user)
- Text area: "complete case study response", links allowed (Google Docs, presentations, etc.)
- Document upload: Word/PDF, max 10 MB (optional)
- Excel upload: .xls/.xlsx, max 10 MB (optional)
- Video upload: .mp4/.mov/.avi/.wmv, max 100 MB (optional)
The assessment itself specifies no format.

## Proposed mapping
| Form field | What goes in | Why |
|---|---|---|
| Text area | Short cover note (problem, idea, headline results, main limitation) + links: GitHub repo, presentation | Reviewer sees the story in 1 minute; links lead to the evidence |
| Document (PDF) | Full report: Sections 1–3 + model-category overview + limitations + sources | Core deliverable, answers every question |
| Video | 2–4 min screen recording in the user's voice: the problem, the notebook running, results | Shows the working system without the reviewer needing a GPU |
| Excel | All result tables (bake-off, H1, 30-plan robustness, ablation, real-world pilot, cost) | Lets reviewers check the numbers themselves; costs little |
| GitHub (link) | Notebook WITH outputs (the _run file), decisions/, research/, README (how to run), no dataset files | Shows the process and failures they asked for |

## Rejected / deprioritised
- Vercel deployment of the prototype: the system needs a local GPU + Ollama, and the design principle is that scripts
  never leave the board's machines. A live web version would contradict that. An optional read-only results page
  is possible later, clearly labelled "pre-computed".
- Presentation: not requested. Lowest priority. If made, linked in the text area.

## Repo hygiene
- Never include Student_MCQ.csv or file.txt (real names/IDs).
- Don't commit the dataset; link to its DOI (CC BY 4.0) instead.
- Rendered page images and the cache contain student handwriting from the public dataset. Leave them out of the repo
  (they're large and not needed to read the results).
