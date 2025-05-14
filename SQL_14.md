## Question:

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
