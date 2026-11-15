# Databricks Data Pipeline

## Project overview

A small, self-developed Data Engineering project demonstrating how retail order data can be ingested, cleaned, validated and aggregated using Databricks, PySpark and Delta Lake.

The project was created as a practical learning exercise to gain hands-on experience with data pipelines, notebook development, GitHub integration, workflow orchestration and the Medallion Architecture.

## Architecture

**GitHub CSV → Bronze → Silver → Gold**

The pipeline follows the Medallion Architecture, separating raw data ingestion, data cleaning and business-level aggregations into three layers.

### Bronze – Data ingestion
- Reads synthetic retail order data from a CSV file hosted on GitHub.
- Loads the dataset using Python, Pandas and Spark.
- Stores the raw data in a Bronze Delta table.

### Silver – Data transformation
- Reads data from the Bronze layer.
- Removes duplicate rows and completely empty records.
- Trims whitespace and converts empty text fields to NULL.
- Replaces missing store names with "Ukendt" (Unknown).
- Converts and validates order dates, excluding records with invalid or missing dates.
- Stores the cleaned data in a Silver Delta table.
- Performs data quality checks, including NULL counts, duplicate detection and unknown store counts.

### Gold – Data aggregation
- Reads cleaned order data from the Silver layer.
- Calculates revenue after discounts.
- Aggregates revenue by store and month.
- Calculates the number of distinct orders and total units sold.
- Stores the aggregated results in a Gold Delta table for analytical use.

## Technologies

- Databricks
- Python / PySpark
- Pandas
- Delta Lake
- Unity Catalog
- Databricks Workflows
- Git & GitHub

## Repository structure

```text
databricks-data-pipeline/
├── notebooks/
│   ├── bronze/
│   │   └── 01_bronze_ingestion.ipynb
│   ├── silver/
│   │   └── 02_silver_transformation.ipynb
│   └── gold/
│       └── 03_gold_aggregation.ipynb
├── syntetiske_butiksordrer_2026.csv
└── README.md
```

## Workflow orchestration

The project includes a Databricks Workflow named `retail_orders_etl_job`, which orchestrates the complete pipeline using three dependent notebook tasks:

1. **bronze_ingestion** – Ingests raw retail order data.
2. **silver_transformation** – Cleans and validates the data.
3. **gold_aggregation** – Creates aggregated datasets for analytical use.

Each task depends on the successful completion of the previous task.

The complete workflow has been successfully executed using Databricks Serverless compute.

## Data quality

Basic data quality validation is implemented in the Silver layer.

The validation includes:
- Total row count.
- NULL values per column.
- Duplicate row count.
- Number of records with unknown store names.

Missing customer IDs are preserved because orders may still be valid without an identified customer.

## Project status

**Status: Functional end-to-end pipeline**

The Bronze, Silver and Gold layers have been implemented and successfully executed through Databricks Workflows.

The repository contains the source data and notebooks. Execution takes place in a separate Databricks workspace.

This remains a learning and portfolio project, with opportunities for further development.

## Next steps

- Implement automated data quality tests with failure conditions.
- Add logging and monitoring for pipeline execution.
- Improve handling and tracking of rejected records.
- Explore incremental data processing.
- Improve error handling and deployment automation.
