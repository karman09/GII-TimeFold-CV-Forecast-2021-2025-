# GII-TimeFold-CV-Forecast-2021-2025-
🧭 1. Proje Özeti

Bu proje, yıllık veriler üzerinde gelecek yılları tahmin etmek için tasarlanmış, tamamen sızıntısız, realistik, zaman boyutunu koruyan bir makine öğrenimi pipeline’ıdır.

Pipeline’ın temel bileşenleri:

🛡 Zero-Leakage (train/test tamamen ayrık)

⏳ Time-Based Fold Cross-Validation

🔍 Modified Z-Score Outlier Detection

🩺 Median + KNN Imputation (train-only)

📏 Train-Only Scaling (StandardScaler)

🧬 LASSO Feature Selection

🔁 Iterative VIF Removal

🤖 Model Seti: XGBoost, LightGBM, RandomForest

🎯 Yıl Bazlı Tahmin Üretimi (Final Forecast)

🗂️ 2. Pipeline Mimarisi

Aşağıdaki pipeline, notebook içerisinde adım adım uygulanmıştır.

🔍 2.1 Outlier Detection — Modified Z-Score

Sadece train yıllarında hesaplanır

|Modified-Z| > 3.5 → aykırı değer kabul edilir

Aykırı değerler NaN yapılır (silinmez)

Median & MAD → leakage engellenir

✔ Test dönemine dokunulmaz.
✔ Parametreler geleceği görmez.

🩺 2.2 Median Imputation (Only Outlier NaNs)

Outlier → NaN olan değerler doldurulur

Train median hesaplanır

Test → train median ile doldurulur

"Çift imputasyon" yoktur.

📏 2.3 Scaling (StandardScaler — Train Only)
scaler.fit(train)
scaler.transform(train)
scaler.transform(test)


✔ Test set’in bilgisi train’e sızmaz.
✔ Zamansal tutarlılık korunur.

🧮 2.4 KNN Imputation — Scaled Domain

Notebook’taki prensip uygulanır:

scale → KNN → inverse scale

Train scaled → KNN

Test scaled → (train-fitted KNN)

Sonra tüm değerler inverse-scale edilir

✔ Sızıntısız
✔ Tutarlı
✔ Tekrarlanabilir

🧬 2.5 LASSO Feature Selection (LassoCV)

CV ile optimum alpha

Katsayısı sıfır olmayan değişkenler tutulur

Sonuç dosyası + Türkçe çeviri oluşturulur

Final feature set → VIF aşamasına girer

🔁 2.6 Multicollinearity Control — VIF Filtering

Her iterasyonda VIF hesaplanır

VIF > 10 olanlar çıkarılır

Tekrar hesaplanır

En stabil değişken seti elde edilir

🌐 2.7 Türkçe Değişken İsimleri

translation_map ile İngilizce → Türkçe dönüşüm

Son raporlar tamamen Türkçeleştirilmiş değişken isimleri içerir

Akademik sunum kalitesi artırılır

🤖 3. Model Eğitimi

Notebook’ta şu modeller ile eğitim yapılır:

⚡ XGBoost Regressor

Gradient boosting yapısı

Hızlı ve güçlü

🌲 RandomForest Regressor

Non-linear yapı

Güçlü kararlılık

💡 LightGBM Regressor

Memory efficient

Büyük veri için hızlı

Her model için:

Train R²

Test R²

RMSE

MAE

MAPE

Time-Fold CV R² (Mean & Std)

Tahmin süresi

raporlanır.

🧪 4. Time-Fold Cross-Validation Yapısı

Klasik K-Fold yerine zaman tabanlı fold kullanılır.
