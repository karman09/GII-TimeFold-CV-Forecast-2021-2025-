🌍 GII TimeFold CV Forecast (2021–2025)
Zero-Leakage, Time-Aware Machine Learning Forecasting Pipeline

Bu proje, Global Innovation Index (GII) tahmini için tasarlanmış, tamamen sızıntısız, zamana duyarlı, gerçekçi ve tekrarlanabilir bir makine öğrenimi pipeline’ıdır.
Pipeline, yıllar arası bilgi sızıntısını tamamen ortadan kaldıran Time-Fold Cross-Validation yapısını kullanır.


:

🤖 3. Model Eğitimi

Notebook’ta dört model ile eğitim yapılır:

⚡ XGBoost Regressor

Gradient boosting

Yüksek doğruluk

Hızlı hesaplama

💡 LightGBM Regressor

Büyük veri için optimize

Düşük gecikme

Memory-efficient

🌲 RandomForest Regressor

Non-linear ilişkilerde güçlü

Yüksek stabilite

Bagging tabanlı yapı

🔺 AdaBoost Regressor

(Notebook kodunda DecisionTree tabanlı AdaBoost modeli var)

Weak learner → güçlü modele dönüştürür

Outlier’lara karşı duyarlı

Zayıf ilişkilerde bile iyileştirici etki sağlar

Özellikle yüksek bias durumlarında güçlü sonuç verir

Her model için şu metrikler hesaplanır:

Train R²

Test R²

RMSE

MAE

MAPE (%)

Time-Fold CV R² (Mean & Std)

Model Çalışma Süresi
