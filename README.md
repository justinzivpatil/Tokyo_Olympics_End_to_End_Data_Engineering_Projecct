

```markdown
# Tokyo Olympics Data Engineering Project

This project demonstrates an end-to-end data engineering solution for analyzing Tokyo Olympics data using Microsoft Azure services. It involves data ingestion, transformation, and analysis using Azure Blob Storage, Azure Data Factory, Azure Databricks, and Synapse Analytics.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Tools and Services Used](#tools-and-services-used)
3. [Setup Steps](#setup-steps)
4. [How to Run the Project](#how-to-run-the-project)
5. [Folder Structure](#folder-structure)
6. [Authors](#authors)

---

## Introduction
The goal of this project is to create a seamless data pipeline to:
- Ingest raw data related to the Tokyo Olympics.
- Transform the data into a structured format.
- Store, query, and analyze the data using Azure Synapse Analytics.

---

## Tools and Services Used
- **Azure Blob Storage**: For storing raw and transformed data.
- **Azure Data Factory**: For data ingestion and transformation.
- **Azure Databricks**: For advanced data processing using PySpark.
- **Azure Synapse Analytics**: For data analysis and visualization.
- **Python**: For scripting and data transformations.

---

## Setup Steps

### 1. Create a Resource Group
- Log in to the [Azure Portal](https://portal.azure.com).
- Create a resource group with the name `Tokyo_Olympics`.

### 2. Create a Storage Account
- Create a storage account under the resource group.
- Set up two containers: `raw_data` and `transformed_data`.

### 3. Upload Data
- Upload raw datasets into the `raw_data` container.
- Create a dummy file in `transformed_data`.

### 4. Set Up Azure Data Factory
- Create a Data Factory in the resource group.
- Build a pipeline for data ingestion using Copy Data activity.
- Source data from Azure Blob Storage and store it in the `transformed_data` container.

### 5. Configure Azure Databricks
- Deploy an Azure Databricks workspace.
- Set up a cluster with required configurations.
- Mount the storage container using the following script:

```python
configs = {
    "fs.azure.account.auth.type": "OAuth",
    "fs.azure.account.oauth.provider.type": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
    "fs.azure.account.oauth2.client.id": "<CLIENT_ID>",
    "fs.azure.account.oauth2.client.secret": "<CLIENT_SECRET>",
    "fs.azure.account.oauth2.client.endpoint": "https://login.microsoftonline.com/<TENANT_ID>/oauth2/token"
}

dbutils.fs.mount(
    source="abfss://tokyo1olympicdata@<STORAGE_ACCOUNT_NAME>.dfs.core.windows.net",
    mount_point="/mnt/tokyoolympicdata",
    extra_configs=configs
)
```

### 6. Analyze Data Using PySpark
- Load datasets using PySpark.
- Perform transformations and aggregations as needed.
- Save transformed data back to `transformed_data`.

### 7. Set Up Azure Synapse Analytics
- Create a Synapse workspace.
- Connect to the transformed data in Blob Storage.
- Use SQL to analyze the data.

---

## How to Run the Project

1. **Prepare Azure Services**:
   - Ensure all Azure resources are set up as described above.

2. **Ingest and Transform Data**:
   - Use Azure Data Factory pipelines to move raw data to transformed data.

3. **Process Data in Databricks**:
   - Use Databricks notebooks to clean and process data.

4. **Analyze Data in Synapse Analytics**:
   - Query the processed data using Synapse SQL.

---

## Folder Structure

```plaintext
root/
├── raw_data/                 # Contains raw datasets
├── transformed_data/         # Contains transformed datasets
├── databricks_notebooks/     # Contains Databricks PySpark notebooks
└── sql_queries/              # Contains SQL scripts for data analysis
```

---

