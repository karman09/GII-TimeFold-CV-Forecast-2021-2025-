
# 🌍 GII TimeFold CV Forecast (2021–2025) 
## Bu proje, Global Innovation Index (GII) tahmini için tasarlanmış, sızıntısız, zamana duyarlı, gerçekçi ve tekrarlanabilir bir makine öğrenimi pipeline’ıdır.Pipeline, yıllar arası bilgi sızıntısını ortadan kaldıran Time-Fold Cross-Validation yapısını kullanır.
##  Veri Seti

## 📘 Colab Notebook

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/10FsgY2jjHbj90VDW4izMx3b2lJ5aFJd3?usp=drive_link)


### 📂 Veri Seti
[FINAL_PREPROCESSED_DATA.xlsx](data/FINAL_PREPROCESSED_DATA.xlsx)


# 🧭 1. Proje Özeti

## Bu proje yıllık veriler üzerinde gelecek yılı tahmin etmek üzere tasarlanmış bir zaman-serisi odaklı ML yapısıdır. Pipeline; veri temizleme, özellik seçimi, zaman tabanlı validasyon, çoklu model eğitimi ve nihai forecast adımlarını eksiksiz uygular.

### Kullanılan ana bileşenler:

#### 🛡 Zero-Leakage Training

#### ⏳ Time-Based Fold Cross-Validation (Train genişler → Test = 1 yıl sonrası)

#### 🔍 Modified Z-Score Outlier Detection

#### 🩺 Median + KNN Imputation (train-only)

####  📏 Train-Only StandardScaler

#### 🧬 LASSO Feature Selection (LassoCV)

####  🔁 Iterative VIF Filtering

#### 🤖 ML Modelleri: XGBoost, LightGBM, RandomForest, AdaBoost

#### 🎯 Son yıl (2025) için final forecast

# 🤖 3. Model Eğitimi

## Pipeline; dört farklı regresyon modeliyle eğitilir.

### ⚡ XGBoost Regressor

Gradient boosting

Yüksek doğruluk

Hızlı ve verimli

### 💡 LightGBM Regressor

Büyük veri için ideal

Hızlı ve memory-efficient

### 🌲 RandomForest Regressor

Non-linear ilişkilerde güçlü

Stabil ve sağlam modeller üretir

### 🔺 AdaBoost Regressor

DecisionTree tabanlı

Weak learner → güçlü modele dönüşüm

Bias yüksekse özellikle etkili

## Tüm modeller için şu metrikler hesaplanır:

### Train R², Test R², RMSE, MAE, MAPE (%), Time-Fold CV R² (Mean & Std), Model çalışma süresi (s)

# 🕒 4. Time-Fold Cross-Validation Yapısı
### Bu çalışmada, Cerqua vd. (2025) tarafından önerilen expanding window temporal cross-validation uygulanmıştır.
## Toplam fold sayısı: 3
| Fold | Train Yılları  | Valid (Test) Yılı |
| ---- | -------------- | ----------------- |
| 1    | 2021           | 2022              |
| 2    | 2021–2022      | 2023              |
| 3    | 2021–2022–2023 | 2024              |

### Bu yapının sağladığı avantajlar:

### 🚫 Zero leakage (ilerideki yılların bilgisi kullanılmaz)

#### 🔁 Expanding window (gerçek zaman akışını taklit eder)

### 🎯 En sağlam geçerlilik (2025 test yılına dokunulmaz)

### 🧪 CV tamamen train içinde

# 📈 5. Final Forecast (2025 Tahmini)

# Notebook sonunda:

### 2021–2024 tüm verisiyle model yeniden eğitilir, 2025 yılı için forecast üretilir. 

### Örnek çıktı:

COUNTRY     |  PRED_2025
------------|------------
Country A   |   47.82
Country B   |   61.12
Country C   |   54.30
