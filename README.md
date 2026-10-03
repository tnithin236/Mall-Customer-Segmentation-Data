# Mall Customer Segmentation using K-Means Clustering

An unsupervised machine learning project that groups mall customers into meaningful segments based on their **annual income** and **spending behaviour**, so the business can target each group with the right marketing strategy.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-K--Means-orange)
![Status](https://img.shields.io/badge/status-complete-brightgreen)

---

## Table of Contents
- [Problem Statement](#problem-statement)
- [Dataset](#dataset)
- [Approach](#approach)
- [Customer Segments](#customer-segments)
- [Key Decisions](#key-decisions)
- [Bonus Work](#bonus-work)
- [Limitations](#limitations)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)

---

## Problem Statement
A mall wants to understand its customers better. With no predefined labels, the goal is to **discover natural groups** of customers so that promotions, loyalty programs and store offers can be tailored to each group instead of treating everyone the same.

## Dataset
| Item | Details |
|---|---|
| Source | [Kaggle: Customer Segmentation Tutorial in Python (vjchoudhary7)](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python) |
| Size | 200 rows, 5 columns |
| Columns | `CustomerID`, `Gender`, `Age`, `Annual Income (k$)`, `Spending Score (1-100)` |
| Target | None (unsupervised learning) |

> The CSV is not redistributed here if you prefer to download it yourself from Kaggle. Place `Mall_Customers.csv` in the project root before running the notebook.

## Approach
1. **Data exploration:** shape, data types, missing values, summary statistics, distributions of Age, Income and Spending Score, and an Income vs. Spending scatter plot.
2. **Preprocessing:** dropped `CustomerID`; excluded `Gender` from the main model (justified below); selected Annual Income and Spending Score as clustering features.
3. **Feature scaling:** applied `StandardScaler`, because K-Means is distance-based and features on larger scales would otherwise dominate.
4. **Choosing K:** compared the **Elbow Method** (inertia) with the **Silhouette Score** for K = 1 to 10.
5. **Model training:** trained the final K-Means model, added cluster labels to the dataframe, and checked stability across random seeds, `init` methods and `n_init` values (Adjusted Rand Index).
6. **Visualisation and profiling:** cluster scatter plot with centroids marked, plus average Age, Income and Spending per cluster, with a business label for each segment.
7. **Conclusion:** summary of segments, K selection, scaling approach and limitations.

## Customer Segments
Five segments emerge from the income and spending patterns:

| Segment | Profile | Suggested Action |
|---|---|---|
| **High income, high spenders** | Premium, highly engaged customers | VIP programs, early access, loyalty rewards |
| **High income, low spenders** | Wealthy but under-engaged; untapped potential | Targeted premium offers, better product matching |
| **Low income, high spenders** | Enthusiastic, trend-driven shoppers | Trend promotions, installment or credit offers |
| **Low income, low spenders** | Budget-conscious, low engagement | Low-cost discounts only |
| **Average income, average spenders** | Largest, "typical" customer group | General promotions, upsell to higher tiers |

*Exact cluster sizes, averages and plots are in the notebook.*

## Key Decisions
- **K = 5:** the elbow curve flattens after K = 5 and the silhouette score peaks there, so both methods support it. It also matches the five visible groups in the raw scatter plot.
- **Scaling with `StandardScaler`:** K-Means uses Euclidean distance, so every feature must be on a comparable scale.
- **Gender excluded from the main model:** it is binary, and after scaling it can dominate distances and split clusters by gender rather than behaviour. Male and female averages for income and spending are also very similar.
- **Stability checks:** results were consistent across different seeds, `init` settings and `n_init` values.

## Bonus Work
- **K-Means from scratch (NumPy only):** random centroid initialisation, assignment step, update step and convergence check. Its cluster assignments were compared with scikit-learn's output using the Adjusted Rand Index.
- **4-feature clustering:** repeated the analysis with Age, Income, Spending Score and encoded Gender, then compared the segments with the 2-feature result. Including Age and Gender makes the groups overlap more in the income-spending plane, so the 2-feature segments are cleaner and easier to act on.

## Limitations
- K must be chosen in advance, and the elbow is somewhat subjective.
- K-Means assumes roughly spherical, similar-sized clusters.
- Centroids are means, so the algorithm is sensitive to outliers.
- With only 200 customers and two behavioural features, segments are a starting point, not a complete customer picture.

## Getting Started

**1. Clone the repository**
```bash
git clone https://github.com/tnithin236/Mall-Customer-Segmentation-Data.git
cd Mall-Customer-Segmentation-Data
```

**2. Install dependencies**
```bash
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
```

**3. Add the dataset**
Download `Mall_Customers.csv` from the [Kaggle link](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python) and place it in the project root.

**4. Run the notebook**
```bash
jupyter notebook Mall_Customer_Segmentation_KMeans.ipynb
```

## Project Structure
```
Mall-Customer-Segmentation-Data/
├── Mall_Customer_Segmentation_KMeans.ipynb   # Full analysis, plots and written summary
├── Mall_Customers.csv                        # Dataset (from Kaggle)
├── README.md
└── .gitignore
```

## Tech Stack
Python, NumPy, pandas, Matplotlib, Seaborn, scikit-learn, Jupyter Notebook

---

*Project completed as part of the QSpiders data analytics training.*
