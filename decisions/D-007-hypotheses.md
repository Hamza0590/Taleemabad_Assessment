# D-007 — Hypotheses for the prototype
Date: 2026-11-25
Status: DECIDED (H1); H2 PROPOSED

## H1 (main, user adopted it)
At a fixed review budget (20% of scripts re-checked by a human), risk-ranked review catches
more marking errors than random review.
- Measured as: % of planted marking errors caught (recall) at 20% budget, random vs ours.
- Also report the curve over budgets of 5–50%, not just one point (so we're not cherry-picking).

## H2 (user's extension: money)
The user's point: boards already spend real money on this review, likely millions of rupees a
year. If part of it goes into an audit system, the same spending gives better results.
Careful: H1's "budget" means HUMAN EFFORT (number of scripts reviewed), not money.
H2 is the money version:
- Cost of human review per script: ~Rs 30–50 (2023 Punjab and Multan rates).
- [ESTIMATE, to compute properly later] 20% of ~20M matric scripts = ~4M reviews/year,
  x ~Rs 35 = ~Rs 140M per year. Labelled as a rough estimate.
- Cost of our audit per script = GPU time measured in the prototype, plus hardware amortised.
- H2: the audit costs much less per script than one human review, so it pays for itself if it
  makes even a small share of review effort count.
Status: PROPOSED. We only claim it with our measured per-script compute cost.

## Rejected
- "AI accuracy vs examiner" as the main metric. REJECTED: the AI doesn't award marks, so its
  raw marking accuracy matters only through how well it ranks risk.
