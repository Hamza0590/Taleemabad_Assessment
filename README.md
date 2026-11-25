# Parakh: Risk-Ranked Auditing of Board Exam Marking with Local AI

*Parakh* (پرکھ, "to examine closely") is an audit layer that sits **on top of** the existing marking of board exams.
It does not mark papers and it never awards marks. It re-reads every marked script, flags places where the marking
looks wrong, and gives each script a **risk score**. Human checkers then review the riskiest scripts first,
instead of a random 20% sample.

Everything runs **locally** on one consumer GPU (RTX 5060 Ti, 16 GB) through [Ollama](https://ollama.com), so no
student script leaves the machine.

> Case study submission for the Taleemabad AI Internship (Future of Education Challenge), November 2026.
> Full report: [`report/Parakh_report.pdf`](report/Parakh_report.pdf) · Results workbook: [`results/Parakh_results.xlsx`](results/Parakh_results.xlsx)

---

## The problem in one paragraph

In Pakistani board exams, a "re-check" usually means **re-counting** the totals, not re-reading the answers. A script
that is ticked correct but under-marked, or has a mark copied wrongly to the award list, is rarely caught. Boards that
use e-marking review a **random** sample (around 20%) of the work. Random sampling spends most of the review time on
scripts that were marked correctly. Parakh asks a simple question: **with the same 20% review budget, can we choose
*which* scripts to review so that more marking errors get caught?**

## How it works

```
marked script (PDF)
      │
      ▼
 1. Render pages ──► 2. Split ink: student layer (blue/black) + examiner layer (red)
                                   │                       │
                                   ▼                       ▼
                     3. Local vision model reads each layer (qwen3-vl:8b-instruct)
                                   │
                                   ▼
 4. Consistency rules   – totals add up? copied correctly to the award list? mark ≤ maximum? every answer marked?
 5. AI second reader    – an independent mark estimate per answer vs the key (used only as a signal)
                                   │
                                   ▼
 6. Risk score = 10 × strong flags + 3 × other flags + AI disagreement
                                   │
                                   ▼
 7. Review queue: humans check the top 20% by risk
```

## Main results

The dataset is public and was already marked by a teacher, so the evaluation **plants known marking errors** (six
types: copy error, total error, mark over the maximum, under-credit, over-credit, unmarked answer). The error plan is
sealed before the audit runs. It also checks the dataset's **real** teacher records, where nothing was planted.

| What we measured | Result |
|---|---|
| Student handwriting read correctly (chosen pipeline) | ~99% of letters, 95.1% coverage |
| Examiner's red marks read correctly | **27.4%** (main limitation) |
| Errors caught at a 20% review budget, averaged over 30 random error plans | **30.1% with Parakh vs 20% random** (range 16.7–47.9%) |
| Best variant in the ablation (rules + AI second reader, no red-ink flags) | **39.2%** caught at 20% budget |
| Real errors found in the original teacher records | 3 real cases; ranked **#1, #2 and #13** of 50 |
| Estimated cost (see D-021, an estimate under stated assumptions) | **~Rs 0.83 per script** vs ~Rs 35 for a human re-check; ~600 scripts/day on one PC |

**The main limitation is reading the examiner's red ink.** Question numbers fade in the red layer, so the model often
can't tell which question a red mark belongs to. Because of this, flags built on red-ink readings add noise, and
removing them improved the result (30.4% → 39.2%). All runs used one consumer GPU. A board-level deployment would
use much stronger hardware and larger models.

Full details, negative results included, are in the report and in [`decisions/`](decisions/).

## Repository layout

```
prototype/
  marking_audit_v2_run.ipynb   one notebook, a heading on every block, all outputs kept
  outputs/                     result tables (CSV/JSON) and the cache of every model answer
data/
  baseline_fixes.csv           3 verified issues in the original dataset (kept apart from planted errors)
  README.md                    how to download the dataset
decisions/                     D-001 … D-026: every design choice, the options considered, and why
research/                      notes and sources behind the figures in the report
report/                        PDF report + LaTeX source
results/                       Excel workbook of all results
```

## How to run it

**Requirements:** Windows or Linux, Python 3.11+, an NVIDIA GPU with ~16 GB of VRAM (8 GB works for the 4B model), and
[Ollama](https://ollama.com/download).

```bash
# 1. Python packages
pip install -r requirements.txt

# 2. Local models (the "-instruct" tags matter: the default qwen3-vl tags "think" silently and return empty text)
ollama pull qwen3-vl:8b-instruct
ollama pull qwen3-vl:4b-instruct      # used in the bake-off and as the structuring model
ollama pull minicpm-v4.5              # bake-off only
ollama pull glm-ocr                   # bake-off only

# 3. Dataset: download it into data/ (see data/README.md)

# 4. Open the notebook from inside prototype/ and run the cells in order
cd prototype
jupyter notebook marking_audit_v2_run.ipynb
```

**No GPU?** Every model answer is cached in `prototype/outputs/cache/`. With the dataset in place, re-running the
notebook reuses the cache and gives the same numbers without calling a model again. The audit and evaluation sections
(13–18) only need the CSV files.

**Run order:** sections 0–10 (setup and bake-off) → 11–12 (read all 50 scripts, AI second reader) → 13–18 (planted
errors, audit, evaluation, ablation, cost). Seeds are fixed: 2026 for the main plan, 100–129 for the 30 repeated plans.

## Data and privacy

- Dataset: K. P. Dinesh, *A Dataset of Digitized Student Examination Papers, Answer Keys, and Manual Evaluations for
  Automated Grading Research*, Mendeley Data, V1, 2026. DOI: [10.17632/sf3kvjwknt.1](https://doi.org/10.17632/sf3kvjwknt.1)
  (CC BY 4.0). It is **not** included here. Download it from the source.
- The dataset ships `Student_MCQ.csv` and `file.txt`, which appear to contain real student names and IDs. **They are
  never loaded** by the notebook. Only the anonymised files are used.
- Problems found in the dataset itself (for example, the Q1 answer key mismatch) are reported as pre-existing and kept
  separate from the planted errors (D-010, D-012). The official answer key (B) is followed.
- Real board scripts were not publicly available, so this is a proof of concept on a public English-language exam.

## Author

**Muhammad Hamza**, BS Artificial Intelligence, FAST NUCES Islamabad ·
[LinkedIn](https://linkedin.com/in/hamza35502) · [GitHub](https://github.com/Hamza0590)

Code is released under the MIT License (see `LICENSE`). The dataset keeps its own CC BY 4.0 license.
