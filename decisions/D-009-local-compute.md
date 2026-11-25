# D-009 — Run models locally (no third-party AI APIs)
Date: 2026-11-25
Status: DECIDED (user)

## Why
- Student scripts are sensitive. A board couldn't send them to a foreign API.
- There are millions of scripts, so per-call API costs add up. Local cost is mostly fixed hardware (feeds H2).
- It matches the assessment's Q3 (in-house GPU).
## Consequence
The model must fit the available GPU memory, which means open-weight VLMs (exact model to be decided
in D-01x after a quick test). We measure seconds per script on the user's machine.
