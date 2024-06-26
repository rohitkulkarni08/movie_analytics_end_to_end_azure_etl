# End-to-End ETL Pipeline with Microsoft Azure for IMDb Movie Rating Dataset

## Overview

This project focuses on building a comprehensive Extract, Transform, and Load (ETL) pipeline leveraging the robust functionalities of Microsoft Azure. The pipeline is designed to efficiently fetch data from Azure Blob Storage perform necessary transformations using Azure Databricks and Azure Data Factory, store it in Azure Data Lake and finally store the analyzed data in a SQL layer for further use. This end-to-end solution aims to streamline the data processing workflow and provide actionable insights from the transformed data.

## Dataset and Analysis

The [Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) used in this project contains information for over 45,000 movies with 26 million ratings! Since this is primarily a Data Engineering project, we'll only be focusing on one of the datasets "movies-metadata" which contains information such as budget, revenue, release dates, languages, production countries and companies

### Analysis #1: Language Analysis

We perform language-based analysis on a movie dataset, focusing on non-numeric original language entries. We generate a summary dataframe that includes the number of movies, average budget, average revenue, and average popularity for each language. This analysis helps in understanding the impact of the original language on various movie metrics

### Analysis #2: Release Date Analysis

We analyze movies released after 1995 in the dataset. We calculate the number of movies released per year and perform a genre analysis to identify the top 5 genres for each year. The final output summarizes the number of movies released and the top 5 genres for each year post-1995

### Analysis #3: Genre Analysis

We conduct a comprehensive analysis of movie genres in the dataset. We calculate the distribution of genres and aggregates the average budget, revenue, rating, and popularity for each genre. The final output summarizes the average budget, revenue, rating, popularity, and the number of movies for each genre, providing insights into the characteristics and trends of different movie genres

## Prerequisites

1. **Microsoft Azure subscription**
2. **Azure Blob Storage**: Object storage service for storing large amounts of unstructured data
3. **Azure Data Lake Gen2 Storage**: Scalable storage for big data analytics
4. **Azure Databricks**: Analytics platform based on Apache Spark for big data processing and machine learning
5. **Azure SQL Server**: Fully managed relational database service with SQL Server engine
6. **Azure SQL Database**: Managed relational database with SQL Server compatibility
7. **Azure Data Factory**: Data integration service that enables you to create, schedule, and orchestrate ETL and ELT workflows. ADF provides a visually intuitive interface to build data-driven workflows for orchestrating data movement and transforming data at scale


<img src="https://github.com/rohitkulkarni08/Azure-ETL-Pipeline-MovieAnalytics/blob/a0e8db3a6c03ef87bdfc023cd12e7c31da40ff17/images/azure_resource_group.png" width="1100" height="550">

## Data flow:

1. **Extract Data**: Retrieve CSV data from Azure Blob Storage for processing
2. **Transform Data**: Utilize Python and PySpark on Azure Databricks to analyze and process the data, storing the results in Azure Data Lake Storage Gen2
3. **Load Data**: Transfer the processed data into an Azure SQL database to establish a reporting layer for dashboard creation
4. **Automation**: Construct end-to-end pipelines in Azure Data Factory to automate the data flow from extraction to reporting layers

<div style="text-align:center;">
  <img src="https://github.com/rohitkulkarni08/Azure-ETL-Pipeline-MovieAnalytics/blob/808ba18def5693ef899c34b535315e0faf1bd159/images/Flow.png" width = "900" height = "500">
</div>

## Setup and Configuration

### Azure Blob Storage
1. Create a container in your Azure Blob Storage account
2. Upload your input data files to the container

### Azure Data Lake Storage
1. Create a file system in your Azure Data Lake Storage account
2. Create a directory in the file system to store the processed Parquet files

### Azure Databricks
1. Create and configure a cluster with the necessary dependencies and settings for Python and PySpark.
2. In our case, I have used created a cluster with the configuration: 9.1 LTS (includes Apache Spark 3.1.2, Scala 2.12)
3. Create a new notebook in your Azure Databricks workspace

#### Azure SQL Database
1. Create a SQL database in Azure
2. Create the necessary tables in the database to store the processed data

#### Azure Data Factory
1. Create a new pipeline in your Azure Data Factory instance
2. Create a link service for each of the Azure functionalities used. I have created a Linked Service for: Azure Blob Storage, Azure Data Lake Gen2 Storage, Azure Databricks, and Azure SQL
3. Add activities to the pipeline for each step of the workflow:
   a. Data processing in Azure Databricks
   b. Data copy from Azure Data Lake Storage to Azure SQL Database

<div style="text-align:center;">
  <img src= "https://github.com/rohitkulkarni08/Azure-ETL-Pipeline-MovieAnalytics/blob/808ba18def5693ef899c34b535315e0faf1bd159/images/adf_pipeline.png" width = "600" height = "400">
</div>

4. Running the Pipeline:
   a. Trigger the pipeline run in Azure Data Factory
   b. Monitor the pipeline run to ensure that each step completes successfully

<img src= "https://github.com/rohitkulkarni08/Azure-ETL-Pipeline-MovieAnalytics/blob/808ba18def5693ef899c34b535315e0faf1bd159/images/adf_pipeline_run.png">

By the end of it all, we have a fully automated ETL pipeline that fetches the data from blob, transforms the data and generates the necessary insights and loads it to the reporting layer :)
