# D-028 — No video; a 14-slide deck instead
Date: 2026-11-26
Status: DECIDED (user: "we are not doing the video part")

## Decision
- Step 7 (video) is dropped. The form's video field is optional.
- Step 8: a 14-slide deck (Claude Slides). Because nobody presents it live, every slide must be readable on its own:
  a one-line claim as the title, the evidence under it, and the source in a footer.
- Order: story → scale → today's checks → Parakh → pipeline → test setup → reading bake-off → H1 → ablation →
  real errors → cost → limitation → summary + links.
- Look: navy and paper colours, with the examiner's red-pen colour as the only accent. EB Garamond for headings,
  Public Sans for text.

## Honesty choices (same as the report)
- The H1 headline is the 30-plan average (30.1%), not the single plan (53.8%). The 39.2% is labelled as a post-hoc ablation.
- "Rules only" scores highest (41.1%) but ranks the real Student_10 error last. Shown on the slide, not hidden.
- The 27% red-ink limitation gets its own slide, with a breakdown of what goes wrong.
- Cost is labelled as an estimate (D-021).

## Rejected
- PowerPoint file: not asked for. The deck can be exported as PDF/PPTX from the viewer if needed.
- Putting the full results tables on the slides: they are in the report and the Excel file. The slides carry one idea each.
