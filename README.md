# FMCG Data Lakehouse ETL Pipeline

## 📌 Overview
This project demonstrates an **end-to-end ETL pipeline** built on **Databricks Free Edition** using the **Medallion Architecture (Bronze, Silver, Gold layers)**.  
The pipeline was designed to integrate data from a newly merged FMCG company into the existing enterprise lakehouse, enabling unified analytics and business intelligence.

---

## 🏢 Business Requirement

### Problem Statement
After the merger of two FMCG companies, the organization faced challenges in consolidating data:
- The **existing company’s data** was already curated and available in the **Gold layer**, maintained by a separate pipeline.  
- The **new company’s data** was not yet integrated, requiring ingestion from raw sources and transformation into analytics-ready datasets.  
- Reporting was fragmented, with inconsistent definitions across dimensions and fact tables.  
- Historical records needed to be preserved while enabling **incremental daily loads** for new transactions.  
- Business stakeholders demanded unified dashboards across **sales, supply chain, and finance** to support faster decision-making.

### Approach
Our pipeline concentrated on the **new company’s data**:
1. **Data Ingestion (Bronze Layer)**  
   - Raw datasets ingested into **Amazon S3**.  
   - Established catalog and schema for structured ingestion.  

2. **Data Transformation (Silver Layer)**  
   - Applied cleaning, validation, and harmonization using **PySpark and SQL**.  
   - Standardized data models to align with the parent company’s definitions.  

3. **Data Modeling (Fact & Dimension Tables)**  
   - Built **Customer Dimension**, **Product Dimension**, and **Pricing Dimension** tables.  
   - Built the **Sales Fact table** including measures such as **Gross Price**, Quantity, and Revenue.  
   - Supported both **historical loads** (legacy data migration) and **incremental loads** (daily updates).  

4. **Integration (Gold Layer)**  
   - Delivered curated datasets into the Gold layer, ensuring compatibility with the existing company’s data.  
   - Created denormalized tables for faster querying and BI consumption.  

5. **Automation & Monitoring**  
   - Orchestrated jobs with Databricks workflows.  
   - Implemented monitoring and alerting for pipeline reliability.  

6. **Analytics Delivery**  
   - Exposed unified datasets to **BI dashboards (Power BI/Tableau)** and **Genie** for advanced querying.  

---

## 📒 Notebook Execution Flow

The pipeline is organized into multiple Databricks notebooks:

### **1_setup/**
- **dim_date_table_creation.ipynb** → Creates the **Date Dimension** table for fiscal year calculations and aligning transactions.  
- **setup_catalog.ipynb** → Handles **catalog, schema, and database creation** in Databricks.  
- **utilities.ipynb** → Defines **global variables** and reusable functions for consistency across notebooks.  

### **2_dimension_data_processing/**
- **1_customers_data_processing.ipynb** → Builds the **Customer Dimension** table.  
- **2_products_data_processing.ipynb** → Builds the **Product Dimension** table.  
- **3_pricing_data_processing.ipynb** → Builds the **Pricing Dimension** table.  

### **3_fact_data_processing/**
- **1_full_load_fact.ipynb** → Creates the **Sales Fact table** for **historical loads**.  
- **2_incremental_load_fact.ipynb** → Updates the **Sales Fact table** with **incremental daily loads**.  
- Both notebooks integrate the **child company’s fact data** with the **parent company’s Gold layer**.  

### **0_data/**
- Contains raw datasets (CSV files) placed in **Amazon S3**.  
- Includes both **historical loads** and **incremental loads** (e.g., `orders_2025_12_31.csv`).  

### **2_dashboarding/**
- **denormalise_table_query_fmcg.txt** → SQL query for creating a **denormalized table** for BI consumption.  
- **fmcg_dashboard.pdf** → Example dashboard showing unified analytics across both companies.  

### **resources/**
- **databricks_project.excalidraw** → Editable architecture diagram.  
- **project_architecture.png** → Visual representation of the pipeline (Bronze → Silver → Gold → BI).  

---

## 🏗️ Architecture
- **Bronze Layer** → Raw data ingestion into Amazon S3.  
- **Silver Layer** → Data cleaning, validation, and transformation with PySpark & SQL.  
- **Gold Layer** → Curated fact and dimension tables optimized for BI dashboards and analytics.  

---

## ⚙️ Tech Stack
- **Databricks (Lakehouse)** – Orchestration, catalog setup, pipeline execution  
- **Amazon S3** – Cloud storage for raw datasets  
- **PySpark & SQL** – Data transformation and fact/dimension table processing  
- **Genie** – Querying and advanced data exploration  
- **BI Tools** – Dashboards for stakeholders (Power BI / Tableau)

---

## 🚀 Features
- Raw data ingestion from cloud storage (Amazon S3)  
- Dimension and fact table creation with incremental + historical loads  
- Automated orchestration and monitoring of ETL jobs  
- Denormalized tables for faster querying  
- BI-ready datasets integrated with dashboards for decision-making  

---

## 📂 Project Structure

project-de-fmcg-atlikon/
│
├── 0_data/                     # Raw datasets (historical + incremental)
├── 1_codes/
│   ├── 1_setup/                 # Setup notebooks (catalog, date table, utilities)
│   ├── 2_dimension_data_processing/ # Dimension processing (customers, products, pricing)
│   └── 3_fact_data_processing/  # Fact table processing (full + incremental loads)
├── 2_dashboarding/              # Denormalized queries + dashboards
├── resources/                   # Architecture diagrams
└── README.md                    # Project overview
