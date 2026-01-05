# 📈 Retail SKU Demand Prediction

## 📌 Overview
This project implements an **end-to-end demand forecasting system** to predict **SKU-level daily demand** for a retail store over a **21-day future horizon**.  
The solution uses **classical machine learning / statistical techniques**, applies standard **time-series feature engineering**, and evaluates performance using **RMSE**.

---

## 📂 Dataset
The dataset contains **transaction-level retail sales data** for the financial years **2009–10 and 2010–11**.

### Column Description
- **InvoiceNo**: 6-digit invoice number (starting with `C` indicates cancellation)
- **StockCode**: 5-digit SKU identifier
- **Description**: Product name
- **Quantity**: Quantity purchased per transaction
- **InvoiceDate**: Date and time of transaction
- **UnitPrice**: Price per unit (GBP)
- **CustomerID**: 5-digit customer identifier
- **Country**: Customer’s country

---

## 🎯 Objective
- Forecast **daily demand at SKU level**
- Predict demand for the **next 21 days**
- Apply **time-series feature engineering**
- Split data into **train / validation / test**
- Evaluate accuracy using **RMSE**
- Export forecasts as a **SKU × Day matrix (CSV)**

---

## 🧠 Methodology

### 1️⃣ Data Cleaning & Preprocessing
- Converted `InvoiceDate` to datetime format
- Removed cancelled transactions (`InvoiceNo` starting with `C`)
- Removed invalid records (negative quantity or price)
- Filtered valid 5-digit SKUs
- Aggregated transaction data to **daily SKU-level demand**
- Filled missing dates with zero demand to ensure time continuity
- Removed weak SKUs with very low overall demand

---

### 2️⃣ Feature Engineering
- Lag features (e.g., 1, 7, 14 days)
- Rolling statistics to capture short-term trends
- Time-based features to capture seasonality

---

### 3️⃣ Model Training & Forecasting
- Used a classical ML / statistical forecasting model
- Performed **time-aware splitting** into:
  - Training set
  - Validation set
  - Test set
- Forecasted demand **iteratively for a 21-day horizon**

---

### 4️⃣ Evaluation
- Evaluated model performance using **Root Mean Squared Error (RMSE)**
- RMSE calculated on the test dataset
- Results analyzed at SKU level

---

### 5️⃣ Output
- Forecasts generated for **21 future days**
- Output stored as a **CSV file** in the following format:

| SKU | Day_1 | Day_2 | ... | Day_21 |
|-----|-------|-------|-----|--------|
| 12345 | 10 | 12 | ... | 15 |

Each value represents the **forecasted quantity** for the SKU on that day.

---

## 🛠 Tools & Technologies
- Python
- Pandas, NumPy
- Scikit-learn / classical ML models
- Matplotlib / Seaborn
- Jupyter Notebook
