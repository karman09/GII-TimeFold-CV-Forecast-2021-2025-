# 🌍 Global Innovation Index (GII) Forecasting (2021-2025)

This project aims to forecast the **2025 Global Innovation Index (GII)** scores using a ** Nested Temporal Cross-Validation** approach. The methodology addresses the challenges of small sample sizes and time-series dependencies by strictly preventing data leakage and evaluating both short-term (Lag-1) and medium-term (Lag-2) impacts of socio-economic indicators.

* **📄 Dataset:** [FINAL_PREPROCESSED_DATA.xlsx](FINAL_PREPROCESSED_DATA.xlsx) (Click to view or download)
* **🚀 Run Analysis:** Click the "Open in Colab" badge above or [here](https://colab.research.google.com/drive/1OJJ5Q3m74OAgdgswThlvJpXPSVYm2lC8?usp=sharing)

## 🚀 Key Features & Methodology

### 1. Multi-Lag Analysis
The model iterates through **1-year (Lag-1)** and **2-year (Lag-2)** time delays to determine whether indicators have immediate or delayed effects on innovation scores. This allows for a comparative analysis of how different variables impact innovation over time.

### 2. True Nested Temporal CV with Expanding Window
Unlike standard K-Fold CV which shuffles data (causing data leakage in time series), we utilize an **Expanding Window (Anchored Walk-Forward) Validation** strategy. This strictly preserves temporal order.

#### 📅 Validation Scheme (Expanding Window):
The model is trained on past data and tested *strictly* on the future year, expanding the training set in each iteration:

| Fold | Training Years | Test Year |
| :--- | :--- | :--- |
| **Fold 1** | `[2021]` | `[2022]` |
| **Fold 2** | `[2021, 2022]` | `[2023]` |
| **Fold 3** | `[2021, 2022, 2023]` | `[2024]` |
| **FINAL** | `[2021, 2022, 2023, 2024]` | **Forecast 2025** |

### 3. Strict Feature Selection (Inside the Loop)
To prevent "look-ahead bias," feature selection is performed dynamically **inside each fold** using *only* that fold's training data.
1.  **High Correlation Filter:** Removes highly correlated features (>0.99).
2.  **LASSO (L1 Regularization):** Selects the most predictive sparse features.
3.  **Stepwise VIF (Variance Inflation Factor):** Removes multicollinearity (VIF > 10).

---

## 📂 Project Structure & Workflow

The analysis is executed through 4 sequential scripts:

### 1️⃣ Code 1: Preprocessing
* **Goal:** Cleans raw data, handles missing values, and standardizes country names.
* **Output:** `FINAL_PREPROCESSED_DATA.xlsx`

### 2️⃣ Code 2: Feature Selection (Multi-Lag Loop)
* **Goal:** Identifies the "Selected Features" for Lag-1 and Lag-2 scenarios separately using the full training set (2021-2024). This serves as the basis for the final model and thesis reporting.
* **Outputs:**
    * `FINAL_SELECTED_FEATURES_LAG1.xlsx`
    * `FINAL_SELECTED_FEATURES_LAG2.xlsx`

### 3️⃣ Code 3: True Nested CV & Final Prediction
* **Goal:** Performs the rigorous validation using the Expanding Window method and generates the final forecast for 2025.
* **Inner Loop:** Performs hyperparameter tuning (RandomizedSearchCV) for each model within each time fold.
* **Models Used:** XGBoost, LightGBM, RandomForest, AdaBoost.
* **Output:** `GII_2025_TRUE_NESTED_RESULTS.xlsx` (Contains R2, RMSE metrics, and 2025 Predictions).

### 4️⃣ Code 4: Process Reporting
* **Goal:** Generates a detailed audit table for the thesis, showing exactly which variable passed or failed at which stage (LASSO/VIF) for both Lag scenarios.
* **Output:** `FINAL_SUREC_TABLOSU.xlsx` (Contains separate sheets: `LAG_1_REPORT` and `LAG_2_REPORT`).

---

## 📊 Results & Outputs

The project produces comparative results for:
* **Lag 1 (Short-term impact):** How last year's data affects this year's GII.
* **Lag 2 (Medium-term impact):** How data from two years ago affects this year's GII.

The final Excel files provide a transparent view of selected features, model performance metrics (R2, RMSE, MAE), and the final **2025 GII Score Predictions**.

## 🛠️ Requirements

* Python 3.x
* pandas
* numpy
* scikit-learn
* xgboost
* lightgbm
* statsmodels
* openpyxl

---
*Author: [karman09](https://github.com/karman09)*
