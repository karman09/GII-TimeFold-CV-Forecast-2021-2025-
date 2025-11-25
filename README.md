
### ✔ Veri Hazırlama
- MOD-Z Score ile aykırı değer analizi  
- Aykırı → median imputasyonu (çifte imputasyon yok)  
- KNN imputasyonu (sadece train üzerinden fit + test’e transform)  
- StandardScaler (train -> fit, test -> transform)

### ✔ Özellik Seçimi
- LASSO (CV) ile ilk daraltma  
- Ardından iteratif VIF < 10 filtresi  
- Nihai model daha az, daha güçlü değişkenle eğitilir

### ✔ Modeller
- **XGBoost (tree_method='hist')**
- **LightGBM**
- **RandomForest**
- **ElasticNetCV** (meta-model – stacking)
- Tüm modellerde eğitim seti ile RandomizedSearchCV hiperparametre araması

### ✔ 2025 Tahmini
Model çıktısı olarak:
- Ülke bazlı 2025 GII tahmini
- Tüm modellerin performans tablosu
- Stacking meta-model final sonucu  
üretilir.

---

## 📂 Proje Yapısı


