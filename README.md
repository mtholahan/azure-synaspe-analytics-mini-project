# Azure Synaspe Analytics Mini Project


## 📖 Abstract
This project demonstrates how to build a data ingestion and transformation pipeline in Azure Synapse Analytics, integrating data lake storage with a dedicated SQL pool. The objective was to load product data from a CSV file in Azure Data Lake Storage Gen2 into a relational data warehouse table (dbo.DimProduct) using Synapse pipelines and data flows.

The workflow began with provisioning an Azure Synapse workspace and linked services, then creating datasets for both the source (Product.csv in ADLS) and destination (DimProduct in the SQL pool). Within Synapse Studio, I designed a pipeline with a data flow that included:

* A source transformation to ingest the CSV product data.

* A lookup transformation to match incoming Product IDs against existing warehouse records.

* An alter row transformation to classify records for insert vs. upsert.

* A sink transformation to load results into the warehouse, with schema mapping applied.

The pipeline was debugged with a staging cluster, published, and executed through Synapse Studio’s monitoring interface. The final run successfully upserted and inserted product records into the DimProduct table.

Through this project, I gained practical experience in Azure Synapse data integration, data lake ingestion, slowly changing dimension handling, and pipeline monitoring, strengthening cloud-native ETL skills relevant to enterprise data warehousing.



## 🛠 Requirements
- Azure subscription with admin access
- Azure Synapse Analytics workspace
- Azure Data Lake Storage Gen2 linked to Synapse
- Dedicated SQL pool provisioned and online
- Azure Cloud Shell (PowerShell) for setup script



## 🧰 Setup
- Clone Microsoft DP-203 GitHub repo in Azure Cloud Shell
- Run setup.ps1 script in lab 10 folder to provision Synapse workspace + resources
- Start dedicated SQL pool in Synapse Studio
- Verify linked Azure Data Lake Storage Gen2 container with Product.csv file



## 📊 Dataset
- Source: Product.csv in Azure Data Lake Storage Gen2
- Destination: dbo.DimProduct table in Synapse SQL pool
- Schema includes: ProductID, ProductName, Color, Size, ListPrice, Discontinued



## ⏱️ Run Steps
- Open Synapse Studio
- Create pipeline "Load Product Data"
- Add data flow with:
  - Source: Product.csv (DelimitedText dataset)
  - Source: dbo.DimProduct (SQL pool dataset)
  - Lookup to match ProductID vs ProductAltKey
  - Alter Row for InsertIf/UpsertIf logic
  - Sink: DimProduct table with Allow Insert + Upsert
- Debug pipeline with Data flow debug
- Publish and trigger pipeline run
- Verify rows in dbo.DimProduct with SELECT TOP 100



## 📈 Outputs
- Updated dbo.DimProduct table in SQL pool
- Inserted new products from Product.csv
- Upserted existing products (slowly changing dimension type 1)



## 📸 Evidence

![synapse_pipeline.png](./evidence/synapse_pipeline.png)  
Screenshot of pipeline orchestration view

![pipeline_run.png](./evidence/pipeline_run.png)  
Screenshot of successful pipeline run




## 📎 Deliverables

- [`- Synapse pipeline JSON exports in /deliverables/`](./deliverables/- Synapse pipeline JSON exports in /deliverables/)

- [`- Screenshots of pipeline run UI`](./deliverables/- Screenshots of pipeline run UI)

- [`- README with setup and execution notes`](./deliverables/- README with setup and execution notes)




## 🛠️ Architecture
- Synapse pipeline encapsulating data flow
- Source: Data Lake Gen2 (CSV)
- Destination: Synapse SQL Pool table
- Logic: Lookup + Insert/Upsert with Alter Row



## 🔍 Monitoring
- Use Synapse Studio Monitor tab to view pipeline runs
- Status: succeeded/failed
- Data preview in Data Flow debug mode



## ♻️ Cleanup
- Delete Azure resource group dp-203-xxxxx to remove Synapse workspace, SQL pool, and storage
- Avoids ongoing Azure charges



*Generated automatically via Python + Jinja2 + SQL Server table `tblMiniProjectProgress` on 09-14-2025 23:37:22*