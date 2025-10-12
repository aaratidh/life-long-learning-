### Work flow to read data from slaesfroce and REST APT Using AWS Appflow lambda 

# AWS AppFlow Workflow: Ingest Salesforce CRM and REST API Data

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
- 


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


