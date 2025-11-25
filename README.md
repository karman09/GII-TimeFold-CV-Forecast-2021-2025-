🧭 1. Proje Özeti

Bu proje, yıllık veriler üzerinde gelecek yılları tahmin etmek için tasarlanmış, tamamen sızıntısız, gerçekçi, zaman boyutuna duyarlı bir makine öğrenimi pipeline’ıdır.

Pipeline; veri temizleme, özellik seçimi, çoklu model eğitimi ve zaman tabanlı çapraz doğrulama adımlarını eksiksiz uygulayarak 2025 tahmini üretir.

Kullanılan ana bileşenler:

🛡 Zero-Leakage Training

⏳ Time-Based Fold Cross-Validation (Year → Year+1)

🔍 Modified Z-Score Outlier Detection

🩺 Median + KNN Imputation (train-only)

📏 Train-Only Standardization

🧬 LASSO Feature Selection

🔁 Iterative VIF Filtering (Multicollinearity)

🤖 ML Modelleri: XGBoost, LightGBM, RandomForest, AdaBoost

🎯 Son yıl (2025) için final tahmini

🗂️ 2. Pipeline Mimarisi

Notebook'un uyguladığı adımlar aşağıdaki gibi özetlenmiştir.

🔍 2.1 Outlier Detection — Modified Z-Score

Yalnızca train yıllarında hesaplanır

|Z| > 3.5 olan gözlemler → NaN

Median & MAD → leakage’sız hesaplama

✔ Test set'e dokunmaz
✔ Gelecek yılların bilgisi kullanılmaz

🩺 2.2 Median Imputation (Only Outlier NaNs)

Outlier → NaN olan değerleri doldurur

Train median → test’e uygulanır

Çifte imputasyon yoktur

📏 2.3 Scaling (StandardScaler — Train Only)
scaler.fit(train)
scaler.transform(train)
scaler.transform(test)


✔ Parametreler geleceği görmez
✔ Zaman sırası korunur

🧮 2.4 KNN Imputation — Scaled Domain

Notebook’taki prensip:

scale → KNN → inverse scale

Train scaled → KNN ile doldurulur

Test scaled → train-fitted KNN ile doldurulur

Sonra inverse-scale edilir

🧬 2.5 LASSO Feature Selection (LassoCV)

CV ile optimum alpha

Sıfır olmayan katsayılı değişkenler

Seçilmiş değişken tablosu

Türkçe çeviri eşlemeleri

🔁 2.6 Multicollinearity Control — VIF Filtering

VIF > 10 olan değişkenler çıkarılır

Döngü VIF < 10 olana kadar devam eder

Sonuç: daha stabil, daha anlamlı özellik seti

🌐 2.7 Türkçe Değişken İsimleri

translation_map içinden otomatik çeviri

Final Excel raporları Türkçe isimlerle oluşturulur

Rapor okunabilirliği artırılır

🤖 3. Model Eğitimi

Notebook dört farklı regresyon modeli ile eğitim yapar:

⚡ XGBoost Regressor

Gradient Boosting tabanlı

Hızlı + yüksek doğruluk

Non-linear ilişkileri iyi yakalar

💡 LightGBM Regressor

Memory efficient

Büyük veri odaklı

Çok hızlı eğitim süresi

🌲 RandomForest Regressor

Bagging tabanlı

Yüksek kararlılık

Hyperparametre bağımlılığı düşük

🔺 AdaBoost Regressor

Weak learner → strong learner

DecisionTree tabanlı boosting

Yüksek bias senaryolarını iyileştirir

Basit ama etkili bir boosting algoritması

Her model için notebook şunları hesaplar:

Train R²

Test R²

RMSE

MAE

MAPE (%)

Time-Fold CV R² (Mean & Std)

Model çalışma süresi

Sonuçlar tablo halinde raporlanır.

🧪 4. Time-Fold Cross-Validation Yapısı

Her fold’da eğitim yılları genişler, test yılı 1 yıl ilerler:

Fold	Train Yılları	Test Yılı
1	2019	2020
2	2019–2020	2021
3	2019–2021	2022
4	2019–2022	2023
5	2019–2023	2024

Bu yapı şu avantajları sağlar:

🚫 Zero leakage

🕒 Zaman sırası bozulmaz

🎯 Gerçek dünyaya en yakın validasyon yapısı
