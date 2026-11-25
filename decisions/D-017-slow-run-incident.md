# D-017 — Incident: the full run was ~12x slower than the bake-off (fixed by restarting)
Date: 2026-11-25
Status: RESOLVED

## What happened
Section 11 (read all 50 scripts) started at ~67 s per model call. The same calls took 4–7 s in the bake-off.
Student_2 took 551 s (normal is ~40–60 s).
## Checks done
- `ollama ps`: only qwen3-vl:8b-instruct loaded, 100% GPU -> not CPU offloading.
- Task Manager: GPU 0%, CPU 58% during calls.
- `ollama run ... --verbose` text test: 73 tokens/s -> the GPU and model are healthy.
- Cache timestamps: a steady ~67 s per call, which suggests queueing/stuck state rather than slow compute.
## Fix
Quit and reopen Ollama, keep only one notebook kernel, restart the kernel, Run All (resumes from cache).
After: 4–11 s per call, ~40–55 s per script (Student_4 55 s, Student_5 39 s).
## Root cause
Not proven. Most likely another client (the old notebook's kernel, finishing the GLM bake-off) was queueing
requests on the same Ollama server, or Ollama was in a bad state. Lesson: one client per Ollama server
during measured runs.
## Impact on results
The H2 cost uses seconds per script. Student_1–3 times are distorted (cached/slow), so H2 must use the
median, not the mean. TODO: change the cost cell to median (or exclude the first 3 scripts) before reporting.
