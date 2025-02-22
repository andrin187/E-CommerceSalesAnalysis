# 🛍️ E-CommerceSalesAnalysis
### E-Commerce Sales Analysis: Identifying Revenue Trends & Customer Insights

## 💡 Customer Behaviour Analysis
**1. What are the top-selling products based on quantity sold?**

   ```sql
   SELECT *
   FROM`ecommerce-data`
   ORDER BY Quantity DESC;
   ```
   <img width="771" alt="Screenshot 2025-02-22 at 3 44 10 PM" src="https://github.com/user-attachments/assets/d80fe225-2367-4c0b-9a51-c3b75c875410" />
   


**2. What is the average order value per customer?**

   We can calculate the total spending for each customer `SUM(TotalUnitCost)`. Then, we take the average of those totals,  `AVG(TotalSpent)`, which gives us the average order value per customer.
```sql
SELECT AVG(TotalSpent) AS AverageOrderValue
FROM (
	SELECT CustomerID, SUM(TotalUnitCost) AS TotalSpent
    FROM `ecommerce-data`
    GROUP BY CustomerID
    ) AS CustomerSpending;
```

<img width="111" alt="Screenshot 2025-02-22 at 3 48 51 PM" src="https://github.com/user-attachments/assets/479780ef-0da0-4785-bd0a-6388af7d8b56" />



**3. How many unique customers are in the dataset?**

```sql
SELECT COUNT(*) AS TotalCount
FROM `ecommerce-data`
```

<img width="140" alt="Screenshot 2025-02-22 at 3 54 12 PM" src="https://github.com/user-attachments/assets/0c15ee20-dc17-46d6-a1ea-f284102dc7eb" />


```sql
SELECT COUNT(DISTINCT CustomerID) AS CustomerCount
FROM `ecommerce-data`
```

<img width="91" alt="Screenshot 2025-02-22 at 3 54 31 PM" src="https://github.com/user-attachments/assets/b0978d41-39cb-421a-ae3d-5504a348dadd" />


## 💡 Sales Performance & Revenue Analysis
