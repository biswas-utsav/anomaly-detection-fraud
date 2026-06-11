# Anomaly Detection for Fraud and Sensor Data

## What This Project Is About ?

Credit card fraud is one of those problems that looks simple on the surfacebut gets really interesting once you start digging into the data. This notebook is my attempt at building a pipeline that can automatically flag suspicious transactions — without ever having seen a labeled fraud case during training.

The core idea: fraudulent transactions *behave* differently. They tend to happen far from home, involve unusually large amounts, and cluster with other recent 
transactions. The challenge is teaching a model to notice that — purely from the numbers.

## What I Did ?

I started with a synthetic dataset of 1000 credit card transactions (950 normal, 50 fraudulent) and worked through four different approaches to spot the outliers:

- Z-Score – flagged transactions where distance from home was statistically extreme (beyond 3 standard deviations)
- IQR Method – caught unusual transaction amounts using the interquartile range
- Isolation Forest – a tree-based ML model that isolates anomalies by how easily they get separated from the rest
- Local Outlier Factor (LOF) – a density-based approach that compares each point to its neighbors

## Results

| Method           | Precision | Recall |
|------------------|-----------|--------|
| Isolation Forest | 0.90      | 0.90   |
| LOF              | 0.34      | 0.34   |

Isolation Forest clearly outperformed LOF here. LOF struggled because the fraud points weren't isolated in clearly low-density regions — a good reminder that 
no single method works best in every situation.

## Tech Stack

- Python 3
- NumPy, Pandas
- SciPy
- Scikit-learn

## Key Takeaway

Statistical methods like Z-Score and IQR are fast and interpretable but only look at one feature at a time. Models like Isolation Forest consider all features 
together — and that makes a real difference when fraud patterns are spread across multiple dimensions.
