# Loan Default Prediction — ML & MLOps Project

This repository contains an end-to-end Machine Learning & MLOps pipeline for predicting loan defaults.  
The project is structured to move from **Exploratory Data Analysis (EDA)** → **Feature Engineering** →  
**Model Development** → **Experiment Tracking** → **Containerized Deployment** → **Monitoring & Drift Detection**.

---

## 📌 Project Workflow

### 1. Exploratory Data Analysis (EDA)
We begin by loading raw loan-level data and performing an in-depth EDA to understand the structure, quality,  
and predictive patterns in the dataset. The EDA notebook:  
* notebooks/eda.ipynb


#### EDA Steps
1. **Load raw dataset** from `data/raw/`.
2. **Data profiling**  
   - Missing value analysis  
   - Data types & schema validation  
   - Summary statistics  
3. **Target distribution**  
   - Class imbalance check (default vs non-default).  
4. **Univariate analysis**  
   - Numerical feature distributions  
   - Categorical value counts  
5. **Bivariate analysis**  
   - Correlation heatmap  
   - Relationship between target and each feature  
6. **Outlier analysis**  
   - Boxplots  
   - Z-score/IQR methods  
7. **Feature quality assessment**  
   - Duplicate rows  
   - High-cardinality categoricals  
   - Skewed distributions  

EDA deliverables:
- Clean dataset → `data/processed/`
- EDA report → `notebooks/eda.ipynb`  
- Initial feature list & data dictionary

---

## 2. Data Preprocessing & Feature Engineering
After EDA, we will:
- Handle missing values  
- Treat outliers  
- Encode categorical variables  
- Create feature pipelines (scikit-learn Pipeline)  
- Save cleaned versioned datasets using **DVC**

Code will be in:
* src/features.py


---

## 3. Baseline Modeling
We start with tree-based and linear models:
- Logistic Regression  
- XGBoost  
- LightGBM  
- Random Forest  

Metrics used:
- AUC-ROC  
- Precision / Recall  
- Precision@K (top-risk borrowers)  
- Confusion matrix  
- Calibration curves  

Baseline model code:
* src/train.py


Experiments tracked in MLflow:
* mlruns/


---

## 4. Model Deployment
We containerize the model using **FastAPI + Uvicorn** and deploy using:

- Docker  
- Kubernetes (with readiness/liveness probes)  
- Optionally Seldon/BentoML for production-grade serving  

- Artifact:
    - src/serve.py
    - Dockerfile
    - k8s/


---

## 5. Monitoring & Drift Detection
Using **Evidently AI** and **Prometheus/Grafana**:
- Data drift detection  
- Prediction drift  
- Feature distribution shift  
- Model performance decay  
- Latency & error monitoring  

- Artifacts:
    - monitoring/
    - prometheus_rules/
    - grafana_dashboards/


---

## 6. CI/CD for ML
GitHub Actions will manage:
- Linting & tests  
- Schema validation  
- Model training workflow  
- Building & pushing Docker images  
- Deployment to staging → canary → production  

Artifacts:
- .github/workflows/

---

## 📁 Repository Structure
```
loan-default-mlops/
│── data/
│ ├── raw/
│ └── processed/
│── notebooks/
│ └── eda.ipynb
│── src/
│ ├── train.py
│ ├── serve.py
│ └── features.py
│── monitoring/
│── k8s/
│── requirements.txt
│── README.md
│── pre-requisites.md
```


---

## 🚀 Next Steps
After completing EDA:
1. Build preprocessing pipeline  
2. Create baseline models  
3. Log experiments via MLflow  
4. Package model for serving  
5. Implement CI/CD  
6. Set up monitoring dashboards  
7. Add alerts + governance  

---

# 👍 Contribution
PRs, suggestions, and improvements are welcome.

---
