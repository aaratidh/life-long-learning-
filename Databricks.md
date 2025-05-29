###  What is Databricks?
- It is webbased cloud platform taht uses spark and Notebooks with cluster 
- Combines the functionality of a data warehouse and datalake
- It is used for data processing, data storage, machine learning and business
- Platform is abailbale in Azure , Amazon Aws , GCP
- Pay as You Go
- Records Notebook Changes
- Switch Between languages pyspark , java R scala 
- Support existing files zip file can be uploaded 
- Scalibility and compute
- Pair programming
- Decreased development time and easier workflows
- Integrates with Github
- MLflow and Delta Lake
- Databricks support multiple languages
- so one can works with SQL using %sql% from
- or you can  read dataframe in sql like: df = spark.sql(select * from emp)
- Streaming means dat comes inform of packets 

### for what purpose Datbricks is used ?
- Create Utilities and Data Models
- Extract, Transform , and load data
- Use with orchestration Tools like dbt and datafactory 
- Store Data
- Using applications

### Other properties of Databricks 
- Readstream , Writestream 
- Since it does both batch and streaming processing
- Read method means batch reading, and write method means batch reading
- Readstream while we read data from streaming means data comes in packets and there need to be a destination to dump that packets. There always need to be a combination of Readstream and writestream since data are continious comming. One need to provide sink for the data. 
- Spark streaming is continious process and while pushing data into table spark is wating for new data to process( data process can be writting a new data into output file). For every new data identification spark add new record and write it into directory.
- Spark maintains version for writting new data every time:
    - version '0'  create data
    - version '1'  add 1st batch
    - version '2'  add 2nd batch
### HAnding Failure in data bricks
- We will be using version and timestamp to identiofy when we were left to process data
- Here are few methods to process data:
    - Read from start
    - Read from Table
    - Read from Specific Verison
    - Read from specific timestamp
    - Resilancy and checkpointing
###  Checkpointing 
- Checkpointing is the mechanism where spark record meta data of the successfull batches od data process (which can be read job, write job, clenaing job )
- Sometime time stampp and version can be inclusive and may introduce the duplicated data so we prefer checkpointing 
  

