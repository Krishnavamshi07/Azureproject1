# Azureproject1

# Azure End-to-End Data Engineering Project 

This project is an end-to-end data engineering pipeline built using Microsoft Azure.
The main goal of this project was to understand how data can be collected from a source, stored in a data lake, transformed using PySpark, and finally prepared for analytics and visualization.

I built this project while learning Azure Data Engineering concepts and working with services such as Azure Data Factory, Azure Data Lake Storage, Azure Databricks and Delta Lake.

---

##  Project Overview

In this project, I worked with **NYC Taxi trip data** and created a complete data pipeline on Azure.

The pipeline follows the **Medallion Architecture**, where data moves through three main layers:

**Bronze → Silver → Gold**

* **Bronze Layer** – Raw data
* **Silver Layer** – Cleaned and transformed data
* **Gold Layer** – Processed data ready for analysis

The project helped me understand how different Azure services can work together to build a complete data engineering workflow.

---

<img width="2760" height="1536" alt="Gemini_Generated_Image_qvmf47qvmf47qvmf" src="https://github.com/user-attachments/assets/7cbc6667-e482-4900-ab78-2377fc6492f5" />


## Architecture

```text
                    Data Source
                        │
                        ▼
              ┌──────────────────┐
              │ Azure Data        │
              │ Factory           │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Azure Data Lake  │
              │ Storage Gen2     │
              └────────┬─────────┘
                       │
                  Bronze Layer
                       │
                       ▼
              ┌──────────────────┐
              │ Azure Databricks │
              │     PySpark      │
              └────────┬─────────┘
                       │
                 Transformations
                       │
                       ▼
                  Silver Layer
                       │
                       ▼
                 Delta Tables
                       │
                       ▼
                   Gold Layer
                       │
                       ▼
                  ┌──────────┐
                  │ Power BI │
                  └──────────┘
```

---

##  Technologies Used

| Technology                       | Purpose                                   |
| -------------------------------- | ----------------------------------------- |
| **Azure Data Factory**           | Data ingestion and pipeline orchestration |
| **Azure Data Lake Storage Gen2** | Storing raw and processed data            |
| **Azure Databricks**             | Data processing and transformation        |
| **PySpark**                      | Distributed data processing               |
| **Delta Lake**                   | Reliable storage and versioning           |
| **Power BI**                     | Data visualization and reporting          |
| **Python**                       | Data processing and scripting             |

---

## Project Structure

```text
Azure-Data-Engineering-Project/
│
├── README.md
│
├── notebooks/
│   ├── data_ingestion.py
│   ├── data_transformation.py
│   └── data_analysis.py
│
├── pipelines/
│   └── azure_data_factory/
│
├── data/
│   └── sample_data/
│
├── screenshots/
│   ├── architecture.png
│   ├── data_factory.png
│   ├── databricks.png
│   └── powerbi.png
│
└── sql/
    └── queries.sql
```

---

#  Data Pipeline

## 1. Data Ingestion

The first step was to collect the NYC Taxi dataset and move the data into Azure Data Lake Storage.

I used **Azure Data Factory** to create the ingestion pipeline.

The pipeline is responsible for:

* Connecting to the data source
* Reading the required files/data
* Copying the data into Azure Data Lake
* Organizing the data inside the Bronze layer

---

## 2. Bronze Layer 🥉

The Bronze layer contains the **raw data**.

At this stage, I don't perform major transformations because the purpose of this layer is to keep the original data available for further processing.

Example:

```text
Data Source
     │
     ▼
Azure Data Factory
     │
     ▼
Azure Data Lake
     │
     ▼
Bronze
```

---

## 3. Data Processing with Databricks

After the raw data was stored in the Bronze layer, I used **Azure Databricks** to process the data.

PySpark was used for:

* Reading data from Azure Data Lake
* Checking the data
* Handling missing values
* Removing unnecessary records
* Changing data types
* Creating derived columns
* Performing aggregations
* Preparing data for the next layer

Example PySpark operations used in the project:

```python
from pyspark.sql.functions import col

df = spark.read.format("csv") \
    .option("header", "true") \
    .option("inferSchema", "true") \
    .load("path_to_data")

df = df.dropna()

df = df.withColumn(
    "total_amount",
    col("fare_amount") + col("tip_amount")
)
```

---

# 🥈 Silver Layer

The Silver layer contains the **cleaned and transformed data**.

Here, the raw data is converted into a more useful format.

Some of the transformations include:

* Data cleaning
* Data type conversion
* Removing invalid records
* Handling missing values
* Creating calculated columns
* Filtering unnecessary data
* Basic data analysis

The processed data is stored using **Delta format**.

---

# 🥇 Gold Layer

The Gold layer contains the final data that is ready for analytics.

At this stage, the data is more structured and focused on business/analytical requirements.

Examples of analysis that can be performed:

* Total number of trips
* Total revenue
* Average fare
* Trips by location
* Trips by time
* Payment type analysis
* Passenger analysis
* Revenue trends

The Gold layer can then be connected to a BI tool such as Power BI.

---

#  Delta Lake

I used **Delta Lake** to store the processed data.

Delta Lake provides features that are useful for reliable data pipelines, such as:

* ACID transactions
* Data versioning
* Schema management
* Time Travel
* Reliable updates
* Data history

For example, Delta tables can be queried using:

```python
df = spark.read.format("delta").load("path_to_delta_table")
```

One of the interesting features I explored was **Time Travel**, which allows previous versions of Delta tables to be accessed.

---

#  Medallion Architecture

The project follows the Medallion Architecture:

```text
                RAW DATA
                   │
                   ▼
          ┌─────────────────┐
          │     BRONZE      │
          │   Raw Data      │
          └────────┬────────┘
                   │
                   ▼
          ┌─────────────────┐
          │     SILVER      │
          │ Cleaned Data    │
          └────────┬────────┘
                   │
                   ▼
          ┌─────────────────┐
          │      GOLD       │
          │ Analytics Data  │
          └────────┬────────┘
                   │
                   ▼
                POWER BI
```

This architecture makes it easier to separate raw, processed and analytical data.

---

# 📊 Power BI

The final processed data can be connected to **Power BI** for visualization.

Possible dashboard metrics include:

* 🚕 Total Trips
* 💰 Total Revenue
* 📍 Trips by Location
* 💳 Payment Type
* 👥 Passenger Count
* 📅 Trips over Time
* 💵 Average Fare



#  Azure Security

During the project I also explored how Azure services can securely communicate with each other.

Some of the concepts covered include:

* Azure Entra ID
* Managed Identity
* Service Principals
* Authentication
* Access control
* Permissions for Azure Data Lake

These concepts are important because data pipelines should not rely on storing credentials directly inside notebooks or pipelines.

---

#  What I Learned

This project helped me understand the complete flow of a data engineering project rather than learning each technology separately.

### Azure

* Azure Resource Groups
* Azure Storage
* Azure Data Lake
* Azure Data Factory

### Data Engineering

* ETL pipelines
* Data ingestion
* Data transformation
* Pipeline orchestration
* Data validation

### Databricks

* Databricks workspace
* Clusters
* Notebooks
* PySpark
* Delta Tables

### Data Architecture

* Medallion Architecture
* Bronze/Silver/Gold layers
* Data Lake architecture

### Analytics

* Delta Lake querying
* Data analysis
* Power BI integration

---

# 🚧 Challenges I Faced

While building this project, I faced some issues with the Azure environment and connecting the different services.

Some of the main challenges were:

* Configuring Azure resources correctly
* Connecting Data Factory with Data Lake
* Setting permissions and authentication
* Connecting Databricks with Azure Storage
* Understanding PySpark transformations
* Working with Delta tables
* Managing Azure free/student resources

Solving these problems helped me understand the practical side of cloud data engineering.

---

#  Future Improvements

There are several things I would like to improve in the future:

* Add incremental data loading
* Automate the complete pipeline
* Add better data quality checks
* Add monitoring and logging
* Improve the Power BI dashboard
* Add CI/CD using Azure DevOps
* Implement more advanced transformations
* Explore real-time data processing
* Improve security using managed identities

---

#  Resources

I used the following resources while working on this project:

* Microsoft Azure documentation
* Azure Data Factory documentation
* Azure Databricks documentation
* Delta Lake documentation
* PySpark documentation

---

# 👨‍💻 About

This project was created as a **learning project to gain practical experience in Azure Data Engineering**.

I built it to understand how a real-world data pipeline works from data ingestion to transformation and analytics.

### Skills Practiced

`Azure` `Azure Data Factory` `Azure Data Lake` `Databricks` `PySpark` `Delta Lake` `ETL` `Data Engineering` `Power BI` `Python`

---

⭐ If you found this project useful, feel free to check out the repository and leave a star!
