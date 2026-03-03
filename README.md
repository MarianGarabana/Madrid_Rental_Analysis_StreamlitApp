
# Madrid Rental Market — Interactive ML Dashboard

> A Streamlit application analyzing Madrid's rental housing market through machine learning.  
> Built for the Machine Learning I course · MBDS · IE University · 2026

**Live App:** [madridrentalapp-mariangarabana.streamlit.app](https://madridrentalapp-mariangarabana.streamlit.app/)

---

## Overview

This dashboard brings a full end-to-end machine learning pipeline to life using ~2,100 rental listings sourced from Idealista (Madrid). It covers everything from exploratory data analysis to unsupervised clustering, rent prediction, and binary classification — all interactive, all trained live from the raw data at startup.

---

## Features

| Page | Description |
|---|---|
| **Market Explorer** | Filter listings by district and rent range. View rent distributions, median rent by district, rent vs. size scatter plots, and a correlation heatmap. |
| **Property Segments** | Explore 5 K-Means clusters with radar charts and segment profiles. Enter a property's attributes to classify it into its market segment. |
| **Rent Predictor** | OLS linear regression with VIF filtering and RFECV feature selection. Predict monthly rent with a 95% prediction interval and see where it sits in the market distribution. |
| **High Rent Classifier** | Logistic regression with interactive ROC curve, confusion matrix, odds ratios, and a probability gauge. Classify any property as High Rent (≥ €1,800). |

---

## ML Pipeline

### Phase 0 — EDA & Cleaning
- 2,100 listings → 2,089 after cleaning
- Fixed floor outlier (data entry error > 100)
- Engineered features: `Is_Special`, `Price_per_sqm`, `SqMt_per_Bed`, `District_Premium`, `Zone`, `Is_Central`, `Is_Studio`, `High_Rent`

### Phase 1 — K-Means Clustering (k=5)
- Features: size, bedrooms, floor, exterior exposure, property type
- Validated with elbow method + silhouette score
- Segments: **Entry-Level Interior**, **High-Rise Exterior**, **Grand Estate**, **Standard Exterior Living**, **Urban Premium**

### Phase 2 — Association Analysis
- Apriori algorithm applied to property segments
- Evaluated by support, confidence, and lift (see notebook)

### Phase 3 — OLS Linear Regression
- VIF-based multicollinearity filtering (threshold = 10)
- RFECV feature selection (Repeated K-Fold, 5 splits × 3 repeats)
- Statsmodels OLS for p-values and 95% prediction intervals
- Target: monthly rent in €

### Phase 4 — Logistic Regression
- Same VIF pipeline + stratified train/test split
- Binary target: High Rent (≥ €1,800)
- Evaluated via AUC-ROC, confusion matrix, odds ratios, and threshold sensitivity

---

## Project Structure


