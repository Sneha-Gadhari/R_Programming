# Experiment 3 — Multi-Source Retail Sales Data Integration and Analysis

**Name:** Sneha Gadhari
**Roll No.:** 23102B0055
**Subject:** R Programming
**Platform:** R / Google Colab
**Domain:** Retail Analytics

> Full theory, objective, description, and conclusion are documented in
> [`R_Prog_Experiment-3_23102B0055_Sneha_Gadhari.pdf`](./R_Prog_Experiment-3_23102B0055_Sneha_Gadhari.pdf).

---

## Repository Contents

```
Experiment-3/
├── README.md                                          # This file
├── R_Prog_Exp-3_23102B0055.ipynb                       # Google Colab notebook (code + outputs)
├── R_Prog_Experiment-3_23102B0055_Sneha_Gadhari.pdf    # Theory document / notebook write-up
├── Online_Retail_raw.xlsx                              # Raw UCI Online Retail dataset (auto-downloaded)
├── transactions.csv                                    # Split source: InvoiceNo, StockCode, CustomerID, Quantity, InvoiceDate
├── products.json                                       # Split source: StockCode, Description, UnitPrice
├── customers.xlsx                                      # Split source: CustomerID, Country
└── retail_analysis.db                                  # SQLite database with the final cleaned/integrated `retail_sales` table
```

## Dataset

**Source:** Chen, D. (2015). *Online Retail* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33

The raw dataset is downloaded automatically inside the notebook — no manual download is required. It is then split into three source files (`transactions.csv`, `products.json`, `customers.xlsx`) to simulate a multi-system retail environment before the cleaning and integration steps begin.

## Tech Stack

`readr` · `jsonlite` · `readxl` · `writexl` · `dplyr` · `tidyr` · `lubridate` · `DBI` · `RSQLite` · `stringr`

## How to Run

1. Open `R_Prog_Exp-3_23102B0055.ipynb` in Google Colab.
2. Set the runtime to **R** (Runtime → Change runtime type → R).
3. Run all cells top to bottom — the dataset is fetched automatically and all outputs (including `retail_analysis.db`) are regenerated in place.

## Skills Demonstrated

CSV/JSON/Excel import · data cleaning & preprocessing · missing-value handling · `dplyr` manipulation · `left_join()` / `inner_join()` · `group_by()` / `summarise()` · `case_when()` · SQLite connectivity & SQL querying · business analytics and critical interpretation.
