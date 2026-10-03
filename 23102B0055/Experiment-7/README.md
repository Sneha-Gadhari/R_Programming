# Experiment 7: Customer Segmentation and Predictive Analytics Using Machine Learning

| | |
|---|---|
| **Student** | Sneha Gadhari |
| **Roll Number** | 23102B0055 |
| **Course** | B.E. Semester VII, Computer Engineering |
| **Subject** | R Programming |
| **Instructor** | Prof. Sanjeev Dwivedi |
| **Institute** | Vidyalankar Institute of Technology |
| **Language / Platform** | R on Google Colab |

## Objective

To segment e-commerce customers from the UCI Online Retail dataset and predict which customers belong to the high-value segment. Customer-level RFM and behavioural features are engineered and grouped using K-Means and Hierarchical Clustering, validated with the Silhouette Score and PCA, and then used to train Random Forest and SVM classifiers. The results are used to recommend targeted marketing strategies for each segment.

## Folder Contents

```
Experiment-7/
├── R_Prog_Exp_7_23102B0055.ipynb                         # Complete R notebook with outputs
├── R_Prog_Experiment-7_23102B0055_Sneha_Gadhari.pdf      # Lab report
└── README.md
```

## Dataset

- **Source:** [UCI Machine Learning Repository: Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail)
- **Size:** 541,909 transactions with Invoice Number, Stock Code, Description, Quantity, Invoice Date, Unit Price, Customer ID and Country.
- **Loading:** The notebook downloads the dataset directly from the UCI link, so no manual upload is needed.

## Workflow

1. **Data cleaning:** removed missing CustomerID, cancelled invoices, non-positive quantity or price, and duplicate rows (392,692 transactions and 4,338 customers remained).
2. **Feature engineering:** Recency, Frequency, Monetary, Average Transaction Value, Total Quantity, Purchase Frequency, Unique Products, Average Basket Quantity.
3. **Outlier treatment and scaling:** log transformation, IQR capping, standardisation.
4. **Clustering:** K-Means with the Elbow Method, and Hierarchical Clustering (Ward linkage) with a dendrogram.
5. **Validation:** Silhouette Score and Adjusted Rand Index.
6. **Dimensionality reduction:** PCA with 2D projection and interactive 3D Plotly visualisations.
7. **Customer profiling:** cluster-wise RFM profiles and segment naming.
8. **Prediction:** Random Forest and SVM (RBF) classifiers for high-value customers, with Accuracy, Precision, Recall, F1-Score, ROC-AUC, confusion matrices and feature importance.
9. **Recommendations:** targeted marketing strategies for each segment.

## Key Results

### Clustering

| Method | Silhouette Score |
|---|---|
| K-Means (k = 4) | 0.2672 |
| Hierarchical (Ward) | 0.2123 |

Adjusted Rand Index between the two methods: **0.5141**. PCA: the first two components explain **73.91%** of the variance.

### Customer Segments

| Cluster | Segment | Customers | Avg. Recency (days) | Avg. Frequency | Avg. Monetary | Revenue Share |
|---|---|---|---|---|---|---|
| 3 | Champions | 790 (18.21%) | 20.66 | 12.92 | 7,845.62 | 69.74% |
| 4 | Recent Low-Value | 1,322 (30.47%) | 51.13 | 3.75 | 1,236.75 | 18.40% |
| 2 | Dormant (mid-value) | 1,165 (26.86%) | 128.99 | 1.58 | 732.73 | 9.61% |
| 1 | Dormant (low-value) | 1,061 (24.46%) | 157.62 | 1.43 | 189.03 | 2.26% |

### Classification (High-Value = Champions)

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---|---|---|---|---|
| Random Forest | 0.9781 | 0.9664 | 0.9114 | 0.9381 | 0.9974 |
| SVM (RBF) | 0.9942 | 1.0000 | 0.9684 | 0.9839 | 0.9998 |

The SVM performed best. Monetary value, Total Quantity and Frequency were the strongest predictors in the Random Forest.

> **Note:** The high-value label was derived from the clusters built on the same features, so the high classification scores reflect cluster separability rather than independent predictive accuracy.

## Marketing Recommendations

- **Champions:** VIP loyalty tier, early access to new products, referral rewards, exclusive bundles.
- **Recent Low-Value:** onboarding emails, second-purchase discounts, free-shipping nudges, entry-level bundles.
- **Dormant segments:** low-cost reactivation emails and clearance offers; reduce paid campaign spend if unresponsive.

## How to Run

1. Open [Google Colab](https://colab.research.google.com/) and upload `R_Prog_Exp_7_23102B0055.ipynb` (File → Upload notebook).
2. Make sure the runtime is **R** (Runtime → Change runtime type → R).
3. Run all cells (Runtime → Run all). The first cell installs the required packages and may take several minutes.

### R Packages Used

`readxl`, `dplyr`, `tidyr`, `ggplot2`, `lubridate`, `cluster`, `randomForest`, `e1071`, `pROC`, `plotly`, `htmlwidgets`, `reshape2`

## Conclusion

RFM-based clustering separates customers into four meaningful segments. A small Champions group (18.21% of customers) accounts for nearly 70% of revenue. K-Means produced better-separated clusters than Hierarchical Clustering, and the SVM was the best classifier. The segment profiles give a practical basis for targeted marketing, retention and reactivation strategies.
