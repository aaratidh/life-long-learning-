# Question

Write a SQL query that retrieves the top 3 most-purchased products by quantity, specifically for customers who are members. Output columns: `product_id`, `product_name`, `total_quantity_purchased`.

# Answer

```sql
-- Write your query here

SELECT 
    p.product_id, 
    p.name, 
    SUM(t.quantity) AS total_quantity_purchased 
FROM  
    product p 
JOIN    
    transaction t ON t.product_id = p.product_id
JOIN 
    customer c ON c.customer_id = t.user_id
WHERE  
    is_member = TRUE 
GROUP BY    
    p.product_id, p.name
ORDER BY  
    total_quantity_purchased DESC
LIMIT 3;
