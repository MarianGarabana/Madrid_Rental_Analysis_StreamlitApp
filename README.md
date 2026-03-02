# 🏠 Madrid Rental Market – Streamlit Application

Interactive data science application for exploring, segmenting, and modeling the Madrid rental market.

This project integrates exploratory data analysis, clustering, regression, and classification into a single end-to-end Streamlit dashboard.

---

# 📌 Project Overview

The application is structured into four analytical modules:

1. 🔍 Market Explorer  
2. 🏘️ Property Segments (Clustering)  
3. 💶 Rent Predictor (Regression)  
4. 📊 High Rent Classifier (Classification)  

All models are trained at startup and cached for performance optimization.

---

# 📂 Dataset

**File:** `Houses for rent in Madrid.xlsx`

The dataset contains rental listings with features such as:

- Rent (€)
- Square meters (`Sq.Mt`)
- Bedrooms
- Floor
- District
- Elevator
- Exterior-facing indicator
- Property type flags (Penthouse, Duplex, Cottage, etc.)

---

# 🧹 Data Cleaning & Feature Engineering

## Cleaning Steps

- Dropped column with high missing values (`Number`)
- Removed rows with missing `Area`
- Corrected floor outliers (>100)
- Imputed missing values (median or mode depending on variable)

## Engineered Features

- `Is_Special` → Combines rare property types
- `Price_per_sqm` → Descriptive metric (not used in models)
- `SqMt_per_Bed` → Spaciousness proxy
- `District_Premium` → Median district rent mapping
- `Zone` → Geographic grouping
- `Is_Central` → Prime/central district indicator
- `Is_Studio` → Studio listing indicator
- `High_Rent` → Binary target (Rent ≥ €1,800)

---

# 🔍 1. Market Explorer

Interactive filters:
- Rent range
- District selection

Displays:
- Key summary metrics
- Rent distribution histogram
- Median rent by district
- Rent vs size scatter plot
- Correlation heatmap
- Filtered dataset table

Purpose:  
Understand structure, distribution, and pricing dynamics of the Madrid rental market.

---

# 🏘️ 2. Property Segments (K-Means Clustering)

## Model

- Algorithm: K-Means
- k = 5
- StandardScaler preprocessing
- Features:
  - Sq.Mt
  - Bedrooms
  - Floor
  - Is_Special
  - Outer

## Identified Segments

1. Entry-Level Interior  
2. High-Rise Exterior  
3. Grand Estate  
4. Standard Exterior Living  
5. Urban Premium  

The app provides:
- Segment summary table
- Visual comparisons
- Interactive property classification tool

Purpose:  
Identify structural sub-markets within Madrid rentals.

---

# 💶 3. Rent Predictor (Linear Regression)

## Pipeline

1. Train/Test split (80/20)
2. Multicollinearity removal via VIF
3. Feature selection using RFECV
4. Final model: Statsmodels OLS
5. Test evaluation

## Metrics Displayed

- R² (test)
- RMSE
- MAE
- Actual vs Predicted visualization
- Feature effect visualization
- 95% prediction interval for new inputs

## Input Features

- Sq.Mt
- Bedrooms
- Floor
- Exterior
- Elevator
- Is_Special
- Is_Central
- Is_Studio

Purpose:  
Estimate expected monthly rent and interpret key price drivers.

---

# 📊 4. High Rent Classifier (Logistic Regression)

## Target

`High_Rent = 1` if Rent ≥ €1,800

## Pipeline

- Stratified train/test split
- VIF-based feature refinement
- Statsmodels Logistic Regression
- ROC evaluation

## Metrics Displayed

- Accuracy
- AUC (test)
- AUC gap (overfitting check)
- ROC curves
- Confusion matrix
- Odds ratios table
- Threshold sensitivity analysis

## Interactive Prediction

Outputs:
- High/Low classification
- Probability score
- Gauge visualization

Purpose:  
Estimate probability that a property belongs to the premium rental segment.

---

# ⚙️ Tech Stack

- Python
- Streamlit
- Pandas
- NumPy
- Scikit-learn
- Statsmodels
- Plotly
- OpenPyXL (Excel support)

---

# 🚀 Installation & Usage

## 1. Clone Repository

```bash
git clone <your-repo-url>
cd <your-project-folder>
```

## 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### Required Libraries

```
streamlit
pandas
numpy
plotly
scikit-learn
statsmodels
openpyxl
```

## 3. Place Dataset

Ensure the dataset is located at:

```
data/Houses for rent in Madrid.xlsx
```

## 4. Run the Application

```bash
streamlit run madrid_rental_app.py
```

---

# 🧠 Modeling Design Decisions

- Multicollinearity handled using iterative VIF removal.
- Feature selection performed via RFECV cross-validation.
- OLS chosen for interpretability (p-values, confidence intervals).
- Logistic regression used for probabilistic classification.
- Clustering validated during development using elbow and silhouette methods.

---

# 📈 Project Highlights

- End-to-end data science workflow
- Structured feature engineering
- Unsupervised market segmentation
- Interpretable econometric modeling
- Probabilistic classification
- Interactive deployment with Streamlit
