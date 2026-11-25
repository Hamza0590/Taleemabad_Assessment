# D-023 — Add my own model-selection experience to Q1
Date: 2026-11-25
Status: DECIDED (user asked for it)

## What
Q1 (Section 2.2 in the report) now has a paragraph and a table "From my own experience: choosing a local agent model",
taken from my Agentic Systems course project (D:\Uni\SEM 7\Agentic\long_horizon_agent_memory), read-only:
- decision 0043: local-only constraint and the selection rule set BEFORE testing (tool-call failures, decision test
  after a change, minutes per run);
- EXP_019 / decision 0049: qwen3-coder:30b 0/91 rejected tool calls, 3/4 decision tests, 11.4 min/run;
  gpt-oss:20b 65/105 and 99/118 rejected, 0/4, 10.0 and 7.3 min; one commit in ten episodes;
- decision 0046: LiteLLM did not detect qwen3-coder's tool support at first (tool calls as text) -> small fix -> 0 bad calls;
- decision 0038: qwen3:14b did not build the specified interface, repetition loops with greedy decoding;
- EXP_013/014: Claude Haiku 5.5 (paid) built the specified interface (upper reference).
"My choice" now names qwen3-coder:30b as the single-GPU open-weight option.

## Why
It is real, recent, first-hand evidence for the exact question (choosing an agent model), and it shows the same method the
answer recommends: fix the rule first, test on your own task.

## Citation
Cited as my own course-project records (agenticlog, agentic0038, agentic0043, agentic0046, agentic0049 in references.bib).

## Build fix made at the same time
More than 26 references now share author "Hamza" and year 2026, which broke natbib's a-z year suffixes.
Fixed with a local copy of the style, unsrtnat-numeric.bst (no suffixes; they never show in numeric citations).
Captions with citations now have a short caption for the List of Tables/Figures.
