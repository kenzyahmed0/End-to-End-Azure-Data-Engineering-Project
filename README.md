# End-to-End Azure Data Engineering Project

## Project Overview

This project demonstrates an end-to-end data engineering solution using Microsoft Azure services and Apache Spark.

The project uses a retail business scenario with five datasets: Categories, Products, Sales, Stores, and Warranty.

The solution follows the Medallion Architecture (Bronze, Silver, and Gold) to organize, clean, transform, and analyze data.

## Architecture

The project uses the following technologies and services:

- Azure Data Factory (ADF) for data ingestion.
- Azure Data Lake Storage Gen2 (ADLS Gen2) for data storage.
- Azure Databricks for data processing.
- PySpark for data transformation and analysis.
- Microsoft Entra ID for identity and access management.

**Project Architecture:**

<img width="923" height="597" alt="image" src="https://github.com/user-attachments/assets/3d3d3733-b834-4c5d-891b-6d2c3df4a673" />


*Figure 1: End-to-end Azure data engineering architecture.*

## Dataset Description

The project uses five retail datasets:

| Dataset | Description |
|---|---|
| Categories | Product category information |
| Products | Product details |
| Sales | Retail sales transactions |
| Stores | Store information |
| Warranty | Warranty claims and repair status |

## Data Ingestion – Azure Data Factory

Azure Data Factory was used as part of the data ingestion process to transfer source data into Azure Data Lake Storage Gen2.

**ADF Pipeline:**

<!-- INSERT IMAGE: adf-pipeline.png -->

*Figure 2: Azure Data Factory pipeline.*

**Pipeline Execution:**

<!-- INSERT IMAGE: adf-monitor.png -->

*Figure 3: Pipeline execution monitoring, if available.*

## Data Lake Storage – Medallion Architecture

The data lake is organized into three layers:

- **Bronze:** Stores the raw source data.
- **Silver:** Stores cleaned and transformed data.
- **Gold:** Stores aggregated and analytics-ready datasets.

<!-- INSERT IMAGE: storage-containers.png -->

*Figure 4: Bronze, Silver, and Gold storage containers.*

## Bronze Layer – Raw Data

The source CSV files were read from the Bronze layer using PySpark in Azure Databricks.

The Sales dataset contains 1,040,200 records and five columns.

<!-- INSERT IMAGE: bronze-layer.png -->

*Figure 5: Reading and displaying raw data in Databricks.*

## Silver Layer – Data Cleaning and Transformation

The Silver layer applies data cleaning and preparation operations, including:

- Removing duplicate records.
- Filtering records with missing key values.
- Trimming unnecessary spaces from string columns.
- Applying data quality filters.
- Saving transformed datasets in Parquet format.

The transformations were applied to Categories, Products, Sales, Stores, and Warranty datasets.

<!-- INSERT IMAGE: silver-layer.png -->

*Figure 6: Silver layer transformations using PySpark.*

## Gold Layer – Business Aggregations

The Gold layer contains four analytical datasets created using PySpark aggregations and joins:

| Gold Dataset | Description | Rows |
|---|---|---:|
| product_sales | Sales metrics for each product | 89 |
| category_sales | Sales metrics by product category | 10 |
| store_sales | Sales metrics by store | 75 |
| warranty_analysis | Warranty claims grouped by repair status | 4 |

<!-- INSERT IMAGE: gold-layer.png -->

*Figure 7: Creating Gold analytical datasets.*

## Data Quality Checks

Data quality checks were performed to validate relationships between the datasets:

1. Checking sales records with missing product references.
2. Checking sales records with missing store references.
3. Checking products with missing category references.
4. Checking warranty claims with missing sales references.

<!-- INSERT IMAGE: data-quality.png -->

*Figure 8: Data quality validation using PySpark.*

## Gold Layer Validation

The four Gold datasets were read from Azure Data Lake Storage Gen2 and their record counts were validated.

Expected output:

```text
product_sales: 89 rows
category_sales: 10 rows
store_sales: 75 rows
warranty_analysis: 4 rows
```

<!-- INSERT IMAGE: gold-validation.png -->

*Figure 9: Gold datasets validation results.*

## Technologies Used

- Microsoft Azure
- Azure Data Factory
- Azure Data Lake Storage Gen2
- Azure Databricks
- Apache Spark
- PySpark
- Python
- Parquet
- Microsoft Entra ID

## Project Reference

This project was inspired by an Azure Data Engineering tutorial and extended with a Gold layer containing business-oriented analytical datasets.

Reference: [Azure Data Engineering Project – Source Repository](https://github.com/anarwade149/Azure-Data-Engineering-Project)

---

**Project Focus:** Building an end-to-end cloud data engineering workflow, from raw data ingestion to cleaned and analytics-ready datasets.
