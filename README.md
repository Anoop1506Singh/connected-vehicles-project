# Connected Vehicles Data Engineering Platform

## Project Overview

Built an end-to-end Azure Data Engineering solution to ingest, process, transform, and analyze connected vehicle telemetry data from multiple source systems using modern lakehouse architecture.

This project simulates how fleet/logistics organizations centralize vehicle sensor data for operational monitoring, reporting, and analytics.

---

## Business Problem Statement

Connected vehicles continuously generate telemetry data such as:

- Vehicle ID  
- GPS coordinates  
- Speed  
- Temperature  
- Event timestamps  
- Source system feed  

Organizations need a scalable platform to:

- Ingest data from multiple sources  
- Store raw historical records  
- Clean and standardize telemetry feeds  
- Build trusted analytical datasets  
- Generate business KPIs for fleet monitoring  

---

## Architecture

```text
GitHub Historical Feed        Mockaroo Live API
        │                           │
        └────────────┬──────────────┘
                     │
          Azure Data Factory (ADF)
                     │
               ADLS Gen2 Raw Layer
                     │
             Azure Databricks
                     │
      Bronze → Silver → Gold Layers
                     │
              Analytics / BI Layer
````

---

## Tech Stack

* Azure Data Factory
* Azure Data Lake Storage Gen2
* Azure Databricks
* PySpark
* Delta Lake
* Unity Catalog
* GitHub

---

## Source Systems

### 1. Historical Source

GitHub-hosted JSON files containing historical vehicle telemetry records.

### 2. Live Source

Mockaroo REST API generating recurring vehicle telemetry JSON feeds.

---

## Data Lake Design

```text
raw/
bronze/
silver/
gold/
archive/
```

---

## Medallion Architecture

### Bronze Layer

Purpose:

* Ingest raw source feeds
* Standardize schemas
* Add ingestion metadata
* Preserve source lineage

Output Table:

```text
dbx_connectedveh_dev.bronze.vehicle_data
```

---

### Silver Layer

Purpose:

* Remove duplicates
* Filter invalid speed values
* Validate coordinates
* Improve data quality

Output Table:

```text
dbx_connectedveh_dev.silver.vehicle_data
```

---

### Gold Layer

Business-ready aggregated KPI datasets.

#### Gold Tables

```text
dbx_connectedveh_dev.gold.city_kpi
dbx_connectedveh_dev.gold.vehicle_kpi
```

---

## KPIs Created

### City KPI

* Active vehicles by city
* Average speed by city
* Average temperature by city

### Vehicle KPI

* Total records by vehicle
* Average speed
* Maximum speed
* Maximum temperature

---

## ADF Pipelines

### Pipeline 1

```text
pl_ingest_github_json
```

Daily historical ingestion.

### Pipeline 2

```text
pl_ingest_mockaroo_json
```

15-minute recurring live API ingestion.

---

## Key Engineering Concepts Demonstrated

* Multi-source ingestion
* REST API integration
* Dynamic file naming
* Managed Identity authentication
* Medallion architecture
* Delta Lake storage
* PySpark transformations
* Catalog-based table management
* Layered analytics modeling

---

## Sample File Naming

```text
vehicle_history_20260418.json
vehicle_live_20260418_101526.json
```

---

## Project Outcomes

* Built scalable lakehouse architecture on Azure
* Automated ingestion from batch + API sources
* Produced analytics-ready KPI tables
* Implemented production-style data layering

---

## Future Enhancements

* Kafka / Event Hub streaming ingestion
* Incremental MERGE logic
* SCD Type 2 dimensions
* Window functions
* Performance tuning using OPTIMIZE / ZORDER
* Power BI dashboarding
* CI/CD deployment pipelines

---

## Repository Structure

```text
Connected-Vehicles-Data-Engineering/
│── README.md
│── architecture/
│── adf/
│── databricks/
│── notebooks/
│── sample-data/
│── screenshots/
```

---

## Author

Anoop Kumar Singh
Data Engineer Portfolio Project

```
```
