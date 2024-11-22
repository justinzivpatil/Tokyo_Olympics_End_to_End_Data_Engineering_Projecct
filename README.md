# Tokyo Olympics: End-to-End Data Engineering and Analytics Project

This project focuses on building an end-to-end data pipeline to analyze and visualize Tokyo Olympics data using Microsoft Azure services. It involves processing datasets related to athletes, events, and medals to derive actionable insights.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Technologies Used](#technologies-used)
- [Features](#features)
- [Data Pipeline Workflow](#data-pipeline-workflow)
- [Insights Delivered](#insights-delivered)
- [Setup Instructions](#setup-instructions)
- [Key Learnings](#key-learnings)
- [Acknowledgments](#acknowledgments)

---

## Project Overview
The Tokyo Olympics Data Project aims to create a robust data pipeline for analyzing datasets related to athletes, events, and medals. By leveraging cloud-based tools, the project processes raw data into structured, actionable insights and provides visualization through dashboards.

---

## Technologies Used
- **Cloud Platform**: Microsoft Azure
- **Storage**: Azure Data Lake Storage Gen2
- **Data Ingestion**: Azure Data Factory
- **Data Processing**: Azure Databricks and PySpark
- **Data Analytics**: Azure Synapse Analytics
- **Visualization**: Power BI
- **Programming Language**: Python (PySpark)

---

## Features
- **Comprehensive Data Pipeline**: Handles ingestion, transformation, and loading of Tokyo Olympics datasets.
- **Scalable Processing**: Processes large datasets with Azure Databricks.
- **Secure Data Management**: Sensitive data is anonymized and masked.
- **Real-Time Insights**: Power BI dashboards provide dynamic visualizations.

---

## Data Pipeline Workflow
1. **Data Ingestion**:
   - Raw datasets related to Tokyo Olympics are uploaded to Azure Data Lake Gen2.
   - Data Factory pipelines move raw data to a `processed_data` container.

2. **Data Processing**:
   - Cleaning and transformation are done in Azure Databricks.
   - Key processing includes:
     - Removing duplicate and null records.
     - Aggregating metrics like total medals by country and sport.
     - Anonymizing athlete personal data.

3. **Data Analytics**:
   - Transformed data is analyzed using SQL scripts in Azure Synapse Analytics.
   - Queries are run to calculate metrics like top-performing countries, medal counts, and event trends.

4. **Data Visualization**:
   - Processed data is visualized using Power BI dashboards, focusing on medal trends, athlete performance, and event analysis.

---

## Insights Delivered
1. **Medal Trends**:
   - Total medal counts by year and country.
   - Distribution of gold, silver, and bronze medals.
2. **Athlete Performance**:
   - Top-performing athletes and their contribution to medal tallies.
   - Age and gender distribution of athletes.
3. **Event Insights**:
   - Popular sports based on participation.
   - Regional dominance in specific events.

---

## Setup Instructions

### Azure Resource Setup
1. **Create a Resource Group**:
   - Set up a resource group in the Azure Portal named `Tokyo_Olympics`.
2. **Storage Account**:
   - Create an Azure Data Lake Gen2 account with hierarchical namespace enabled.
   - Create containers for `raw_data` and `processed_data`.
3. **Data Factory**:
   - Build a pipeline to ingest raw data into Azure Data Lake.
   - Schedule the pipeline for recurring updates.
4. **Databricks Workspace**:
   - Set up a Databricks workspace and cluster.
   - Mount Azure Data Lake using the following script:

     ```python
     configs = {
         "fs.azure.account.auth.type": "OAuth",
         "fs.azure.account.oauth.provider.type": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
         "fs.azure.account.oauth2.client.id": "<CLIENT_ID>",
         "fs.azure.account.oauth2.client.secret": "<CLIENT_SECRET>",
         "fs.azure.account.oauth2.client.endpoint": "https://login.microsoftonline.com/<TENANT_ID>/oauth2/token"
     }

     dbutils.fs.mount(
         source="abfss://tokyoolympicdata@<STORAGE_ACCOUNT_NAME>.dfs.core.windows.net",
         mount_point="/mnt/tokyoolympicdata",
         extra_configs=configs
     )
     ```


## Key Learnings
- Building end-to-end data pipelines with Azure.
- Using PySpark for large-scale data transformation.
- Visualizing complex datasets with Power BI.
- Optimizing pipelines for scalability and performance.
