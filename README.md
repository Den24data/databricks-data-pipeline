# Databricks Data Pipeline

## Project overview

A small, self-developed Data Engineering project demonstrating how retail order data can be ingested and transformed using Databricks, PySpark and Delta Lake.

The project was created as a practical learning exercise to gain hands-on experience with data pipelines, notebook development, GitHub integration and the Medallion Architecture.

## Architecture

**GitHub CSV → Bronze → Silver → Gold (planned)**

### Bronze – Data ingestion
- Reads synthetic retail order data from GitHub.
- Loads the dataset using Python and Spark.
- Stores the raw data in a Delta table in Databricks.

### Silver – Data transformation
- Reads data from the Bronze layer.
- Applies basic cleaning and transformation operations using PySpark.
- Writes the processed data to a Silver Delta table.

### Gold – Analytics (planned)
- Aggregate cleaned data into business-oriented datasets.
- Prepare data for reporting and analytical use cases.

## Technologies

- Databricks
- Python / PySpark
- Delta Lake
- Unity Catalog
- Databricks Workflows
- Git & GitHub

## Repository structure

```text
notebooks/
├── bronze/
│   └── 01_bronze_ingestion.ipynb
├── silver/
│   └── 02_silver_transformation.ipynb
└── README.md

README.md
syntetiske_butiksordrer_2026.csv
```

## Workflow orchestration

The project includes a Databricks Job configured with separate Bronze and Silver notebook tasks, where the Silver task depends on completion of the Bronze task.

## Project status

This is a learning and portfolio project under development. The repository contains the source data and notebooks. Execution takes place in a separate Databricks workspace.

## Next steps

- Implement the Gold layer.
- Add data quality validation.
- Extend automated pipeline execution and deployment.
- Improve documentation and error handling.
