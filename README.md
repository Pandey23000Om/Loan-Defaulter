---

# 🏦 **Loan Default Prediction – End-to-End ML & MLOps Project**

This project builds an end-to-end **Loan Default Prediction** system, covering:

✔ Data cleaning & preprocessing
✔ Exploratory Data Analysis (EDA)
✔ Feature engineering
✔ Handling imbalanced datasets
✔ Model training & evaluation
✔ Model explainability (SHAP)
✔ MLflow experiment tracking & model registry
✔ System architecture design for production deployment
✔ Presentation deck summarizing the results

The goal is to develop a **production-ready, fully governed, explainable ML solution** to estimate the probability of loan default for a financial institution.

---

## 📂 **Repository Structure**

```
├── data/
│   ├── processed/          # Raw data (not versioned in repo)
│   ├── raw/                # Cleaned & transformed datasets
│
├── notebooks/
│   ├── 01-Preprocessing.ipynb
│   ├── 02-Feature_Analysis-Transformations.ipynb
│   ├── 03-Model_Development.ipynb
|   |── 04-ML-flow-Training.ipynb
│
├── System Architecture.svg        # System architecture diagram
├── Fraud Detection Presentation.pptx
├── README.md
└── requirements.txt
```

---

# 🚀 **1. Problem Statement**

Financial institutions need reliable mechanisms to **predict loan default risk**.
Traditional rule-based methods struggle with:

* Nonlinear borrower behavior
* Interactions between demographic & financial features
* Missing or incomplete credit history
* Imbalanced data (rare defaulters)

This project develops a **high-performance ML model** to score borrowers and assist credit underwriting, early warning systems, and risk monitoring.

---

# 🧹 **2. Data Cleaning & Preprocessing**

Key steps:

### ✔ Missing Value Handling

* `<4%` missing: **median** for numeric, **mode** for categorical
* High-missing columns: added indicator flags (e.g., `Score_Source_1_missing`)

### ✔ Outlier & Skewness Handling

* Binning: `Own_House_Age → Own_House_Age_bin`
* Log transform planned for extremely skewed features

### ✔ Categorical Cleaning

* Standardized gender (removed `XNA`)
* Encoded binary variables as category type

### ✔ Mixed Data Types

Fixed columns that had mixed numeric+string values.

### ✔ Final Dataset

Saved to:

```
data/processed/train.csv
data/processed/val.csv
data/processed/test.csv
```

---

# 🔍 **3. Exploratory Data Analysis (EDA)**

### ✔ Univariate analysis

* Distribution study for numeric & categorical variables
* Detected skewness, outliers, and rare categories
* Identified variable cardinality

### ✔ Bivariate analysis

* Default rate across categorical variables
* Correlation heatmaps
* Feature-wise AUC tests to evaluate predictive power

### ✔ Key EDA Findings

* Credit bureau scores (1/2/3) are strongest predictors
* High loan amount & annuity = higher risk
* Younger borrowers show higher default tendencies
* Employment duration strongly reduces risk

---

# 🛠 **4. Feature Engineering**

Implemented:

* Label encoding for categorical features
* Binning (`Own_House_Age`)
* Missing value indicators
* Feature-type separation (numeric vs categorical)
* Stratified train/val/test split (70/15/15)

No scaling needed for tree models.

---

# 🤖 **5. Modeling & Model Selection**

Models trained:

| Model               | AUC   | Recall | F1    | Recall @ Top 5% |
| ------------------- | ----- | ------ | ----- | --------------- |
| Logistic Regression | Low   | Low    | Low   | 0.10            |
| Decision Tree       | ~0.70 | 0.59   | 0.24  | 0.19            |
| **XGBoost**         | 0.75  | 0.84   | 0.21  | 0.21            |
| **LightGBM (Best)** | 0.755 | 0.841  | 0.216 | 0.208           |

### 📌 Final Choice: **LightGBM**

Because of:

* Highest AUC
* Strong recall for defaulters
* Stable behavior
* Excellent SHAP explainability
* Fastest inference time

---

# 🔎 **6. Model Explainability (SHAP)**

### ✔ Global Interpretability

Top contributors to default risk:

1. **Score_Source_3**
2. **Score_Source_2**
3. **Score_Source_1**
4. **Credit_Amount**
5. **Employment Days**
6. **Client Education**
7. **Age Days**
8. **Loan Annuity**

### ✔ Local Explanation

Waterfall plots describe **why** a borrower is predicted as high risk.

SHAP ensures **governance, fairness, and audit readiness**, crucial for banking.

---

# 📊 **7. MLflow Tracking & Model Registry**

### Logged via MLflow:

* Metrics (AUC, Recall, F1, Accuracy)
* Parameters
* Artifacts (plots, datasets)
* Requirement files & environment

### Registry:

* Best model registered under

  ```
  models:/LoanDefaultModel/
  ```
* Versioning
* Promotion workflow (Staging → Production)

### Loaded model:

```python
loaded = mlflow.pyfunc.load_model("models:/LoanDefaultModel/Production")
preds = loaded.predict(X_test)
```

---

# 🏗 **8. System Architecture (MLOps Pipeline)**

Architecture file included: **`architecture.svg`**

Key components:

* Data ingestion (API Gateway / batch)
* Data lake (S3)
* Feature Store (Feast)
* MLflow tracking + registry
* Training pipeline (Airflow/Kubeflow)
* Serving (FastAPI / KServe / SageMaker)
* Monitoring (Prometheus, Grafana, Evidently)
* Canary deployments + automatic rollback
* CI/CD (GitHub Actions + ArgoCD)

---

# 🔐 **9. Security & Governance Practices**

* End-to-end encryption (TLS + AES256)
* PII masking/tokenization
* Role-based access control (IAM + RBAC)
* Model signing + lineage tracking
* Drift detection & fairness monitoring
* Compliance: RBI Fair Lending, GDPR, Responsible AI
* Audit trails via MLflow & Data Catalog

---

# 🧪 **10. How to Run**

### Install dependencies

```bash
pip install -r requirements.txt
```

### Run EDA

Open:

```
notebooks/01-Preprocessing.ipynb
notebooks/02-Feature_Analysis-Transformations.ipynb
```

### Train models

```
notebooks/03-Model_Development.ipynb
```

### MLflow tracking + registry

```
notebooks/04-ML-flow-Training.ipynb
```

---

# 📈 **11. Results Summary**

* Achieved **AUC ~0.755**
* High **recall** for capturing defaulters (**~0.20**)
* Strong **SHAP explainability** ensures transparency
* Deployment-ready architecture included
* MLflow ensures full traceability and governance

---

# 📖 **12. Presentation**

A polished PowerPoint summarizing the project is included:

```
Fraud Detection Presentation.pptx
```

---

# 🙌 **13. Acknowledgements**

This project demonstrates:

* End-to-end DS workflow
* Real-world MLOps practices
* Enterprise-grade ML governance
* Production readiness

---
