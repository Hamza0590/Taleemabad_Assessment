# Research 07 — The model landscape for agents (as of late Nov 2026)
Collected 2026-11-25. Many of these are aggregator sites, which are lower quality and often quote vendor
numbers. The independent ones are marked [IND]. KEY OBSERVATION: the leaderboards disagree.

## Independent / standardised
- [IND] vals.ai Terminal-Bench 4.0 (as of 2026-11-19), same agent harness for all (Mini-SWE-agent):
  Claude Fable 5.2 65.15% ($14.56 total, 20.6 min), Claude Opus 5.5 65.15% ($12.04, 28.3 min),
  Claude Sonnet 5.5 64.14% ($10.75), Kimi K3.1 Pro 63.64% ($4.57, open weights),
  Gemini 4 Carbon 63.13% ($7.45, 12.5 min), Gemini 4 Neon 61.62%, GPT-6 Astra 59.60%.
  https://www.vals.ai/benchmarks/terminal-bench-4
- Official tbench.ai board (read 2026-11-07): Opus 5.5 64.8% ± 3.1% (Claude Code, max effort).
  https://www.developersdigest.tech/benchmarks/terminal-bench
- SWE-bench Pro commercial (private) set, Scale: on unseen code, scores drop a lot vs the public set
  (e.g. GPT-5.4 59.1% public vs 43.4% private). Shows contamination/overfitting risk in public benchmarks.
  https://www.morphllm.com/terminal-bench-2

## Aggregators (use with caution)
- geotoolbox (Nov 6): Opus 5.5 leads coding; Gemini 4 Argon leads Arena and Mercor APEX-Agents
  (82.4% vs 73.5%); GPT-6.1 Sol is the "value" pick. https://geotoolbox.ai/blog/best-ai-model
- benchlm agents ranking: Claude Fable 5.2 91.3, Gemini 4 Carbon 86.6, Claude Opus 5.5 84.2.
  https://benchlm.ai/best/agents
- Prices quoted (per 1M tokens in/out): Opus 5.5 $4/$20; GPT-6 Astra $10/$50; GPT-6.1 Sol about $1/$5;
  Gemini 4 Carbon $4/$20; Fable 5.2 $8/$40. https://aitoolsreview.co.uk/insights/best-ai-models ,
  https://letslearngenai.com/guide/benchmark
- Open weights: Kimi K3 (2.8T total / 104B active, July 2026) leads open tool-use benchmarks.
  GLM-5.2/5.3 (MIT, ~750B) are strong for long-horizon coding. DeepSeek V4.1 Flash is cheap.
  Qwen3.x 27B is the single-GPU option. https://www.morphllm.com/best-open-source-llm ,
  https://andrew.ooo/answers/best-open-weight-coding-model-2026-glm-deepseek-qwen-guide/

## Takeaways
1. At the top, the frontier models sit within a few points of each other on agent benchmarks,
   often within the error bars (±3).
2. Price and time per task differ much more than score (e.g. Kimi K3.1 Pro gets ~98% of Opus 5.5's
   Terminal-Bench 4.0 score at ~38% of the cost).
3. Vendor-reported numbers and unseen-data numbers can differ a lot, so you must run your own eval.
