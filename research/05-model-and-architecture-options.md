# Research 05 — Model and architecture options (local, 16 GB GPU)
Date: 2026-11-25

## What the pipeline has to do
1. Read the student's handwriting per question (questions appear out of order).
2. Read the examiner's RED marks: ticks/crosses, per-question marks, section and grand totals.
3. Judge each answer against the key (MCQ: exact; short answer: key points).
4. Produce a risk score per script.

## Evidence on current models (Nov 2026)
- Handwriting is still hard for all models. WildHandBench (2026): best model only 71.85%, a
  "persistent handwritten gap". Source: https://arxiv.org/pdf/2608.22959
- OmniHandwritingOCR (2026): Qwen3-VL-8B had the best aggregate handwritten OCR score, beating
  much larger Qwen2.5-VL-72B and InternVL3-78B. Source: https://arxiv.org/pdf/2608.18586v1
- Small dedicated OCR models top printed-document benchmarks (PaddleOCR-VL-1.6 96.34%,
  GLM-OCR 95.22% on OmniDocBench, ~1B params) and beat Qwen3-VL-235B there. But that
  benchmark is mostly PRINTED documents. Source: https://roboflow.com/blog/best-open-source-ocr-models
- Indonesian classroom study: the VLM struggled with student handwriting, causing "error propagation"
  into LLM grading. Source: https://arxiv.org/abs/2506.04822
- Handwritten-exam VLM grading studies use Qwen2.5-VL-7B / InternVL3-8B as standard open
  baselines (arXiv 2609.14284). Cropping to bounding boxes improves small-model grading
  (arXiv 2607.18767).
- Local sizes: Qwen3-VL-8B is about 6 GB quantised, Qwen3-VL-4B about 3.3 GB (promptquorum, Nov 2026).
=> This supports our design choice: AI must not award marks. Its readings are noisy, so we use
   them only to RANK risk, and the strongest signal (red-ink consistency) needs little AI.

## Architecture options
A. One general VLM end-to-end (e.g. Qwen3-VL-8B): page image -> JSON {question: student answer,
   red mark, tick/cross} -> judge vs key in the same or a second call.
   + simplest, one model; - one failure point, can hallucinate marks, hard to explain.
B. OCR specialist + text LLM: PaddleOCR-VL / GLM-OCR transcribes -> a text LLM judges vs key.
   + modular, each stage measurable, cheap; - tuned for print, may merge red and blue ink or drop
   ticks, two models to run.
C. Classical CV for red ink + VLM for reading: HSV colour threshold separates the examiner's red
   from the student's ink. Ticks/crosses/numbers become a "red layer" image. The VLM reads
   (i) the student layer and (ii) the red layer separately.
   + the consistency audit is explainable and cheap, and the VLM gets cleaner inputs (like the
   bounding-box finding); - colour thresholds can fail on faded or pink scans.
D. Fine-tune (LoRA) a VLM on this data. REJECTED for v1: 50 scripts, no time, and it would be
   tested on what it's trained on. Belongs in Q3 (in-house GPU) as the next step.
E. Classic line-level HTR (TrOCR). REJECTED: needs line segmentation first and is weak on whole pages.

## Model shortlist (fits 16 GB, open weights)
- Qwen3-VL-8B-Instruct: best evidence for handwritten OCR at this size. Main candidate.
- Qwen3-VL-4B: faster and cheaper, for the speed/cost comparison (feeds H2 and Q2).
- InternVL3.5-8B or MiniCPM-V (8B): an alternative family, to avoid single-vendor bias.
- PaddleOCR-VL / GLM-OCR (~1B): the OCR-specialist route (option B).

## Runtime options
- Ollama (Windows native, simplest; supports Qwen3-VL). Recommended for a 2-day build.
- vLLM (fast batching, but needs Linux/WSL), or HF transformers (most control, slowest setup).

## Proposed bake-off (small, cheap, decides the model honestly)
5 pages (mixed students). We hand-transcribe them as ground truth. Measure per model:
question-number detection accuracy, student-text character error rate, red-mark reading
accuracy (mark value + tick/cross), and seconds per page. Pick by the numbers. Log the losers too.
