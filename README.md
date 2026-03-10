# 🏥 Hospital Operations & Patient Readmission Prediction
> End-to-end Data + AI system built on Databricks | Medallion Architecture | MLflow | RandomForest

---

## 📌 Problem Statement
Hospital readmissions within 30 days are a critical operational and financial challenge.
This project builds a complete Data + AI pipeline to:
- Analyse patient flow, length of stay, and department-level KPIs
- Predict which patients are at high risk of readmission
- Support hospital administrators with actionable dashboards

---

## 📊 Dataset
- **Source:** Diabetes 130-US Hospitals Dataset (Kaggle)
- **Records:** 101,766 patient encounters
- **Features:** 50 columns including demographics, diagnoses, medications, and procedures
- **Target:** Readmission status (<30 days, >30 days, No readmission)

---

## 🏗️ Architecture — Medallion Pipeline
```
RAW CSV
   ↓
🥉 BRONZE LAYER  →  Raw ingestion, no transformations
   ↓
🥈 SILVER LAYER  →  Cleaning, null handling, feature encoding
   ↓
🥇 GOLD LAYER    →  Feature engineering, aggregations, ML-ready data
   ↓
🤖 ML MODEL      →  RandomForest Readmission Prediction + MLflow Tracking
   ↓
📊 DASHBOARD     →  Visualizations & KPI Summary
```

---

## 📁 Project Structure
```
hospital-operations-ai/
│
├── 01_Bronze_Ingestion.ipynb
├── 02_Silver_Transformation.ipynb
├── 03_Gold_Feature_Engineering.ipynb
├── 04_ML_Readmission_Prediction.ipynb
├── 05_Dashboard_Visualizations.ipynb
│
├── chart1_overview.png
├── chart2_patient_flow.png
├── chart3_kpis.png
├── chart4_feature_importance.png
│
└── README.md
```

---

## ⚙️ Setup & Requirements

- Databricks Community Edition (Runtime 13.3 LTS)
- Dataset uploaded to Unity Catalog Volume:
  `/Volumes/workspace/default/hospital_operations_ai/diabetic_data.csv`
- Libraries used: PySpark, MLflow, pandas, matplotlib

**Run notebooks in order:**
1. `01_Bronze_Ingestion`
2. `02_Silver_Transformation`
3. `03_Gold_Feature_Engineering`
4. `04_ML_Readmission_Prediction`
5. `05_Dashboard_Visualizations`

---

## 🔧 Feature Engineering (Gold Layer)

| Feature | Description |
|---|---|
| `high_medication_flag` | Patients with >15 medications |
| `high_procedures_flag` | Patients with >3 procedures |
| `frequent_visitor_flag` | Combined prior visits >3 |
| `long_stay_flag` | Hospital stay >7 days |
| `insulin_flag` | Active insulin prescription |
| `diabetes_primary_flag` | Diabetes as primary diagnosis |

---

## 🤖 ML Model — Readmission Risk Prediction

| | V1 | V2 (Tuned) |
|---|---|---|
| Algorithm | RandomForest | RandomForest |
| Trees | 100 | 200 |
| Max Depth | 6 | 8 |
| AUC | 0.6699 | **0.6742** |
| Accuracy | 0.6248 | **0.6287** |
| F1 Score | 0.6193 | **0.6225** |

**Top Predictors:**
1. `number_inpatient` — Prior hospitalizations (most dominant)
2. `frequent_visitor_flag` — Engineered feature (2nd highest)
3. `number_emergency` — Emergency visit history

Both experiments tracked and versioned in **MLflow**.

---

## 📈 Dashboard Visualizations

| Chart | Insight |
|---|---|
| ![Overview](chart1_overview.png) | Readmission distribution & avg length of stay |
| ![Patient Flow](chart2_patient_flow.png) | Admission types & age-group readmission rates |
| ![KPIs](chart3_kpis.png) | Medication load & risk flag analysis |
| ![Feature Importance](chart4_feature_importance.png) | ML model top predictors |

---

## 💡 Business Impact

- Identifies high-risk patients **before discharge** for targeted intervention
- Department-level KPIs support **administrator capacity planning**
- Readmission rate insights help reduce **operational costs and penalties**
- Fully reproducible pipeline supports **ongoing monitoring and retraining**

---

## 👩‍💻 Author
**Dhakshitha Herculin C**  
MBA – Business Analytics | SRM University  
[LinkedIn](https://linkedin.com/in/dhakshitha-herculin-c-042718172) | 
[GitHub](https://github.com/dhakshi128)
