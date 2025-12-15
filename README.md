#  E-commerce Funnel Analysis — Electronics Store

##  Project Overview
This project performs an end-to-end **funnel analysis** on large-scale e-commerce event data from an electronics store.  
The objective is to understand **user behavior across the purchase funnel**, identify **drop-off points**, and build **reusable analytical datasets** for further analysis such as churn, retention, and CLV.

The project mirrors real-world **data engineering and analytics workflows**, using **Snowflake, Python, Parquet, and Quarto** to handle large volumes of data efficiently.

---

## Dataset Information

- **Source:** Kaggle  
- **Dataset:** *E-commerce Events History – Electronics Store*  
- **Time Period:** October 2019 – February 2020 (~5 months)  
- **Raw Data Size:** ~2.4 GB (CSV files)  
- **Granularity:** Event-level user interactions  


## Project Workflow

### 1️⃣ Data Optimization (Python)
- Converted raw CSV files to **Parquet** format.
- Reduced storage size by ~**85%**.
- Improved ingestion and query performance in Snowflake.

---

### 2️⃣ Data Ingestion & ETL (Snowflake)
An end-to-end ETL pipeline was built using layered data modeling:

#### 🔹 Staging Layer
- Loaded Parquet files using Snowflake stages.
- Standardized schemas and timestamps.

#### 🔹 Transformation Layer
- Deduplicated events using window functions.
- Cleaned and standardized price and timestamp fields.
- Created behavioral flags (viewed, carted, purchased).

#### 🔹 Analytics Layer
Final enriched tables were created at multiple **levels of detail**:
- Product-level  
- Session-level  
- User-level  

These tables support funnel, conversion, churn, and retention analyses.

---

### 3️⃣ Data Cleanup & Normalization (Python)
- Extracted cleaned data from Snowflake (`.gz` format).
- Replaced Snowflake-specific null markers (`\N`) with proper NULLs.
- Converted timestamps from string format to datetime.
- Normalized timezones for consistency.

---

### 4️⃣ Funnel Analysis
Primary funnel analyzed:

**Users → Product Views → Cart Additions → Purchases**

Key findings:
- Largest drop-off occurs between **product views and cart additions**.
- Cart-to-purchase conversion is comparatively higher.
- User-level behavior reveals strong repeat-purchase patterns.

---

### 5️⃣ Visualization (Quarto)
- Built interactive dashboards using **Quarto + Plotly**.
- Exported as **HTML** for easy sharing.
- Chosen over Tableau Public due to large data volume.

---

## Repository Structure

```text
.
├── data/
│   ├── parquet/               # Parquet-converted files
│
├── sql/
│   ├── staging.sql            # Raw ingestion
│   ├── transformations.sql   # Cleansing & enrichment
│   ├── final_tables.sql      # Analytics-ready tables
│
├── python/
│   ├── csv_to_parquet.py     # CSV → Parquet conversion
│   ├── snowflake_extract.py  # Extract & clean .gz files
│   ├── timezone_fix.py       # Timestamp normalization
│
├── visualization/
│   ├── funnel_analysis.qmd   # Quarto dashboard
│
└── README.md
