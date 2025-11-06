+## Question:

### points to take: 
- if the name of sql column has white space the use `` this bracket
- to find comulative sum in SQL use sum(column on which value has to be summed) over ()
- converting different columns of a table in a same column of another table can be done using Union all.
- If there are no common column in cross join then use cross join
  



Provide the name for each region for every order, as well as the account name and the unit price they paid (`total_amt_usd / total`) for the order.  
However, you should only provide the results if the **standard order quantity exceeds 100**.  
Your final table should have **3 columns**:  
- Region name  
- Account name  
- Unit price  

To avoid a division by zero error, it's helpful to add **`0.01` to the denominator**, like so:  
`total_amt_usd / (total + 0.01)`

---

### Database Schema:

![Screenshot 2025-05-14 132605](https://github.com/user-attachments/assets/de86b74c-7a0a-4fd6-99f8-3cd362c44535)

---

## Answer:

```sql

SELECT 
    r.name AS region, 
    a.name AS accountname, 
    o.total_amt_usd / (o.total + 0.01) AS unit_price
FROM region r
JOIN sales_reps s
  ON r.id = s.region_id
JOIN accounts a 
  ON s.id = a.sales_rep_id
JOIN orders o 
  ON a.id = o.account_id
WHERE standard_qty > 100 
  AND poster_qty > 50;
```



### Question 15 

Determine the number of times a particular channel was used in the `web_events` table for each region.  
Your final table should have **three columns**:  
- the **region name**,  
- the **channel**, and  
- the **number of occurrences**.  

Order your table with the **highest number of occurrences first**.

---

### Answer:

```sql
SELECT r.name, w.channel, COUNT(*) AS num_events
FROM accounts a
JOIN web_events w
  ON a.id = w.account_id
JOIN sales_reps s
  ON s.id = a.sales_rep_id
JOIN region r
  ON r.id = s.region_id
GROUP BY r.name, w.channel
ORDER BY num_events DESC;
```

### Question 16 

What was the smallest order placed by each account in terms of total usd. Provide only two columns - the account name and the total usd. Order from smallest dollar amounts to largest.

---

### Answer:

```sql
SELECT a.name, MIN(total_amt_usd) smallest_order
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY a.name
ORDER BY smallest_order;

```
###  Question 16

In which month of which year did Walmart spend the most on gloss paper in terms of dollars?


``` sql 

SELECT DATE_TRUNC('month', o.occurred_at) ord_date, SUM(o.gloss_amt_usd) tot_spent
FROM orders o 
JOIN accounts a
ON a.id = o.account_id
WHERE a.name = 'Walmart'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;


```

### Question 17 

 This time, create a running total of standard_amt_usd (in the orders table) over order time with no date truncation. 
 Your final table should have two columns: one with the amount being added for each new row, and a second with the running total.

###Answer: 

```sql

SELECT standard_amt_usd,
SUM(standard_amt_usd) OVER (partition by date_trunc('month',occurred_at ) ORDER BY occurred_at) AS running_total
FROM orders

```

### Question  18 

Use the accounts table to create first and last name columns that hold the first and last names for the primary_poc.


```sql

select 
 primary_poc,
 left(primary_poc, POSITION (' ' in  primary_poc ))as firstname,
 right(primary_poc, length(primary_poc)-POSITION (' ' in  primary_poc ))as lastname
                     
from  accounts 

```


### Question 19 
Now see if you can do the same thing for every rep name in the sales_reps table. Again provide first and last name columns.


```sql
select 
 name ,
 left(name, POSITION (' ' in  name ))as firstname,
 right(name, length(name)-POSITION (' ' in  name ))as lastname
                     
from  sales_reps 
```
### Question 20 

Each company in the accounts table wants to create an email address for each primary_poc. The email address should be the first name of the primary_poc . last name primary_poc @ company name .com.



```sql
with  t1 as 
( 
 select 
 name ,
 left(primary_poc, POSITION (' ' in  primary_poc ))as firstname,
 right(primary_poc, length(primary_poc)-POSITION (' ' in  primary_poc ))as lastname
                     
from  accounts  

)
      
select 
  CONCAT(firstname,'.',lastname,'@',Replace(name, ' ', ''),'.com' ) as email 
  from t1 
       
```
)



### Questions 17 

Write an SQL query to find the last time when each bike was used.

Return the result table ordered by the bikes that were most recently used. 

The query result format is in the following example.

Table: 
  


### Table: Bikes

| Column Name | Type      |
|-------------|-----------|
| ride_id     | int       |
| bike_number | int       |
| start_time  | datetime  |
| end_time    | datetime  |



```sql

Select  bike_number ,  max(end time) as end time  
from Bikes 
group by bike_number 
order by max(end_time) desc

```


### Question 18 

### Year Over Churn

| driver_id | start_date | end_date   |
|-----------|------------|------------|
|     1     | 2021-07-05 | 2022-08-02 |
|     2     | 2021-07-05 | 2023-09-06 |
|     3     | 2021-07-05 | 2024-08-08 |

     

```sql


with year_Churn as (

slecet year(end_date) as yer , count(1) as churn from lyft_divers 
where end_date is not null 
group by year(end_date)

)

Select current_year.year, current_year.churn  ,

case 
	when last_year.churn > current_year.churn then 'decrease'
	when last_year.chrun < current_year.churn then 'increase'
        else 'no change'
	end as chnage_indicator 
from yearly_churn current_year 
        left join yearly_churn last_year on  current_year.year = last_year.year+ 1

```


### Question 18 

Q.

	Find the best-selling item for each month (no need to separate months by year) where the biggest total invoice was paid.  
	The best-selling item is calculated using the formula (unitprice * quantity ). Output the description of the item along with the amount paid. 

Your output should include:

	the month (use DATE_TRUNC('month', invoicedate)),
	the description of the best-selling item, 
	and the total amount paid.


Table: 

### Table: online_retail

| Column Name  | Data Type | Description                              |
|--------------|-----------|------------------------------------------|
| invoiceno  | VARCHAR   | Unique invoice ID                          |
| stockcode  | VARCHAR   | Product stock code                         |
| description| VARCHAR   | Description of the item                    |
| quantity   | INT       | Number of units purchased                  |
| invoicedate| DATETIME  | Date and time of the invoice               |
| unitprice  | FLOAT     | Price per unit                             |
| customerid | FLOAT     | ID of the customer                         |
| country    | VARCHAR   | Customer’s country                         |


```sql

Solution: 

Select 
	Date_trunc('month', invoicedate) as month 
	max(unitprice * quantity) as best selling item, 
	description 
from 
	online_retails 
group by 
	month, description 
order  by 
	 Date_trunc('month', invoicedate)
limit 1 

```
``` sql

With monthly_sales AS(

Select 
	Date_tunct('month' , invoicedate) as month, 
	description, 
	sum(unitprice * quantity) as total amount 
	group by Date_tunct('month' , invoicedate) as month,  , description
), 

ranke_item as (

	select *, 
       		Rank() over (Partition by  month order by  total amount  desc) as rnk 
        from 
		monthly_sales
)

Select invoceno.,
       description, 
       totalamount 
from 
       Ranked_item 
       where rnk = 1

)



```



### Question 19 

 Email Activity Rank Problem

 Find the email activity rank for each user. Email activity rank is defined by the total number of emails sent. The user with the highest number of emails sent will have a rank of 1. and so on. Output the user, total emails, and their activity rank. Order records by the total emails in descending order. Sort users with the same number of emails in alphabetical order.
In your rankings, return a unique value(i.e a unique rank) even if multiple users have the same number of emails. For tie breaker use alphabetical order of the user usernames. 

---

## Table Schema

| Column Name | Data Type |
|-------------|-----------|
| id          | int       |
| from_user   | varchar   |
| to_user     | varchar   |
| day         | int       |

```sql

Select from_user  as user, 
count(from_user) as email sent, 
ROW_NUMBER(order by  count(from_user) desc , from id asc) as activity_rank
group by  id 
order by count(from_user) desc 

```

#### Note : One can use Rank dense Rank and also Row_number will give same number of output because   we are using a tie breaker which is order of the user username: if there were not a tie break then you cannot use Rank and Dense rank because this  will give you non- unique values 


 #### Q.20  SQL Challenge: Successful Multiple Purchases in the Last 1 Month


**Find customers with successful multiple purchases in the last 1 month.**  
- A purchase is considered **successful** if it is **not returned within 1 week of purchase** (i.e., either return_date is NULL or return_date > purchase_date + 7 days).

---

##  Table: `purchases`

| purchase_id | customer_id | purchase_date | return_date |
|-------------|-------------|----------------|--------------|
| 1           | 101         | 2025-04-30     | 2025-05-01   |
| 2           | 102         | 2025-04-29     | 2025-04-29   |
| 3           | 101         | 2025-04-30     | *(null)*     |
| 4           | 103         | 2025-04-05     | *(null)*     |
| 5           | 103         | 2025-04-17     | *(null)*     |
| 6           | 101         | 2025-04-08     | 2025-04-10   |
| 7           | 102         | 2025-03-28     | *(null)*     |
| 8           | 104         | 2025-04-01     | 2025-04-20   |

---

## SQL Solution

```sql
-- Step-by-step SQL to find customers with successful multiple purchases in the last 1 month

WITH filtered_purchases AS (
    SELECT *
    FROM purchases
    WHERE purchase_date >= CURRENT_DATE - INTERVAL '1 month'
),
successful_purchases AS (
    SELECT *
    FROM filtered_purchases
    WHERE return_date IS NULL 
       OR return_date > purchase_date + INTERVAL '7 days'
),
customer_counts AS (
    SELECT customer_id, COUNT(*) AS purchase_count
    FROM successful_purchases
    GROUP BY customer_id
)
SELECT customer_id
FROM customer_counts
WHERE purchase_count > 1;

```

### Q delete Duplicated from the SQl function 

![image](https://github.com/user-attachments/assets/dc5845b8-7590-4932-84da-9eb32af9e728)

```sql

delete * from care where ctid  not in  (

Select  max(ctid) 
from cars 
group by id, name, model
having count(*) >1
)
```

### Q calulation height salary from each department 

employee table 

| id  | name      | dept    | salary |
|-----|-----------|---------|--------|
| 1   | Alexander | Admin   | 6500   |
| 2   | Leo       | Finance | 7000   |
| 3   | Robin     | IT      | 2000   |
| 4   | Ali       | IT      | 4000   |
| 5   | Maria     | IT      | 6000   |
| 6   | Alice     | Admin   | 5000   |
| 7   | Sebastian | HR      | 3000   |
| 8   | Emma      | Finance | 4000   |
| 9   | John      | HR      | 4500   |
| 10  | Kabir     | IT      | 8000   |

```sql

    select id, name, dept, salary,
           max(salary) over (partition by dept order by salary desc) as highest_Salary,
		   min(salary) over (partition by dept order by salary asc) as lowest_Salary
    from employees


```
![image](https://github.com/user-attachments/assets/6eee3bda-b3fc-4657-a3dd-f08cf9ae908f)


### 21
Q  Finding total sales for each month of the year 2023 

 SQL table

| sale\_id | sale\_date | amount |
| -------- | ---------- | ------ |
| 1        | 2024-11-01 | 150.00 |
| 2        | 2023-10-02 | 200.50 |
| 3        | 2023-01-03 | 350.75 |
| 4        | 2024-11-04 | 420.00 |



```sql 

select Date_trunc(month , sales_date)  as months 
       Date_trunc(year, sales_date) as year 
       sum(amount) as sales_in_month
       where year = '2023' 
       group by 1 

```

###  Question 22
 Write a query to find customer name and city who placed orders after 1st January 1, 2023 ?



Customer table 

| CustomerID | Customer Name | City        |
| ---------- | ------------- | ----------- |
| 1          | Alice Smith   | New York    |
| 2          | Bob Johnson   | Los Angeles |
| 3          | Charlie Davis | Chicago     |
| 4          | Robin Smith   | Chicago     |
| 5          | Tom Cruise    | London      |


Order table 


| OrderID | CustomerID | OrderDate  | OrderAmount |
| ------- | ---------- | ---------- | ----------- |
| 101     | 1          | 2023-01-01 | 250         |
| 102     | 2          | 2024-03-11 | 150         |
| 103     | 4          | 2023-04-10 | 300         |
| 104     | 3          | 2022-05-04 | 450         |
| 105     | 5          | 2024-07-22 | 120         |

	
```sql

Select 
	c.customerID 
        c.Customer Name 
        c.City 
        o.OrderDate 
        o.OrderAmount
from 
    customer c 
join order o 
where orderDate > "2023-01-1" 

```

### 23.  finding second heightest salary  from department  IT


Employee table 


| id  | name      | dept    | salary |
|-----|-----------|---------|--------|
| 1   | Alexander | Admin   | 6500   |
| 2   | Leo       | Finance | 7000   |
| 3   | Robin     | IT      | 2000   |
| 4   | Ali       | IT      | 4000   |
| 5   | Maria     | IT      | 6000   |
| 6   | Alice     | Admin   | 5000   |
| 7   | Sebastian | HR      | 3000   |
| 8   | Emma      | Finance | 4000   |
| 9   | John      | HR      | 4500   |
| 10  | Kabir     | IT      | 8000   |



``` sql 

select  max(salary) from employee 
where  salary <(select max(salary ) from employee where dept = IT)



``` 

Q4.  Find the name of the product that have never been sold  ?



Product table 

| ProductID | ProductName | Price   |
| --------- | ----------- | ------- |
| 1         | Laptop      | 1200.00 |
| 2         | Smartphone  | 800.00  |
| 3         | Tablet      | 500.00  |
| 4         | Headphones  | 150.00  |
| 5         | Smartwatch  | 200.00  |


Sales table 

| SaleID | ProductID | Quantity |
| ------ | --------- | -------- |
| 101    | 1         | 3        |
| 102    | 2         | 5        |


``` Sql 

select   p.producID , p.ProductName p.Price

from product p 
left join sale s 
where salesId  is NULL 


```


Q.5  Find the customer whose order amount exceed 1000 


table cutomer 


| OrderID | CustomerID | OrderAmount |
| ------- | ---------- | ----------- |
| 1       | 101        | 550.00      |
| 2       | 102        | 150.50      |
| 3       | 101        | 300.75      |
| 4       | 103        | 450.00      |
| 5       | 103        | 500.00      |
| 6       | 101        | 250.00      |
| 7       | 104        | 400.00      |
| 8       | 103        | 820.25      |



```  sql 

select 
sum(amount) , customerID 
from customer 
 group by (CustomerID) 
 Having  sum(amount) >  1000



``` 
### TAble empman 

<img width="327" height="169" alt="image" src="https://github.com/user-attachments/assets/1104424c-e55b-48a3-856f-18d690197513" />

### Q Write a query to  retrive the names of employees along with theirs direct  managers. 
		 
```sql 
select e1.Employee_Name as employee , e2.employee_Name as managername 
from	empman e1 
join	empman e2 
on e2.Employee_ID = e1.Manager_ID

```
```sql

Create table customer  (
    CustomerID int  Primary key , 
	CustomerName  varchar(100)
	) 

	INsert into customer ( CustomerID , CustomerName ) values 
	    (1, 'Alice Smith'),
		(2,'Bob Johnson'),
		(3,'Charlie Davis');

Create table orders 
   ( 
   orderID int primary  key, 
   CustomerID int, 
   orderdate  DATE, 
   orderAmount decimal(10 ,2),
   FOREIGN KEy (CustomerID) references Customer(CustomerID)
   )

Create table Payment (
   PAymentID int, 
   OrderID int, 
   PaymentAmount Decimal(10 , 2),
   PaymentDate DATE, 
   FOREIGN KEY (orderID) References Orders(OrderID)

   );


   Insert into orders  (orderID , CustomerID, orderdate , orderAmount ) values

(101, 1, '2023-01-01', 250.00),
(102, 2, '2024-11-03', 150.50),
(103, 1, '2022-10-04', 300.75),
(104, 3, '2023-12-05', 450.00),
(105, 2, '2023-11-07', 120.25);
	

   Insert into payment (PAymentID ,OrderID, PaymentAmount, PAymentDate ) values 

(1001, 101, 250.00, '2023-01-04'),
(1002, 102, 150.50, '2024-11-10'),
(1003, 103, 150.00, '2022-10-08'),
(1004, 104, 450.00, '2023-12-06'),
(1005, 105, 120.25, '2023-12-07');

-- Q Write a query  to list each customer name, total order amount, total payment amounnt  for order placed in 2023 


select c.customername ,  sum(o.orderamount ) , sum(p.paymentamount) 
from customer c 
join  orders o 
on c.CustomerID = o.CustomerID
join payment p 
on p.OrderID = o.orderID
where  Year(orderdate) = 2023
group by  c.customername 


```

# Q24 

# find teh cumulative sum of the following 
Queue table:

| person_id | person_name | weight | turn |
|-----------|-------------|--------|------|
| 5         | Alice       | 250    | 1    |
| 4         | Bob         | 175    | 5    |
| 3         | Alex        | 350    | 2    |
| 6         | John Cena   | 400    | 3    |
| 1         | Winston     | 500    | 6    |
| 2         | Marie       | 200    | 4    |
Output: 

Explanation: The folowing table is ordered by the turn for simplicity.

| Turn | ID | Name      | Weight | Total Weight |
|------|----|-----------|--------|--------------|
| 1    | 5  | Alice     | 250    | 250          |
| 2    | 3  | Alex      | 350    | 600          |
| 3    | 6  | John Cena | 400    | 1000         | (last person to board)
| 4    | 2  | Marie     | 200    | 1200         | (cannot board)
| 5    | 4  | Bob       | 175    | ___          |
| 6    | 1  | Winston   | 500    | ___          |


Solution: 
``` sql

select  
q.turn ,  
q.person_id  As ID ,
q.person_name  as Name , 
q.weight  as Weight,
SUM(weight) OVER (ORDER BY q.turn) AS Total_Weight


```
