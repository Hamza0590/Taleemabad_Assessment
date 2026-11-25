# Data

The dataset is not stored in this repository. Download it from:

**K. P. Dinesh (2026).** *A Dataset of Digitized Student Examination Papers, Answer Keys, and Manual Evaluations for
Automated Grading Research.* Mendeley Data, V1. DOI: [10.17632/sf3kvjwknt.1](https://doi.org/10.17632/sf3kvjwknt.1). License: CC BY 4.0.

Unzip it here, so that the folder looks like this:

```
data/
  A Dataset of Digitized Student Examination Papers,/
    Corrected_Pdf/                          <- marked scripts (input to Parakh)
    Student_Pdf/
    Teacher_manual_marks_Anonymized.csv
    answerkey.txt
    Question.txt
  baseline_fixes.csv                        <- ours (in the repo)
```

`Student_MCQ.csv` and `file.txt` from the dataset are **never used**. They appear to contain real student names and IDs.

`baseline_fixes.csv` lists the 3 issues we verified by eye in the original teacher records. They are used only in the
real-world pilot (notebook section 16):

| student | issue |
|---|---|
| Student_10 | correct MCQ answers (13, 14, 16, 17, 18, 19) crossed out: about 6 marks lost |
| Student_11 | Q34 counted twice across two pages (4 out of a maximum of 2) |
| all | the teacher accepted D for Q1. The published key says B, and we follow the key. |
