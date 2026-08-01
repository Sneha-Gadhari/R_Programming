# R Programming – Experiment 1: Air-Quality Data Cleaning Using R

**Student Name:** Sneha Gadhari
**Roll Number:** 23102B0055
**Semester:** B.E. Semester VII – Computer Engineering
**Subject:** R Programming
**Subject Professor In-charge:** Prof. Sanjeev Dwivedi
**Experiment Number:** 01
**Experiment Title:** Air-Quality Data Cleaning Using R: Management of NA, NULL, and NaN Values

---

## Objective

An environmental monitoring agency collects hourly air-quality and weather readings from multiple monitoring stations. Due to sensor failures, temporary network interruptions, equipment maintenance, and data-entry errors, several pollutant and weather readings are unavailable or invalid. Before this data can be used for pollution analysis, it must be cleaned and validated.

This experiment develops an R program that can:
- Identify missing and undefined values (`NA`, `NULL`, `NaN`)
- Differentiate between these three types of missing/undefined data
- Summarize missing values across selected variables
- Replace missing numerical values using suitable statistical methods
- Replace missing categorical values appropriately
- Handle errors gracefully without terminating the program
- Export a cleaned dataset for further analysis

## Dataset

**Source:** [Beijing Multi-Site Air-Quality Data Set](https://archive.ics.uci.edu/dataset/501/beijing+multi+site+air+quality+data) – UCI Machine Learning Repository

**File used:** `PRSA_Data_Aotizhongxin_20130301-20170228.csv` (Aotizhongxin monitoring station)

**Size:** 35,064 hourly observations across 18 variables, including PM2.5, PM10, SO2, NO2, CO, O3, TEMP, PRES, DEWP, RAIN, `wd` (wind direction), and WSPM.

## Tasks Performed

1. **Import and Inspect the Dataset** – Loaded the CSV with error handling via `tryCatch()`; displayed the first six rows, structure, dimensions, and total missing-value count.
2. **Understand NA, NULL, and NaN** – Demonstrated each with standalone examples and `is.na()`, `is.null()`, `is.nan()`.
3. **Missing-Value Summary Function** – Built `summarize_missing()` to report total records, missing count, and missing percentage per variable, with a warning for any variable exceeding 20% missing.
4. **Identify Invalid Numerical Results** – Computed `aqi_ratio` (PM2.5/PM10), checked for `NA`, `NaN`, and `Inf`, and replaced invalid results with `NA`.
5. **Handle Missing Numerical Values Using a Loop** – Imputed missing values in PM2.5, PM10, SO2, NO2, TEMP, and WSPM using the median, inside a single reusable loop.
6. **Handle Missing Categorical Values** – Built `get_mode_value()` to compute the mode of `wd` and used it to fill missing wind-direction entries.
7. **Implement Error Handling** – Built `safe_clean_column()`, using `tryCatch()` to gracefully handle non-existent columns, non-numeric columns, and all-missing columns.
8. **Compare Missing Values Before and After Cleaning** – Produced a comparison table showing missing counts before/after cleaning and values replaced per variable.
9. **Visualization** – Generated a grouped bar chart comparing missing-value counts before and after cleaning.
10. **Export the Cleaned Dataset** – Exported the cleaned data frame to `cleaned_beijing_air_quality.csv`.

## Key Results

- All selected variables (PM2.5, PM10, SO2, NO2, TEMP, WSPM, wd) had missing percentages under 3%, well below the 20% warning threshold.
- A total of 3,716 missing values across the seven tracked variables were fully resolved after cleaning.
- Numeric columns were imputed using their column-wise medians; the categorical `wd` column was imputed using its mode ("NE").
- Error handling correctly rejected a categorical column and a nonexistent column when passed to the numeric-cleaning function, without stopping program execution.

## Repository Contents

| File | Description |
|---|---|
| `RProg_Experiment_1.ipynb` | R notebook containing the full solution (all 10 tasks) |
| `cleaned_beijing_air_quality.csv` | Cleaned dataset exported after missing-value treatment |
| `R_Prog_Experiment-1_23102B0055_Sneha_Gadhari.pdf` | Experiment write-up / lab record |
| `README.md` | This file |

## Tools Used

- **Language:** R
- **Environment:** Google Colab (R runtime)
- **Key functions/packages:** base R (`tryCatch`, `median`, `table`, `barplot`, `write.csv`)

## Learning Outcomes

- Differentiated between `NA`, `NULL`, and `NaN` in R.
- Identified and summarized missing values using custom functions.
- Applied loops to process multiple variables without repetitive code.
- Handled both numerical and categorical missing data.
- Implemented robust error handling using `tryCatch()`.
- Generated visualizations and exported a cleaned, analysis-ready dataset.
