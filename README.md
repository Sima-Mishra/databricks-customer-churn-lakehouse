# Customer Churn & Lifetime Value Analytics  
## End-to-End Databricks Lakehouse Project

---

## Overview
This project demonstrates a production-grade **Databricks Lakehouse implementation** using **Bronze → Silver → Gold architecture**, governed by **Unity Catalog**, and extended with **machine learning using MLflow**.

The objective is to analyze e-commerce transaction data, engineer customer-level metrics, identify churn behavior, and build a churn prediction model to support data-driven business decisions.

This project was developed for the **Build With Databricks – Hands-On Project Challenge**.

---

## Business Problem
E-commerce businesses struggle to:
- Identify customers likely to churn
- Understand customer lifetime value
- Maintain scalable and governed analytics pipelines

This project addresses these challenges by building an end-to-end Lakehouse pipeline and applying machine learning for churn prediction.

---

## Dataset
- **Dataset**: Online Retail Dataset  
- **Records**: ~541,000 transactions  
- **Type**: Transaction-level retail data  

**Key Columns**
- CustomerID  
- InvoiceDate  
- Quantity  
- UnitPrice  
- Country  

The dataset contains missing values and cancelled transactions, reflecting real-world data quality issues.

---

## Architecture (Medallion Architecture)

Unity Catalog Volume (Raw CSV)
↓
Bronze Layer (Raw Delta Tables)
↓
Silver Layer (Cleaned & Enriched Data)
↓
Gold Layer (Business Metrics & ML Features)
↓
ML Model (Spark ML + MLflow)


---

## Bronze Layer — Raw Ingestion
- Raw CSV ingested from a **Unity Catalog Volume**
- No transformations applied
- Stored as Delta table to preserve data lineage

**Table**
ecommerce.bronze.bronze_online_retail

## Silver Layer — Data Cleaning & Feature Engineering
**Transformations Applied**
- Removed records with NULL `CustomerID`
- Excluded cancelled invoices
- Standardized timestamp format
- Created transaction value feature (`total_amount`)

**Table**
ecommerce.silver.silver_online_retail

## Gold Layer — Business Metrics

### Customer Metrics Table
ecommerce.gold.gold_customer_metrics

**Features**
- Total Spend
- Total Orders
- Last Purchase Date
- Days Inactive
- Churn Label

**Churn Definition**
> A customer is classified as churned if inactive for more than **90 days**, calculated relative to the dataset’s last transaction date.

---

### Monthly Revenue Table
ecommerce.gold.gold_monthly_revenue

## Machine Learning
- **Model**: Logistic Regression (Spark ML)
- **Target Variable**: Churn (0 = Active, 1 = Churned)
- **Features Used**:
  - total_spend
  - total_orders
  - days_inactive

### MLflow Integration
- Experiment tracking
- Model artifact logging
- Metric logging (Accuracy, AUC)
- Artifacts stored in a Unity Catalog volume

---

## Analytics & Insights
Analytics were derived using Databricks SQL on Gold tables:
- Churn distribution analysis
- Top customers by revenue
- Monthly revenue trends

These insights help identify high-value customers and design effective retention strategies.

---

## Orchestration
A Databricks Job automates the full pipeline:
1. Bronze ingestion
2. Silver transformations
3. Gold aggregations
4. ML model training

---

## Governance
- Unity Catalog used for:
  - Catalog and schema management
  - Governed data access
  - Volume-based storage for data and ML artifacts
- Ensures enterprise-grade data governance

---

## Tech Stack
- Databricks (Serverless)
- Apache Spark (PySpark)
- Delta Lake
- Unity Catalog
- Databricks SQL
- MLflow
- Spark ML

---

## How to Run
1. Upload dataset to a Unity Catalog Volume  
2. Run notebooks in order:
   - `01_bronze_ingestion`
   - `02_silver_cleaning`
   - `03_gold_analytics`
   - `04_ml_churn_model`
3. Execute Databricks Job for automation  
4. Run SQL queries on Gold tables for insights  
5. Review MLflow experiment for model performance  

---

## Business Impact
- Early identification of churn-prone customers
- Recognition of high-value customers
- Scalable analytics and ML pipeline
- Production-ready Databricks Lakehouse design

---

## Future Enhancements
- Advanced ML models (Random Forest, XGBoost)
- RFM-based customer segmentation
- Real-time churn prediction
- Interactive dashboards

---

## Conclusion
This project showcases an end-to-end **Databricks Lakehouse solution** combining data engineering, analytics, machine learning, governance, and orchestration.  
It reflects real-world industry practices and serves as a strong portfolio project.



