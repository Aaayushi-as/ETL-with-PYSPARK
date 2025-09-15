# ETL with PySpark 🚀
A mid-level **data engineering project** that demonstrates building a production-style **ETL pipeline** using **PySpark, Apache Airflow, PostgreSQL, and Amazon Redshift**.  
The pipeline extracts transactional data from PostgreSQL, transforms it into a **star schema (dimensions + fact table)** using PySpark, and loads it into a warehouse for **analytics and BI use cases**.
---

## 📂 Repository Structure

ETL-with-PYSPARK/
├ README.md
├ docker-compose.yml # Lightweight Postgres setup
├ dags/
│ └ dvdrental_etl_dag.py                    # Airflow DAG: dims → fact orchestration
├ spark_apps/ # PySpark ETL scripts
│ ├ load_dim_customer.py
│ ├ load_dim_movie.py
│ ├ load_dim_store.py
│ ├ load_dim_staff.py
│ ├ load_fact_sales.py
│ └ postgresql-42.5.1.jar                  # JDBC driver
├ sql_scripts/                             # Schema definitions
│ ├ create_dim_customer.sql
│ ├ create_dim_movie.sql
│ ├ create_dim_store.sql
│ ├ create_dim_staff.sql
│ └ create_fact_sales.sql
└ config/
└ credentials_template.json              # Template for DB credentials



---

## ⚙️ Tech Stack

- **PySpark** – scalable ETL (Extract, Transform, Load)  
- **Apache Airflow** – workflow scheduling & orchestration  
- **PostgreSQL** – source database (dvdrental dataset)  
- **Amazon Redshift** – target data warehouse (cloud-ready)  
- **SQL** – schema creation & queries  
- **Docker** – containerized PostgreSQL instance  

---

## 🏗️ Architecture

**Workflow:**
1. **Extract** – Data is pulled from PostgreSQL with JDBC.  
2. **Transform** – PySpark scripts process raw tables into clean **dimensions** (`customer`, `movie`, `store`, `staff`,`sales`) and a **fact table** (`sales`).  
3. **Load** – Star schema tables are written into Amazon Redshift (or local Postgres as a warehouse).  
4. **Orchestrate** – Airflow DAG manages execution order: **dimensions → fact**.  

---


---

## Pipeline Logic
1. **Initialization**:  
   - Airflow DAG (`dvdrental_etl_dag.py`) initializes and defines the ETL workflow.  
   - PySpark session starts for distributed processing.  

2. **Extraction**:  
   - Source data is extracted from the PostgreSQL **dvdrental** database using JDBC.  

3. **Transformation**:  
   - PySpark scripts (`spark_apps/`) clean, join, and reshape the extracted data.  
   - Data is modeled into **dimensions** (`customer`, `movie`, `store`, `staff`) and a **fact table** (`sales`).  

4. **Loading**:  
   - Transformed star schema tables are loaded into Amazon Redshift (or PostgreSQL warehouse).  

5. **Orchestration**:  
   - Airflow schedules tasks in the correct order (dimension tables first, then fact table).  

---

## Problems Faced
- **Schema Alignment**: Ensuring dimension and fact scripts had consistent keys for joins.  
- **Connection Handling**: Managing PostgreSQL and Redshift connectivity through JDBC drivers.  
- **Workflow Failures**: Debugging Airflow DAG dependencies and retries.  
- **Large Data Volumes**: Optimizing PySpark jobs by partitioning and caching intermediate datasets.  

---








