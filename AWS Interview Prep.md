### Work flow to read data from slaesfroce and REST APT Using AWS Appflow lambda 

# Q1. AWS AppFlow Workflow: Ingest Salesforce CRM and REST API Data

## Workflow Steps

### Step 1: Create AppFlow Connection to Salesforce
- Go to AWS AppFlow → Create Flow
- Select Salesforce as the source
- Authenticate using Salesforce OAuth
- Choose the desired Salesforce objects (e.g., Lead, Contact, Opportunity)

### Step 2: Configure Destination (Amazon S3)
- Set up an S3 bucket/folder like:  
  `s3://your-bucket/raw/salesforce/`
- Select data format: CSV, JSON, or Parquet

### Step 3: Set Flow Trigger
Choose one of the following:
- On demand (manual run)
- Scheduled (e.g., every 1 hour)
- Event-based (if Salesforce supports event triggering)

### Step 4: Add Data Transformation Rules (Optional)
- Mask fields like email or phone number
- Map fields or rename columns to create a uniform schema

### Step 5: Ingest REST API Data
AppFlow does not support REST APIs natively, so use one of the following approaches:
- Use AWS Lambda with Amazon EventBridge (Scheduler) to call the REST API
- Store the response in:  
  `s3://your-bucket/raw/api-data/`
- Alternatively, use a custom connector with AppFlow if available

### Step 6: Orchestrate with Step Functions or Apache Airflow (Optional)
- Use AWS Step Functions or Apache Airflow to orchestrate:
  - The Salesforce AppFlow ingestion
  - The REST API Lambda job
- Validate both datasets are ingested successfully
- Trigger downstream ETL processing

### Step 7: Process with AWS Glue or Lambda
- Use AWS Glue or Lambda to transform, clean, and join Salesforce and REST API data
- Write the processed data to Silver or Gold layers in:
  - Amazon S3
  - Amazon Redshift
  - Snowflake

## AWS EMR ? 



## compile time VS Execution time VS RUntime 
- complie time is time required to convert code into machine language eg.  any code into 101010
- Execution time is exact time required by CUP for processing: CPU USage  time : to reduce: use parrallism threading, Reduce I/O Operations loadone to then reuse it, proper algorithm , used hash intested of nested loops  
- Runtime is total time required to run a programe it include execution time + input output read writes/ overhead +waiting time, use distributed compute
```python 
Total Run Time = Load Time + Execution Time
Compile Time happens before Run Time.
``` 
## How can i build a piple line with Airflow
- I can use a Define DAGs importing from Airflow and then  run dag in python or shell scripting 
eg
<img width="712" height="493" alt="image" src="https://github.com/user-attachments/assets/66253973-acbc-4fff-80eb-191b70614062" />
Each DAGS is the  component that include ingesttion transformation, 


# Q2.  What what the challange you faced in Trasaction analysis problem. 
### Situation: In our real-time fraud detection project, we streamed credit card transactions from multiple sources—ATMs, card readers, and Apple Pay—through Kafka into Databricks Delta Lake using PySpark Structured Streaming.

### Task: After a few days,
- We noticed performance dropped because fraud alerts started taking longer to show up — what used to run in 2 minutes began taking 10–15 minutes.
- When I checked the Delta table in Databricks, I saw thousands of tiny files in the storage path instead of a few big ones.
- The DESCRIBE DETAIL and OPTIMIZE commands showed file counts were very high, confirming the small file problem.
- Problem: More files = more time to read = slower alerts.

### Action: I identified the root cause as the small file problem, where thousands of tiny Delta files were being written from frequent micro-batches. 
- I optimized the pipeline by adjusting the micro-batch trigger to one minute,
- partitioning data by ingestion date, 
- and scheduling daily OPTIMIZE jobs in Databricks to compact small files.

### Result: This reduced metadata overhead by 90%, improved query speed by 5×, and kept the streaming fraud detection system cost-efficient and near real time.

## Note : Fraud alert: The fraud alert was a signal sent when a transaction looked suspicious — like sudden large payments or spending in two faraway places within minutes.The alert job ran on new transactions from the Delta table, scoring each with our fraud model. When performance dropped, these alerts started showing up late instead of instantly.


