# E‑commerce ML Pipeline

[![Python](https://img.shields.io/badge/Python-3.12-blue)](https://www.python.org/)
[![Databricks](https://img.shields.io/badge/Databricks-EE4C2C?logo=databricks&logoColor=white)](https://databricks.com/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Render](https://img.shields.io/badge/Render-Deployed-brightgreen)](https://render.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow)](https://opensource.org/licenses/MIT)

End-to-end ML system for e‑commerce platform covering data pipeline, model training, and real‑time inference.

**Live API:** 👉 [ml-delivery-api-1.onrender.com/docs](https://ml-delivery-api-1.onrender.com/docs)

---

## 📖 Overview

This project demonstrates a complete **end-to-end machine learning pipeline** for an e‑commerce platform:

- **Data Pipeline:** Bronze → Silver → Gold (Medallion Architecture) on Databricks
- **ML Models:** Delivery delay prediction, demand forecasting, sentiment analysis
- **Model Serving:** REST APIs via FastAPI (deployed on Render)
- **Automation:** Daily Databricks Job for batch inference

---

## 🏗️ Architecture


mermaid
graph TD

    A[Raw CSV Files] --> B[Bronze Layer]
    B --> C[Silver Layer]
    C --> D[Gold Layer]
    D --> E[Model Training]
    E --> F[Model Serving]
    F --> G[FastAPI Backend]
    G --> H[Live API Endpoints]
    C --> I[Daily Databricks Job]
    I --> F
    
# 📊 Data Flow

| Layer | Action |
|--------|--------|
| Bronze | Raw data ingestion (Auto Loader) |
| Silver | Data cleaning, type casting, deduplication |
| Gold | Customer-level aggregates, daily aggregations |
| Model Training | CatBoost, XGBoost, Hugging Face |
| Model Serving | Databricks Serving Endpoints |
| API | FastAPI backend (deployed on Render) |

# 🤖 Models

| Model | Type | Best Model | Performance |
|---------|---------|---------|---------|
| Delivery Delay | Binary Classification | CatBoost | ROC-AUC 0.878 |
| Demand Forecasting | Time-Series Regression | CatBoost | MAE 607, MAPE 2.5% |
| Sentiment Analysis | Zero-shot NLP | Hugging Face (DistilBERT) | Aspect-wise sentiment |

# 📝 Model Details

| Model | Description |
|---------|---------|
| Delivery Delay | Predict if an order will be delayed based on platform, order value, delivery time, and customer history. |
| Demand Forecasting | Predict next 7 days total units sold using lags, rolling means, and date features. |
| Sentiment Analysis | Extract aspect-wise sentiment (delivery, quality, price, support, packaging) from customer feedback using zero-shot classification. |

# 🔌 Live API

| Endpoint | Method | Description |
|------------|------------|------------|
| `/docs` | GET | Interactive Swagger UI |
| `/health` | GET | Health check |
| `/predict-delay` | POST | Delivery delay probability |
| `/analyze-sentiment` | POST | Aspect-wise sentiment |
| `/forecast` | GET | Next 7 days demand forecast |

## 📝 Example Request

```bash
curl -X POST "https://ml-delivery-api-1.onrender.com/predict-delay" \
-H "Content-Type: application/json" \
-d '{
  "platform_name":"blinkit",
  "order_value_inr":450,
  "delivery_time_min":25,
  "customer_delay_rate":0.24
}'
```

---

# 🛠️ Tech Stack

| Layer           | Tools                                        |
| --------------- | -------------------------------------------- |
| Data Pipeline   | Databricks, PySpark, Delta Lake              |
| ML Models       | CatBoost, XGBoost, Hugging Face Transformers |
| Model Serving   | Databricks Model Serving                     |
| API             | FastAPI, Uvicorn                             |
| Deployment      | Render (Free Tier)                           |
| Version Control | Git, GitHub                                  |

---

# 📁 Repository Structure

```text
ecommerce-ml-pipeline/
│
├── README.md
├── LICENSE
│
├── notebooks/
│   ├── 01_bronze_ingestion.ipynb
│   ├── 02_silver_transformation.ipynb
│   ├── 03A_gold_customer_features.ipynb
│   ├── 03B_gold_daily_aggregation.ipynb
│   ├── 04_delivery_model_training.ipynb
│   ├── 04_demand_model_training.ipynb
│   ├── 04_sentiment_model_training.ipynb
│   ├── 05_delivery_inference.ipynb
│   ├── 05_demand_inference.ipynb
│   └── 05_sentiment_inference.ipynb
│
├── serving_notebooks/
│   ├── 01_register_delivery_model.ipynb
│   ├── 02_register_demand_model.ipynb
│   └── 03_register_sentiment_model.ipynb
│
│
└── screenshots/
    ├── architecture.png
    ├── databricks_dashboard.png
    └── swagger_ui.png
```

### Folder Description

| Folder/File          | Description                                                                         |
| -------------------- | ----------------------------------------------------------------------------------- |
| `notebooks/`         | Databricks notebooks for Bronze, Silver, Gold layers, model training, and inference |
| `serving_notebooks/` | Model registration notebooks used for Databricks Model Serving                      |
| `screenshots/`       | Architecture diagram, dashboard screenshots, and API documentation screenshots      |
| `README.md`          | Project documentation                                                               |
| `LICENSE`            | Project license                                                                     |

```
```


### 📌 Backend API Repository

`ml-delivery-api`

---

# 🚀 Deployment

## Databricks Pipeline (Daily Automation)

| Configuration | Details                 |
| ------------- | ----------------------- |
| Job Name      | Daily_ML_Pipeline       |
| Schedule      | Daily at 6:00 AM (IST)  |
| Monitoring    | Email Alerts on Failure |

### Workflow Tasks

1. Bronze Ingestion (Incremental Load)
2. Silver Transformation
3. Gold Aggregations
4. Inference Notebooks
5. Monitoring & Alerts

---

## API Deployment (Render)

| Configuration         | Value                                          |
| --------------------- | ---------------------------------------------- |
| Build Command         | `pip install -r requirements.txt`              |
| Start Command         | `uvicorn main:app --host 0.0.0.0 --port $PORT` |
| Environment Variables | Databricks Host, Token, SQL Warehouse Details  |

> **Note:** Render Free Tier may experience cold starts (30–60 seconds) after inactivity. Timeout is configured to 90 seconds.

---


# 📸 Screenshots

## 🏗️ End-to-End ML Pipeline Architecture

![Architecture Diagram](screenshots/Architecture_E-Commerce_Pipeline.png)

---

## 📊 KPI Operations Dashboard

![KPI Dashboard](screenshots/daashboard_E-Commerece_Pipeline.png)

---

## 🚀 FastAPI Swagger Documentation

![Swagger UI](screenshots/swagger_ui.png)

---

---

# 📈 Key Learnings

✅ Building Production-Grade ML Pipelines on Databricks

✅ Medallion Architecture (Bronze → Silver → Gold)

✅ Model Serving & REST API Deployment

✅ Databricks Workflows Automation

✅ Real-Time Inference using FastAPI

✅ End-to-End MLOps Lifecycle

---

# 🔮 Future Improvements

* API Authentication (JWT / API Keys)
* CI/CD using GitHub Actions
* Advanced Monitoring & Logging
* Docker Containerization
* Real-Time Kafka Streaming
* Model Drift Detection
* Automated Retraining Pipeline

---

# 👨‍💻 Author

**Piyush Madhukar**  
PG-DBDA Trainee | Data Analytics | Machine Learning | Big Data Analytics

📧 Open to opportunities in Data Analytics, Data Science, and Machine Learning.

### Connect with Me

- 🔗 GitHub: [byte-piyush16](https://github.com/byte-piyush16)
- 🔗 LinkedIn: [Piyush Madhukar](https://www.linkedin.com/in/piyushmadhukar45/)

---

⭐ If you found this project useful, please consider giving it a star on GitHub.

💡 Feel free to connect with me for collaborations, project discussions, or opportunities in Data Analytics and Machine Learning.
