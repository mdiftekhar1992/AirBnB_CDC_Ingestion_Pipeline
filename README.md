# AirBnB_CDC_Ingestion_Pipeline
Data Workflow for "AirBnB CDC Ingestion Pipeline"
1. Data Source: Ingesting Customer Data from ADLS
Input: Customer data stored in Azure Data Lake Storage (ADLS).
Process:
Azure Data Factory (ADF) triggers hourly data ingestion from ADLS.
ADF performs Slowly Changing Dimension (SCD-1) to update the customer_dim table in Azure Synapse.
Output: Updated customer_dim table in Synapse.
2. Data Source: Reading Bookings CDC Events from CosmosDB
Input: CDC (Change Data Capture) events from CosmosDB.
Process:
ADF connects to CosmosDB using change feed to capture inserts, updates, and deletes in real-time.
Data is fetched as incremental updates.
Output: Real-time CDC data in ADF pipeline for further processing.
3. Data Transformation on Bookings CDC Events
Input: Incremental CDC data from CosmosDB change feed.
Process:
Use ADF’s Data Flow feature for data transformation (e.g., formatting, validation, and enrichment).
Prepare data for the target schema in Synapse.
Output: Transformed booking event data ready for upserts.
4. Data Loading and Upsert Operations in Synapse
Input: Transformed data from ADF pipeline.
Process:
Perform Upsert (Insert or Update) operations on the target table in Synapse.
Ensure no duplicates and consistent data integrity.
Output: Synapse table updated with the latest booking events.
5. Automated Trigger and Dependency Pipeline Workflow
Trigger Setup:
Use Time-based Trigger for hourly ingestion of customer data from ADLS.
Configure Event-based Trigger to listen to changes in CosmosDB for real-time CDC.
Pipeline Dependencies:
ADF pipeline for customer data ingestion runs first.
CDC processing pipeline depends on the successful ingestion of customer data.
Workflow:
Orchestrate dependencies using ADF Pipeline Dependency Settings.
Automate pipeline execution with Azure Monitor for monitoring and alerting.
![diagram-export-03-12-2024-22_12_45](https://github.com/user-attachments/assets/d85422ed-5cd2-42be-9bfc-fe8624c0a9a7)
