# D-011 — Architecture and model
Date: 2026-11-25
Status: DECIDED (user agreed 2026-11-25). Options and evidence in research/05.

## Proposed
Architecture C: red-ink separation (classical CV) + a VLM reading the student layer and the
red layer separately. Option A (one VLM end-to-end) is the baseline to compare against.
Models in the bake-off: Qwen3-VL-8B (main), Qwen3-VL-4B (speed/cost), one other family
(InternVL3.5-8B or MiniCPM-V), and one OCR specialist (PaddleOCR-VL or GLM-OCR).
Runtime: Ollama on Windows.
## Why
- Explainability: the main signal (examiner's marks vs examiner's own ticks, totals) comes from
  the red layer, mostly without AI judgement.
- Evidence says VLMs are still unreliable on handwriting, so cleaner inputs plus a bake-off is safer.
## Rejected
D (fine-tuning: no data or time, goes into Q3 instead), E (TrOCR: needs line segmentation).

## Concrete Ollama models for the bake-off (tags checked on the Ollama library, 2026-11-25)
| Role | Tag | Download size |
|---|---|---|
| Main candidate | qwen3-vl:8b | ~6.1 GB |
| Speed/cost candidate | qwen3-vl:4b | ~3.3 GB |
| Other family | minicpm-v4.5 (built on Qwen3-8B + SigLIP2) | ~6.1 GB |
| OCR specialist | glm-ocr (0.9B) | ~2.2 GB |
Total ~18 GB of disk. qwen3-vl needs Ollama >= 0.12.7; glm-ocr needs a recent Ollama.
InternVL3.5 dropped: not in the official Ollama library, and we'd need a custom build.
MiniCPM-V 4.5 is the "other family" stand-in. Note: its language model is Qwen3-based too,
so the vision encoder differs but the language backbone family doesn't fully. A limitation to state.
User cleared other local Ollama models except the Qwen 30B coder (housekeeping, not a project decision).
