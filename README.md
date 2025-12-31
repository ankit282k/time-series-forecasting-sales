# time-series-forecasting-sales

## Overview
This project builds a **SKU-level demand forecasting system** using historical retail transaction data for the years **2009–10 and 2010–11**.  
The goal is to forecast future demand using only past demand patterns and evaluate the model using **RMSE**.

---

## Data Cleaning & Preprocessing

- Changed the format of `InvoiceDate` to standard datetime
- Removed the invoices starting with **C** as they are cancelled orders and I am forecasting for the demand only
- Cleaned invalid data like **negative prices** and **quantity less than or equal to 0**
- Removed SKUs having `StockCode` other than **5-digit numerical values**
- Combined the dataset of both years **2009–10 and 2010–11**
- Sorted the dataset based on **InvoiceDate**

---

## Data Aggregation (Daily Demand)

- Created a new dataframe having **total quantity of a particular SKU on a single date**
- Filled **0** for dates having no demand of the SKUs to maintain **time continuity**
- Filtered weak SKUs → **Removed SKUs having total demand < 50 units over two years**

This step ensures that each SKU has a continuous daily time series suitable for forecasting.

---

## Feature Engineering

- Added **Lag features** for past **1, 7, and 14 days** to understand previous demand patterns
- Added **Rolling Mean and Rolling Standard Deviation** to capture:
  - Short-term trend
  - Demand volatility
- Removed rows containing **NaN values** generated due to lag and rolling operations

---

## Train / Test Split

- Split the data **based on date**, not randomly, to avoid data leakage
- Used an **80–20 split** based on time
- Split date used: **01-07-2011**
- Defined:
  - Features → lag features, rolling features, calendar features
  - Target → daily demand quantity
- Chose **tree-based models (XGBoost)** as they work well with lag-based features and are computationally efficient

---

## Model Evaluation

- Evaluated the model using **RMSE (Root Mean Squared Error)**
- Achieved an RMSE of approximately **35**
- This means:
  - On average, the forecast is off by **~35 units per SKU per day**

### Baseline Comparison
- Baseline RMSE: **49.42**
- Model RMSE: **~35**
- This shows a **significant improvement over the baseline**

---

## Summary

- Built a complete end-to-end forecasting pipeline
- Handled real-world data issues like cancellations, invalid values, and inconsistent SKUs
- Used time-series aware feature engineering and splitting
- Trained and evaluated a robust ML-based forecasting model

---

## Tools & Libraries Used
- Python
- Pandas
- NumPy
- XGBoost
- Scikit-learn
