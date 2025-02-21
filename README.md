# AirBnB CDC Ingestion Pipeline

## Overview

This project implements a Change Data Capture (CDC) ingestion pipeline for AirBnB data using Azure services. The pipeline extracts data from CosmosDB, transforms it using Azure Data Factory, and loads it into Azure Synapse Analytics for analysis.

## Tech Stack

* **Azure**:
    * Data Lake Storage (ADLS)
    * CosmosDB
    * Data Factory
    * Synapse Analytics
* **Programming Languages**:*
    * SQL
    * Python (for potential custom transformations or utilities)

## Architecture

The architecture of this pipeline is as follows:

1.  **Data Extraction**: AirBnB data is extracted from CosmosDB using the Change Feed feature.
2.  **Data Transformation**: Azure Data Factory is used to orchestrate the pipeline and perform data transformations, including:
    * Data quality checks
    * Data type conversions
    * Data enrichment
3.  **Data Loading**: Transformed data is loaded into Azure Synapse Analytics dedicated SQL pool for analysis and reporting.

## Pipeline Steps

The Azure Data Factory pipeline consists of the following steps:

1.  **LoadCustomerDim Pipeline**:*
    * Extracts customer data from ADLS Gen2.
    * Upserts data into the `customer_dim` table in Azure Synapse Analytics.
    * Archives the raw data file.
2.  **LoadBookingsFact Pipeline**:*
    * Extracts booking data from CosmosDB.
    * Performs data transformations using a Data Flow activity.
    * Loads data into the `bookings_fact` table in Azure Synapse Analytics.
    * Triggers a stored procedure to aggregate booking data.
3.  **AirBnBCDCPipeline**:*
    * Orchestrates the `LoadCustomerDim` and `LoadBookingsFact` pipelines.

## Snapshots

* **ADF Pipeline Snapshots**:*
    * [LoadCustomerDim Pipeline](snaps/AIRBNB-1.PNG)
    * [LoadBookingsFact Pipeline](snaps/AIRBNB-2.PNG)
    * ![Alt text](AIRBNB-3.PNG)
    * [AirBnBCDCPipeline](snaps/AIRBNB-4.PNG)

## Deployment

To deploy this pipeline:

1.  **Prerequisites**:*
    * Azure subscription with necessary resources (ADLS, CosmosDB, Data Factory, Synapse Analytics).
    * Required permissions to access and modify these resources.
2.  **Deployment Steps**:*
    * Create linked services in Azure Data Factory to connect to ADLS, CosmosDB, and Synapse Analytics.
    * Create datasets in Azure Data Factory to define the data sources and destinations.
    * Configure the pipeline activities and data flow transformations in Azure Data Factory.
    * Deploy the pipeline and schedule it to run at desired intervals.

## Usage

1.  **Data Ingestion**: The pipeline will automatically ingest and process new AirBnB data based on the configured schedule.
2.  **Data Analysis**: Use Azure Synapse Analytics to query and analyze the ingested data for insights and reporting.



## Contributing

Contributions to this project are welcome. Please submit a pull request with your changes.

