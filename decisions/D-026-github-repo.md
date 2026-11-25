# D-026 — GitHub repository: what goes in, what stays out
Date: 2026-11-26
Status: DECIDED
Folder: parakh-repo/ (a clean copy; the working folders are not changed)

## Which notebook
Three notebook versions exist in prototype/:
- marking_audit.ipynb — first version, superseded by v2.
- marking_audit_v2.ipynb — code twin of the run file (ablation cells added there first), partial outputs.
- marking_audit_v2_run.ipynb — the completed run: every cell, ablation included, all outputs.

Chosen: only **marking_audit_v2_run.ipynb** goes in the repo, with its name kept so that the report's
reproducibility appendix still matches. Rejected: putting all three in (confusing for a reviewer: which one is real?);
renaming it to something cleaner (it would break the reference in the report).
Locally, the two older versions are moved to prototype/archive/ instead of being deleted (deletion cannot be undone,
and they show the development history).
One change in the repo copy only: the %pip output printed a local path containing the Windows user name. It was
replaced with `<python-env>`. Code and results are untouched.

## Included
Notebook, result CSV/JSON, the model-answer cache (1.3 MB of text, checked: no student names), data/baseline_fixes.csv,
decisions/, research/, report PDF + LaTeX source, the Excel workbook, README, requirements.txt (versions from the
run's pip output), .gitignore and MIT LICENSE.
Why include the cache: anyone can re-run the evaluation and get the same numbers without a GPU.

## Excluded
- The dataset (317 MB, and it has its own licence and DOI). Linked instead, with download steps in data/README.md.
- Student_MCQ.csv and file.txt: they appear to contain real names and IDs. They are blocked in .gitignore through data/*.
- Rendered page images (145 MB, rebuilt from the PDFs) and data/verify, data/peek (crops of dataset pages).
- Section .md drafts (superseded by the report), the Excel lock file, _ablation_cells_payload.py.

## Licence
Code: MIT (most common for a portfolio project; lets reviewers reuse it). Rejected: no licence (legally "all rights
reserved", which is odd for a public submission). The dataset keeps CC BY 4.0.

## Pushing
The user pushes from his own PC with his GitHub account (an outward-facing step only he should take).
