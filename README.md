# Mini-ETL-Pipeline-on-Databricks-Incremental-Loads-with-Auto-Loader
##  Project Overview
This project demonstrates how to build a **modular ETL pipeline** on Databricks using:
- Auto Loader for **incremental ingestion**
- Lookup validation using **Azure SQL Database**
- Data enrichment and transformation
- Aggregation and reporting
- End-to-end orchestration using Lakeflow Jobs
## 🏗️ Pipeline Architecture

Raw (Bronze) → Validation (Silver) → Transformation (Silver) → Aggregation (Gold)


---

##  1. Ingestion
- Ingest raw sales data using Auto Loader (`cloudFiles`).
- Schema inference + checkpointing for incremental loads.
- Written to **Bronze Delta table**.

##  2. Validation
- JDBC connection to Azure SQL for customer and product lookups.
- Validations:
  - Quantity > 0
  - Price > 0
  - CustomerID exists in lookup
  - ProductID exists in lookup
- Split data into good and bad records.
- Added `rejection_reason`.
- Generated summary report for bad data.

## 3. Transformation
- Computed `TotalAmount`.
- Joined with lookup tables to enrich data.
- Written to Silver layer.

## 4. Aggregation
- Top 3 customers by total amount
- Total sales by category and state
- Daily total revenue trend
- Written to Gold layer.

##  5. Orchestration
- Created **Lakeflow Job** to chain:
  - `ingest.py`
  - `validation.py`
  - `transformation.py`
  - `aggregation.py`
- Verified **incremental load** using Auto Loader (300 → 450 records).

---

##  Key Concepts Covered
- Auto Loader & incremental streaming
- Data validation against lookup tables
- Error handling & rejection reports
- Modular pipeline design
- Aggregation & reporting
- Databricks Lakehouse architecture

---

##  Tech Stack
- Azure Databricks
- Delta Lake
- Azure SQL Database
- PySpark
- Auto Loader
- Lakeflow Jobs
- Azure Data Factory (for lookup table loading)


🐙 GitHub: [Your GitHub URL]
