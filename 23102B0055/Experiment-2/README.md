# Experiment-2: Control Flow, Functions & Missing Data Handling in R

**R Programming Lab | Module 1 & 2**

This repository contains two R programming laboratory experiments focused on data cleaning, control flow, custom functions, error handling, and missing-data treatment — applied to real-world healthcare and demographic datasets.

---

## Folder Structure

```
Experiment-2/
├── R_Prog_Exp_2a.ipynb                                  # Lab 3: Control Flow for Data Cleaning
├── R_Prog_Exp_2b.ipynb                                  # Lab 4: Advanced Missing Data Handling
├── cleaned_heart_data.csv                                # Output dataset from Lab 3
├── cleaned_adult_data.csv                                # Output dataset from Lab 4
├── R_Prog_Experiment-2_23102B0055_Sneha_Gadhari.pdf      # Colab notebook export (combined report)
└── README.md
```

| File | Description |
|---|---|
| `R_Prog_Exp_2a.ipynb` | Lab 3 — Control Flow for Data Cleaning (UCI Heart Disease dataset) |
| `R_Prog_Exp_2b.ipynb` | Lab 4 — Advanced Missing Data Handling (UCI Adult/Census Income dataset) |
| `cleaned_heart_data.csv` | Cleaned & validated output from Lab 3 |
| `cleaned_adult_data.csv` | Cleaned & validated output from Lab 4 |
| `R_Prog_Experiment-2_23102B0055_Sneha_Gadhari.pdf` | Exported PDF of both notebooks for submission |

---

## Objective

To apply core R programming concepts — conditional logic, custom functions, loop-based vs. vectorized processing, exception handling with `tryCatch()`, and systematic missing-data detection and imputation — in order to clean, validate, and prepare two real-world datasets (UCI Heart Disease and UCI Adult/Census Income) for downstream statistical analysis.

---

## Description

This experiment consists of two connected R programming labs that together simulate the real-world data-cleaning workflow used by data analysts before any statistical modeling can begin. Both labs work with authentic, messy healthcare and demographic datasets, and both require the data to first be *deliberately corrupted* — injecting negative values, missing values, extreme outliers, blank strings, and impossible entries — so that the detection and treatment logic can be tested against known, controlled problems rather than hoped-for ones.

**Lab 3 — Control Flow for Data Cleaning** (`R_Prog_Exp_2a.ipynb`) uses the UCI Heart Disease dataset, focusing on the `trestbps` (resting blood pressure) variable. It builds a complete cleaning pipeline for a single numeric variable and layers in performance analysis:

- A custom `if-else` based function classifies each BP reading as negative (→ converted to `NA`), extreme (→ capped at 250 mmHg), or valid (→ left unchanged).
- `tryCatch()` wraps two operations that can fail in practice: computing a mean BP when values are missing, and computing a `chol / trestbps` ratio where the denominator might be zero, `NA`, or otherwise invalid — both return informative messages instead of crashing the script.
- The same outlier-detection logic is implemented twice — once with an explicit `for` loop, once with vectorized R operations — and their runtimes are benchmarked with `system.time()` and `microbenchmark()` to make the performance gap concrete rather than theoretical.
- The cleaned column is validated (missing count, min/max/mean/median, and confirmation that no negative or >250 values remain) and exported as `cleaned_heart_data.csv`.

**Lab 4 — Advanced Missing Data Handling** (`R_Prog_Exp_2b.ipynb`) uses the UCI Adult/Census Income dataset and broadens the scope from one numeric variable to a full mixed-type dataset (numeric + categorical). Its emphasis is conceptual precision as much as mechanics:

- It distinguishes four related but distinct ideas that are frequently confused: `NA` (a missing value inside a vector), `NaN` (an undefined numeric result, technically a subtype of `NA`), `NULL` (the absence of an R object entirely, which cannot literally occupy a data-frame cell), and `""` (a blank string — a valid-looking value that is semantically missing).
- Detection uses `is.na()`, `is.nan()`, `is.null()`, direct string comparison for blanks, a logical check for impossible values (`age == 999`), and `naniar::miss_var_summary()` for a variable-by-variable missingness report.
- Treatment converts impossible values to `NA`, replaces blank/missing categorical entries with `"Unknown"`, median-imputes numeric gaps (via a reusable custom function), and drops rows with unrecoverable `NaN` — with `complete.cases()` used to track fully complete vs. incomplete observations throughout.
- Missingness is quantified and visualized (via `naniar::gg_miss_var()`) both before and after treatment, and the final dataset is validated with `skimr::skim()` before being exported as `cleaned_adult_data.csv`.

Across both labs, the underlying skill being exercised is the same: recognizing that raw data cannot be trusted, building reusable and defensive functions to detect and fix specific classes of problems, and proving — through validation checks, timing benchmarks, and missingness reports — that the cleaning actually worked rather than just assuming it did.

---

## Tech Stack

- **Language:** R (run via Google Colab R runtime)
- **Packages:** `microbenchmark`, `naniar`, `skimr`, `dplyr`
- **Datasets:** [UCI Heart Disease Dataset](https://archive.ics.uci.edu/dataset/45/heart+disease), [UCI Adult/Census Income Dataset](https://archive.ics.uci.edu/dataset/2/adult)

---

## How to Run

1. Open `R_Prog_Exp_2a.ipynb` or `R_Prog_Exp_2b.ipynb` in [Google Colab](https://colab.research.google.com).
2. Go to `Runtime > Change runtime type` and set **Runtime type = R**.
3. Run all cells (`Runtime > Run all`). Required packages install automatically on first run.
4. Each notebook exports its cleaned dataset as a `.csv` in the working directory.

---

## Conclusion

Together, the two labs demonstrate that robust data cleaning in R depends on combining precise conditional logic, reusable functions, and proper exception handling with vectorized operations for efficiency — and that correctly distinguishing between `NA`, `NaN`, `NULL`, and `""` is essential, since treating them interchangeably would silently produce incorrect or incomplete cleaning. The resulting pipelines produced two validated, analysis-ready datasets (`cleaned_heart_data.csv` and `cleaned_adult_data.csv`), confirming that a structured, checkable cleaning process is a prerequisite for reliable downstream statistical or machine learning work.

---

## Author

**Sneha Gadhari**
Roll No: 23102B0055
