## Overview

This project demonstrates a robust data engineering pipeline tailored for e-commerce analytics. It ingests raw data (both batch and streaming) into ADLS Gen2, processes it through the Medallion Layers in Databricks, and outputs curated datasets with automated dashboards reflecting any new data arrival.

Key objectives:

- Scalable ingestion for static and streaming e-commerce datasets.  
- Clean, enriched, and performance-optimized data layers.  
- Fully automated orchestration and dashboard refresh.  

---

## Architecture & Technology Stack

| Component            | Technology / Description                        |
|----------------------|--------------------------------------------------|
| Cloud Storage         | **Azure Data Lake Storage Gen2 (ADLS Gen2)**     |
| Compute & Analytics   | **Azure Databricks** with Spark notebooks        |
| Medallion Layers      | Bronze (raw) → Silver (cleaned/enriched) → Gold (business-ready) |
| Streaming             | Structured Streaming + stream partitioning logic |
| Orchestration         | Notebook pipeline automation (e.g. using Databricks Jobs) |
| Visualization         | Automated dashboards (e.g., via Databricks or integrated BI) |
| version control         | Databricks Github Repos |


---

## Pipeline Structure & Notebooks

The notebooks encapsulate each Medallion layer and related processes:

- **`Bronze.ipynb`**  
  Ingests raw e-commerce data from sources (e.g., logs, transactional files) and stores it in the Bronze layer in ADLS.

- **`Silver.ipynb`**  
  Applies data cleaning, validation, and transformation—resolving schema inconsistencies and standardizing formats.

- **`Gold.ipynb`**  
  Performs business aggregations, feature engineering, and readies data for analytics and dashboards.

- **`Stream Data Partitioning.ipynb`**  
  Handles streaming data ingestion, partitioning, watermarking, and writes to the appropriate Medallion layer efficiently.

- **`reader_factory.ipynb`**  
  Contains modular read logic to consume from Bronze/Silver/Gold layers abstractly, boosting reusability.

- **`Dashboard Notebook.ipynb`**  
  Generates visual analytics dashboards (e.g. sales trends, customer behavior, KPIs). Designed to re-run automatically when new data arrives.

---

## Getting Started

### Prerequisites

- Azure account with **ADLS Gen2** and **Databricks** workspace.  
- Access credentials for the storage and workspace.  
- Basic knowledge of Spark and Databricks notebooks.

### Setup Steps

1. Clone this repository:
   ```bash
   git clone https://github.com/sathvikrao7/Ecommerce.git
   cd E-Commerce-use-case

2. In Databricks:

   * Create a new workspace or use an existing one.
   * Upload the notebooks into a structured folder (e.g., `/ECommercePipeline/`).

3. Configure notebook parameters:

   * Set ADLS connection strings, container names, and access keys.
   * Define notebook paths for downstream orchestration.

4. Test pipeline manually:

   * Run in sequence: Bronze → Silver → Gold.
   * Run the streaming notebook and validate streaming writes.
   * Execute the Dashboard notebook and inspect visual outputs.


## Automated Dashboard Flow

To ensure dashboards stay updated with new data:

* Define a **Databricks Job** or **Workflow** with ordered task steps:

  1. `Bronze.ipynb`
  2. `Silver.ipynb`
  3. `Gold.ipynb`
  4. `Stream Data Partitioning.ipynb`
  5. `Dashboard Notebook.ipynb`

* Schedule this pipeline on a trigger (daily, hourly, or based on data arrival events).

* Once executed, dashboards are automatically regenerated with the latest data visualizations.



## Visual Samples 

*(Incorporate here: static image snapshots or links to dashboards showcasing key metrics such as sales trends, user activity, etc.)*



## Deployment & Scheduling

* **Jobs API / Databricks Workflows**: Orchestrate steps using job chaining and parameter passing.
* **Trigger Mechanisms**:

  * **Time-based** (CRON jobs via Databricks)
  * **Event-based** (e.g., ADLS file arrival notifications using Azure Event Grid or Functions)

---


