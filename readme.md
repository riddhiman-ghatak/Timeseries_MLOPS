

# 📈 ARIMA Time Series Forecasting with MLOps on GCP using Flask

A complete end-to-end time series forecasting pipeline using the ARIMA family of models, deployed using MLOps principles on Google Cloud Platform. The project leverages Docker, Kubernetes, Cloud Build, Pub/Sub, and Cloud Functions to ensure CI/CD capabilities and production-readiness.

---

## 🎯 Business Objective

Time series data appears in many real-world applications such as:

* Weather tracking
* Application performance monitoring
* Real-time vital statistics in healthcare systems

The **ARIMA** (Auto-Regressive Integrated Moving Average) model is a powerful statistical tool for time series forecasting. It is well-suited for structured time series data collected at regular intervals. Extensions like **ARIMAX** (ARIMA with exogenous variables) and **SARIMAX** (Seasonal ARIMAX) further enhance its capability.

**MLOps** is the backbone of reliable, scalable, and automated machine learning deployment. This project embodies the MLOps paradigm using GCP services to operationalize ARIMA-based time series forecasting.

---

## 🗂️ Dataset Description

The dataset captures **monthly call center data** across multiple sectors and includes relevant external regressors:

| Column        | Description                                  |
| ------------- | -------------------------------------------- |
| `Month`       | Monthly timestamp                            |
| `Healthcare`  | Calls for the healthcare domain              |
| `Telecom`     | Calls for the telecom domain                 |
| `Banking`     | Calls for the banking domain                 |
| `Technology`  | Calls for the technology domain              |
| `Insurance`   | Calls for the insurance domain               |
| `Phone Lines` | Number of available phone lines (regressor)  |
| `Channels`    | Number of communication channels (regressor) |

* **Total rows**: 132
* **Granularity**: Monthly

---

## 🚀 Project Objectives

* Develop a robust **ARIMA/ARIMAX/SARIMAX** forecasting model.
* Implement a complete **MLOps pipeline** on **Google Cloud Platform**.
* Serve the model using **uWSGI + Flask** in a scalable production environment.

---

## 🧰 Tech Stack

| Domain           | Tools / Frameworks                        |
| ---------------- | ----------------------------------------- |
| Language         | Python                                    |
| ML Libraries     | `pandas`, `numpy`, `statsmodels`, `scipy` |
| Visualization    | `matplotlib`, `seaborn`                   |
| Web Server       | Flask + uWSGI                             |
| Containerization | Docker                                    |
| Orchestration    | Kubernetes (GKE)                          |
| CI/CD            | GCP Cloud Build, Pub/Sub, Cloud Functions |
| Cloud Platform   | Google Cloud Platform                     |

---

## 🧪 Methodology

1. **Data Ingestion & Cleaning**
2. **Exploratory Data Analysis (EDA)**
3. **Stationarity Testing**

   * Augmented Dickey-Fuller (ADF)
   * KPSS Test
4. **Model Selection**

   * White Noise, Random Walk check
   * ACF & PACF Plots
   * Holt-Winters Exponential Smoothing
   * ARIMA Parameter Tuning
   * LLR Test, AIC, Log-Likelihood Comparisons
5. **Model Extensions**

   * **ARIMAX**: Integrate external regressors
   * **SARIMAX**: Handle seasonality
6. **Evaluation & Residual Analysis**

---

## ☁️ MLOps on GCP

### 1. Cloud Build Trigger (CI)

* Create trigger linked to your source repository (GitHub/Cloud Source Repos).

### 2. Google Kubernetes Engine (GKE)

* Launch GKE cluster.
* Apply Kubernetes config files:

  ```bash
  kubectl apply -f deployment.yaml
  kubectl apply -f service.yaml
  ```

### 3. Cloud Pub/Sub

* Create a `cloud-build` Pub/Sub topic.
* Setup a subscriber for downstream triggering.

### 4. Cloud Functions (CD)

* Create a Cloud Function with:

  * Entrypoint: `onNewImage`
  * Trigger: Pub/Sub message
  * Environment Vars: `PROJECT`, `ZONE`, `CLUSTER`, `DEPLOYMENT`
  * Source: Code from `cloud-function-trigger/`

**Pipeline Flow:**

1. Git commit → Cloud Build triggers → Docker image built.
2. Cloud Build sends message to Pub/Sub.
3. Pub/Sub triggers Cloud Function.
4. Cloud Function pulls latest image and deploys to GKE.

**Kubernetes Logs:**

```bash
kubectl get pods
kubectl logs <pod-name>
```

---

## 🗂️ Code Structure

```
project-root/
│
├── Input/                      # Raw Dataset (Data-chillers.csv)
├── Output/                     # Model outputs (pickled .pkl files)
├── Notebook/                   # ARIMA notebook for EDA & modeling
├── MLPipeline/                 # Core ML logic (feature engg, modeling)
├── Engine/                     # Runs MLPipeline scripts
├── cloud-function-trigger/     # GCP Cloud Function code
├── kubernetes-files/           # deployment.yaml, service.yaml
│
├── main.py                     # Flask app entrypoint
├── Dockerfile                  # Docker image config
├── uwsgi.ini                   # uWSGI config file
├── requirements.txt            # Python dependencies
├── __init__.py                 # Required package file
└── README.md                   # You're reading it!
```

---

## 📌 How to Run Locally

1. Clone the repo
2. Create and activate a virtual environment
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```
4. Start server locally:

   ```bash
   uwsgi --ini uwsgi.ini
   ```

---

## 🧠 Key Learnings

* How to build and validate time-series models like ARIMA, ARIMAX, and SARIMAX.
* How to containerize and deploy ML models with Docker & uWSGI.
* How to set up a CI/CD workflow using Cloud Build, Pub/Sub, and Cloud Functions on GCP.
* How to scale and monitor deployments using GKE.


