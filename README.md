# UNSW-NB15 Network Traffic Statistical Analysis

Statistical analysis of network intrusion data, applying descriptive
statistics and formal hypothesis testing to distinguish normal traffic from
attack traffic in the **UNSW-NB15** dataset — a benchmark dataset for network
intrusion detection research.

Academic project — Probability and Statistics (PRST2) module, 2025/2026.

## What this is

Two linked analyses on the same dataset:

1. **Descriptive statistics** — exploring the dataset's structure, class
   balance, attack categories, protocol distribution, and outliers.
2. **Hypothesis testing** — using formal statistical tests to check whether
   observed differences between normal and attack traffic are statistically
   significant, or could be due to chance.

## Dataset

- 82,332 network connections, 45 features, no missing values.
- Two classes: Normal (44.94%) and Attack (55.06%).
- 9 attack categories (dominated by Generic and Exploits).
- Source: [UNSW-NB15 dataset, UNSW Canberra Cyber](https://research.unsw.edu.au/projects/unsw-nb15-dataset)
  (also mirrored on [Kaggle](https://www.kaggle.com/datasets/mrwellsdavid/unsw-nb15)).
  The raw CSV is not included in this repo — download it from the link
  above and place it alongside the notebooks as `UNSW_NB15_testing-set.csv`
  to reproduce the analysis.

## Methods

For every hypothesis test, the same structure is followed: state **H0**
and **H1**, compute the test statistic, compare it to the critical value at
**α = 0.05**, and interpret the result.

Tests used:
- **Student t-test** (and its normal approximation for large samples) —
  comparing means
- **Fisher F-test** — comparing variances
- **Chi-squared goodness-of-fit** — checking whether a category is
  uniformly distributed
- **Chi-squared homogeneity** — comparing distributions across groups

## Key findings

- **Mean duration alone does not separate normal from attack traffic**
  (Z = 0.34, fails to reject H0) — both classes have heavy outliers.
- **Attack traffic has a much higher mean packet rate** than normal traffic
  (≈126,500 vs ≈28,350) — a statistically significant difference
  (Z = −104.38, reject H0).
- **Attack categories are far from uniformly distributed** — Generic and
  Exploits dominate (chi-squared goodness-of-fit, reject H0).
- **Protocol usage differs sharply between normal and attack traffic**:
  normal traffic is mostly TCP, while attacks lean heavily on UDP and
  "unassigned" protocols (chi-squared homogeneity, reject H0).
- Results were cross-checked on a random subsample (n = 200 per group)
  using the Student t(398) distribution — conclusions held.

## Contents

```
notebooks/
├── UNSW_NB15_Statistique_Descriptive_commented.ipynb   # exploration & visualization
└── UNSW_NB15_Hypothesis_Testing.ipynb                  # formal statistical tests
report/
└── UNSW_NB15_Hypothesis_Testing_Report.docx            # full written report
Oral_Presentation_Summary.md                             # presentation script
```

## Tools

Python — pandas, NumPy, Matplotlib, SciPy (`scipy.stats`).
