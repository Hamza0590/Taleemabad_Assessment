# D-021 — How the cost per script (H2) was calculated
Date: 2026-11-25
Status: DECIDED. This is an ESTIMATE, built from one measured number and several assumptions listed below.
Code: prototype/marking_audit_v2_run.ipynb, section 17 (all assumptions are variables at the top of that cell).

## 1. Measured
- Time to read one script with the chosen pipeline (C + qwen3-vl:8b-instruct): MEDIAN = 48 seconds
  over the 50 scripts, on one NVIDIA RTX 5060 Ti 16 GB, Ollama, one request at a time.
- Median, not mean, because the first 3 scripts were distorted (one from cache, two during the slow-run incident, D-017).
  The mean was 60 s.
- 48 s = 48 / 3600 = 0.01333 hours per script.
- Not included in the 48 s: the AI second-reader calls (section 12) were not timed separately. They're short
  text-only calls, but they add some time. Limitation.

## 2. Assumptions (not measured)
| Assumption | Value | Why this value |
|---|---|---|
| GPU power draw while running | 180 W | = the card's MAXIMUM power limit (nvidia-smi shows a 180 W cap), so this is a deliberately HIGH (conservative) figure. A reading during a different full-load job (training, 100% GPU use) showed 119 W. Real draw during our inference was NOT measured |
| Electricity price | Rs 60 per kWh | Rough Pakistani commercial tariff. Change it to the real tariff |
| Workstation price | Rs 450,000 | Rough price of a PC with this GPU |
| Workstation lifetime | 3 years x 365 days x 8 hours = 8,760 working hours | Simple straight-line depreciation over a working day |
| Human re-check cost per script | Rs 35 | Punjab 2023 pay revision: Rs 35/paper for matric examiners marking fewer than 50 papers (Rs 45 for more than 50). Used as a stand-in for the cost of one human re-checking one script. Rates may have changed since 2023 |

## 3. Calculation
- Electricity per script = 0.18 kW x 0.01333 h x Rs 60/kWh = Rs 0.14
- Hardware per script = (Rs 450,000 / 8,760 h) x 0.01333 h = Rs 51.4/h x 0.01333 h = Rs 0.69
- Audit cost per script = 0.14 + 0.69 = Rs 0.83
- Scripts per GPU per 8-hour day = 8 x 3600 / 48 = 600

## 4. How to read the comparison (important)
- Rs 0.83 (machine audit of one script) vs Rs 35 (human re-check of one script).
- The audit does NOT replace the human re-check. It decides WHICH scripts humans re-check.
- So the fair statement is: auditing EVERY script by machine costs about the same as a human re-checking
  about 2–3 out of every 100 scripts (0.83 / 35 = 2.4%).

## 5. Not included (would make the real cost higher)
- Scanning scripts (boards already scan them for e-marking, so we treat it as existing cost)
- Storage, backups, networking
- Staff to run and maintain the system, software development, model updates
- Time of the AI second-reader calls (not timed separately)
- Data-centre hardware at state scale has a different cost per script: higher price per GPU, but much faster
  with batched serving. Not estimated here.

## 6. Options considered
- Mean time (60 s) vs median (48 s): CHOSE median, because the slow-run incident distorted the mean (D-017).
  With the mean, cost = Rs 1.04 per script (same conclusion).
- Cloud-API price comparison: REJECTED, because the design is local-only (D-009).

## 7. Power check (2026-11-25, nvidia-smi)
- Power cap of the RTX 5060 Ti: 180 W. Our assumption uses the full cap, so it overestimates the electricity cost.
- Reading taken while the GPU ran a DIFFERENT job (model training, 100% utilisation): 119 W.
  Not our workload, so not used in the calculation. It only shows real draw is likely below the cap.
- With 119 W the electricity share would be Rs 0.10 instead of Rs 0.14, so the total is about Rs 0.79 instead of Rs 0.83.
  The conclusion doesn't change, because hardware wear (Rs 0.69) dominates the cost.
- To do properly: run nvidia-smi during section 11 (our own reading run) and use that number.
