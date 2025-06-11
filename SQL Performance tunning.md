### What one can do  for performance tunning 


- If you have time series data limitintg to a small time window can make your queries run more quickly 
- Testing your queries on a subset of data, finilizinf your query then removing the subset limitation is a sound strategy
- When working with subqueries, limiting the amount of data you're working with in the place where it will be executed first will have the maximum impact on query run time. 


### Make join less complicated 
- reduce the number of row  that are evaluted during join 
- pre aggregation befor joining 
- use explain tool (call query plan and find the order in which query is executed )

### What is the difference between Rank , dense_Rank  and ROW_number()?

- Rank()  will rank row based on the partition or global rank (group by or order by) and when there is ties and there are no ties breaker it will give same rank to tied rows but skip the next rank

- Dense Rank() will rank row based on the partition or rank  (group by or order by) and when there is tied rows and there are no ties breaker it will give same rank to ties yet continues consecutive order 

- Row number() basically count each row in a database will give unique rank to each row even if there are ties 

from given table 


### Q. Write a SQL query to assign a rank to each student based on their score in descending order using the following window functions:

SQL Table: 

| Name  | Score |
|-------|-------|
| Alice | 100   |
| Bob   | 95    |
| Carol | 95    |
| Dave  | 90    |


Eg. 


```sql 

SELECT 
  Name,
  Score,
  RANK() OVER (ORDER BY Score DESC) AS rank,
  DENSE_RANK() OVER (ORDER BY Score DESC) AS dense_rank,
  ROW_NUMBER() OVER (ORDER BY Score DESC) AS row_number
FROM scores;


````


| Name  | Score | RANK | DENSE_RANK | ROW_NUMBER |
|-------|-------|------|------------|------------|
| Alice | 100   | 1    | 1          | 1          |
| Bob   | 95    | 2    | 2          | 2          |
| Carol | 95    | 2    | 2          | 3          |
| Dave  | 90    | 4    | 3          | 4          |

