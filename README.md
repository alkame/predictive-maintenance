
## Deutsch

**Titel:** Predictive Maintenance (Regression + Klassifikation)  

**Ziel:**  
Frühzeitige Erkennung von Störungen an Maschinenlagern und Sensordaten, bevor akustische oder physische Schäden auftreten.  
Kombination aus Restnutzungsdauer-Schätzung (RUL, Regression) und Frühwarnsignal (Klassifikation).  

**Vorgehen:**  
1. GPU-Setup: Nutzung von LightGBM mit GPU-Beschleunigung  
2. Datenaufbereitung: Laden von Sensordaten (CSV), Zeitstempel, Feature-Lags, Condition-Indicator  
3. Zielvariablen:  
   - `time_to_failure` (Regression)  
   - `y_cls_early_window` (binary classification, 60-Minuten-Fenster)  
   - Klassengewichte gegen Class-Imbalance  
4. Feature Engineering: Skalierung, One-Hot-Encoding, Ordinal-Encoding (`severity`)  
5. Modellierung: LightGBM Regressor + Classifier, Hyperparameter-Tuning mit HalvingRandomSearchCV  
6. Cross-Validation: TimeSeriesSplit zur Sicherung zeitlicher Konsistenz  
7. Metriken:  
   - Regression: MAE, MAPE  
   - Klassifikation: PR-AUC, F1-Score  
   - Kosten-sensitive Schwellenwertoptimierung (FN=5, FP=1)  
8. Visualisierungen: ROC-Kurve, Precision-Recall, Konfusionsmatrix, Feature-Importance, Residuen-Analysen  
9. Artefakte:  
   - Modelle (`rul_lgbm.joblib`, `earlywarn_lgbm.joblib`, `preprocessor.joblib`)  
   - Schwellenwert (`earlywarn_threshold.joblib`)  
   - Metriken (`metrics_summary_pm2.csv`)  
   - Grafiken (`viz/`)  

**Ergebnis:**  
- PR-AUC = 0.87  
- Downtime-Reduktion: 10–12 %  

---

## English

**Title:** Predictive Maintenance (Regression + Classification)  

**Objective:**  
Early detection of failures in bearings and sensor data before acoustic or physical damage occurs.  
Combines Remaining Useful Life estimation (RUL, regression) with early warning classification.  

**Workflow:**  
1. GPU setup: Using LightGBM with GPU acceleration  
2. Data preprocessing: Load CSV sensor data, timestamps, feature lags, condition indicator  
3. Target variables:  
   - `time_to_failure` (regression)  
   - `y_cls_early_window` (binary classification, 60-minute window)  
   - Class weights to handle imbalance  
4. Feature Engineering: Scaling, one-hot encoding, ordinal encoding (`severity`)  
5. Modeling: LightGBM regressor + classifier, hyperparameter tuning with HalvingRandomSearchCV  
6. Cross-validation: TimeSeriesSplit to ensure temporal consistency  
7. Metrics:  
   - Regression: MAE, MAPE  
   - Classification: PR-AUC, F1-score  
   - Cost-sensitive threshold optimization (FN=5, FP=1)  
8. Visualizations: ROC curve, precision-recall, confusion matrix, feature importance, residual analysis  
9. Artifacts:  
   - Models (`rul_lgbm.joblib`, `earlywarn_lgbm.joblib`, `preprocessor.joblib`)  
   - Threshold (`earlywarn_threshold.joblib`)  
   - Metrics (`metrics_summary_pm2.csv`)  
   - Plots (`viz/`)  

**Result:**  
- PR-AUC = 0.87  
- Downtime reduction: 10–12 %  

