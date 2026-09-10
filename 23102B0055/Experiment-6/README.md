# Experiment 6: Statistical Analysis of Physical Characteristics of Palmer Penguins

R programming lab on descriptive statistics, hypothesis testing, ANOVA, and non-parametric tests, applied to the Palmer Penguins dataset. Full objective, detailed description, output, and conclusion are documented in the report PDF — see `R_Prog_Experiment-6_23102B0055_Sneha_Gadhari.pdf`.

## Repository Contents
| File | Description |
|---|---|
| `R_Prog_Experiment-6_23102B0055.ipynb` | Colab notebook (R) with the complete code and output |
| `R_Prog_Experiment-6_23102B0055_Sneha_Gadhari.pdf` | Full report (Objective, Description, Output, Conclusion) |

## Dataset
[Palmer Penguins Dataset](https://raw.githubusercontent.com/allisonhorst/palmerpenguins/master/inst/extdata/penguins.csv) — loaded directly via URL inside the notebook, no manual download needed.

## How to Run
1. Open the notebook in Google Colab.
2. Runtime → Change runtime type → set Runtime type to **R**.
3. Run all cells top to bottom.

## Tech Stack
- R (Google Colab, R runtime)
- Packages: `dplyr`, `ggplot2`, `moments`, `car`

## Topics Covered
- Descriptive statistics (mean, median, variance, SD, IQR, skewness, kurtosis)
- Independent two-sample t-test, confidence interval, Cohen's d
- Shapiro-Wilk test, QQ-plots, Levene's test
- One-way & two-way ANOVA, Tukey HSD
- Kruskal-Wallis test
- Data visualization (histogram, boxplot, density plot)
