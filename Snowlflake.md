 ---
title: "Snowflake vs Redshift and Hive"
output: html_document
---

## Introduction

Snowflake is a modern cloud-based data platform that makes it easy to store, process, and analyze large volumes of data without worrying about infrastructure. It separates storage and computing, allowing you to scale them independently, saving both time and cost. Snowflake is fast, flexible, and works seamlessly across AWS, Azure, and GCP. You write SQL, and Snowflake handles the heavy lifting—performance tuning, scaling, and security—all behind the scenes.

## Snowflake Architecture

Snowflake’s architecture is divided into three main layers:

### 1. Storage Layer

Snowflake stores data in its internal storage layer, built on top of cloud object stores like Amazon S3. The data is automatically compressed and stored in a highly optimized columnar format. When ingested, data is broken into immutable micro-partitions that are automatically indexed and optimized for fast querying. Users do not need to manage indexes or partitions—Snowflake handles it all under the hood.

### 2. Compute Layer

A core advantage of Snowflake is the separation of compute and storage. Query processing is handled by compute clusters called *Virtual Warehouses* (similar to EC2 instances). These can be scaled up or down based on performance requirements. You only pay for compute when it is in use, making the platform highly cost-efficient.

### 3. Cloud Services Layer

This is the brain of the Snowflake platform. It manages metadata, authentication, access control, query parsing, and optimization. It ensures the compute and storage layers work in sync. This layer powers features like automatic performance tuning, concurrency scaling, and Snowflake’s zero-maintenance experience.

## Comparison: Snowflake vs Redshift vs Hive

### Storage

- **Hive** stores data on HDFS (Hadoop Distributed File System), which relies on hard disks.
- **Redshift** and **Snowflake** use cloud-based object storage (e.g., Amazon S3), enabling scalable, high-throughput storage.

### Data Format

- **Hive** stores data in row-based formats by default but supports columnar formats like ORC and Parquet with configuration.
- **Redshift** and **Snowflake** natively use columnar formats, enhancing analytical performance.

### Query Performance

- **Hive** often requires full disk scans, which slows performance and increases resource usage.
- **Redshift** and **Snowflake** leverage random-access object storage, enabling faster and more efficient queries.

### Metadata Management

- **Hive** stores metadata in the Hive Metastore, usually backed by MySQL or PostgreSQL.
- **Redshift** uses a PostgreSQL-based system catalog within its cluster.
- **Snowflake** manages metadata in its internal Cloud Services layer.

### Architecture

- **Snowflake** uniquely separates compute from storage, allowing independent scaling.
- **Redshift** and **Hive** have more tightly coupled architectures.
- All three support internal and external tables, enabling flexible data lake integration.

### Cloud Provider Support

- **Snowflake** supports multi-cloud deployment across **AWS**, **Azure**, and **GCP**, making it cloud-agnostic.
- **Redshift** is primarily tied to AWS.
- **Hive** is typically used on-prem or in self-managed cloud environments.

---

### bulk loading and  staging in snowflake: 
- Staging in Snowflake
       - One can directly create table from snowflake stages by doing load data and create new table and importaing schema 
 
- Bulk loading
       - one can directly load data from s3 into snowflake table using copy into command

![Screenshot 2025-05-21 191830](https://github.com/user-attachments/assets/d94fcdf0-7622-42f7-889f-2606919024cc)

![image](https://github.com/user-attachments/assets/0fa1a6ad-cd4b-43bd-b6a7-694ad3905955)

This  **'COPY INTO'**  code  the data from text.csv which is inside the s3 folder directly into the data table in snowflake. 
Show ** SHOW STAGES LIKE 'ADSB' **  show all the stage like ADSB show url of the s3 which is stage in the snowflake. 

**LIST @ADSB/snow/;**
- This will list all files stored in the external stage @ADSB, specifically within the subfolder input/snow/ in your linked S3 bucket.

**DESC STAGE ADSB;**   this will provide information of This command provides metadata about the stage, including:
- Column Name	      What It Tells You
- url	              The external location (like an S3 bucket) the stage points to
- has_credentials   whether credentials (IAM or access key) are attached
- type	             Type of stage (External, Internal)
- file_format	      Default file format if defined (e.g., CSV, JSON)
- copy_options      Default COPY INTO options if any
- comment	          Any comment added when the stage was created

### READING PARQUET FILES FORM A S3 FOLDER INTO SNOWFLAKE 
```sql
create or replace table listing_parquet(parquet_raw  variant)

```

```sql

copy into listing_parquet from ( select $1 from  @ADSB/stagging)
file_format =(TYPE = 'PARQUET')
PATTERN = '.*\.parquet';

select * from listing_parquet

```
### What does $1 meaning in snowflake slect statemnt snice parquet data doesnot have columns name so it use $1, $2 to refer as columns: 

- $1 = First column
- $2 = Second column
- $3 = Third column

### Colon offer  is used to  access the filed from JSON Data 

```sql 
select $1:buyerid , $1:dateid from  listing_parquet:

```
### MAPPING PARQUET DATA DIRECTLY INTO SNOWFALKE TABLE

```sql
create  or replace table listing  (

  buyerid INTEGER ,
  commission FLOAT,
  dateid integer,
  eventid integer,
  listid integer,
  pricepaid integer,
  qtysold integer,
  salesid integer,
  saletime timestamp,
   sellerid integer
);

```

```sql

COPY INTO listing
FROM (
  SELECT
    $1:buyerid,
    $1:commission,
    $1:dateid,
    $1:eventid,
    $1:listid,
    $1:pricepaid,
    $1:qtysold,
    $1:salesid,
    $1:saletime,
    $1:sellerid
  FROM @ADSB/stagging
)
FILE_FORMAT = (TYPE = 'PARQUET');

```
### You can also drictly write from snowflake into S3 
- AWS  will automatically create folder for the file in Aws  SInce the folder in which data are created are mounted. Hence, snowflake has direct access to the folder and can directly copy data  into S3 folder 

```sql
Copy into  @ADBS/output  from  pipe(a table in snowflake) Output folder in S3

```

```sql

CREATE TABLE V1 as select * from "DB1"."PUBLIC"."TAB_TAB" limit 1;
copy into @S3_STAGE1/snowflake_unload/temp2 from "V1";

```

### You can also create table which is same with existing table:

```sql
create table lisitng_copy LIKE listing

```


## TIME TRAVEL 
- Relation database are not good for fix schema 
- Relational database are not good for dynamic schema 








