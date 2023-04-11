# Azure Databricks Optimization - Cost and Performance (WIP)

## 1. Delta Lake File Inventory Analysis

- Free-up storage space (cost reduction) by identifying Delta Lake Paths containing large number of abandoned files for Delta [Vacuum](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/delta-vacuum). 
- Identify Delta paths containing 'small files' where performance would be improved through small file coalescing with Delta [Optimize](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/delta-optimize). 

### 1.1 Run Blob Storage Inventory Report

Generate a .parquet inventory report file using the [Azure Blob inventory feature](https://learn.microsoft.com/en-us/azure/storage/blobs/blob-inventory). The report will need to capture the following fields  ***Name***, ***Content-Length*** and ***Access-Tier*** and should be written-out to a location accessible by Azure Databricks.

### 1.2 Generate Hierarchical Dataset from Inventory Report

Use the Databricks Notebook, [ADLS_Inventory_File_Process.ipynb](Databricks/ADLS_Inventory_File_Process.ipynb) , to process the blob inventory report for small file analysis and delta path clean-up analysis. 

***Notes***
- The provided Databricks Notebook uses [Azure Data Lake Gen2 Credential Passthrough](https://learn.microsoft.com/en-us/azure/databricks/data-governance/credential-passthrough/adls-passthrough#--azure-data-lake-storage-gen2), please update accordingly to match your existing authentication method in-order to load the inventory file. 