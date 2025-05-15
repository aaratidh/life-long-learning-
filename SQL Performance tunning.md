### What one can do  for performance tunning 


- If you have time series data limitintg to a small time window can make your queries run more quickly 
- Testing your queries on a subset of data, finilizinf your query then removing the subset limitation is a sound strategy
- When working with subqueries, limiting the amount of data you're working with in the place where it will be executed first will have the maximum impact on query run time. 


Make join less complicated 
-reduce the number of row  that are evaluted during join 
-pre aggregation befor joining 
-use explain tool (call query plan and find the order in which query is executed )

