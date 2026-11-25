# D-022 — Source correction: the "second examiner randomly reviews 20%" report was about BISE Peshawar, not FBISE
Date: 2026-11-25
Status: CORRECTED

## What was wrong
research/02, D-004/D-006 discussions and the Section 1 draft said FBISE's e-marking has three tiers
(first examiner marks, a second randomly reviews 20%, the head examiner intervenes), citing https://www.dawn.com/news/1731157.
When fetching the exact headline for the reference list, the article turned out to be:
"Peshawar education board to go for e-marking", Mohammad Ashfaq, Dawn, 12 January 2023. It is about BISE PESHAWAR.

## Also checked while fetching headlines
- https://www.dawn.com/news/1772170 = "FBISE receives applications for paper rechecking after over 38pc students fail
  part-I exam", Kashif Abbasi, Dawn, 26 Aug 2023. This is the FBISE source (about 10% of papers to the head examiner; a head
  examiner said their role became limited under e-marking).
- The 2/75 -> 61/75 rechecking case is from 30 January 2014 (Express Tribune, Kashif Abbasi). Now dated in the report.
- Dawn 1960947 = "Digitisation of all BISEs starts", 14 Dec 2025. TechJuice 197961 = "BISE Lahore to Introduce New Exam
  Re-Marking System", Sabica Tahira, 15 Oct 2025.

## Fix
- Report (LaTeX) and Section 1 md: separate rows for "E-marking (BISE Peshawar, 2023)" and "E-marking (FBISE)".
- research/02: corrected below.
- The argument doesn't change: Pakistani e-marking checks use RANDOM samples (Peshawar 20%, FBISE ~10%).
## Lesson
Verify every news source's headline before citing, not only the search snippet. Now done for all report references.
