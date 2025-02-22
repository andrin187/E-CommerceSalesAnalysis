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
**1. Are there seasonal trends or peak shopping periods?**

Let’s perform a EDA with visualizations using R Statistics.

❗The `Data Cleaning with R` Markdown file will show how to prepare the date for analysis within R.

When the dataset is ready for analysis, we can create a line graph to see trends overtime. 

Extract the month and year: 
```r
ecommercedata$Month <- format(ecommercedata$InvoiceDate, "%m")
ecommercedata$Year <- format(ecommercedata$InvoiceDate, "%Y")
ecommercedata
```

Group the data by month and calculate the total sales per month (sum of TotalUnitCost).
```r
library(dplyr)

monthly_sales <- ecommercedata %>%
  group_by(Year, Month) %>%
  summarise(TotalSales = sum(TotalUnitCost)) %>%
  arrange(Year, Month)

monthly_sales
```

<img width="1245" alt="Screenshot 2025-02-22 at 4 01 42 PM" src="https://github.com/user-attachments/assets/05c2ca92-d9ee-4fab-8a1d-0f3b16b3ce11" />
<img width="1242" alt="Screenshot 2025-02-22 at 4 02 08 PM" src="https://github.com/user-attachments/assets/ea0db3d8-018d-4930-bcea-cd55365aea55" />


We should expect a visualization of sales from Dec. 2010 to Dec. 2011.

```r
library(ggplot2)

ggplot(monthly_sales, aes(x = as.Date(paste(Year, Month, "01", sep = "-")), y = TotalSales)) +
  geom_line(color = "blue") +
  labs(title = "Total Sales per Month", x = "Month", y = "Total Sales") +
  theme_minimal()

```

<img width="709" alt="Screenshot 2025-02-22 at 4 03 17 PM" src="https://github.com/user-attachments/assets/5aaa15d3-81fd-4618-831c-08ec8aa15a29" />


**2. What is the total revenue generated over a specific period?**

   Over this peak seasonal period the total revenue generated from September - November is 3552148.5 from simple addition.

   Let’s see what proportion of sales come from peak season…

```r
total_sales_all_months <- sum(monthly_sales$TotalSales)
total_sales_all_months
```

<img width="114" alt="Screenshot 2025-02-22 at 4 05 28 PM" src="https://github.com/user-attachments/assets/06a7476d-f502-4892-9ba4-d1122580adf0" />

```r
sep_nov_sales <- monthly_sales %>%
  filter(Month %in% c("09", "10", "11"))

total_sales_sep_nov <- sum(sep_nov_sales$TotalSales)

total_sales_sep_nov 
```

<img width="139" alt="Screenshot 2025-02-22 at 4 05 55 PM" src="https://github.com/user-attachments/assets/b8944b5e-1099-465b-ab57-6c4c9202ec79" />


```r
proportion <- total_sales_sep_nov / total_sales_all_months
proportion*100
```

<img width="124" alt="Screenshot 2025-02-22 at 4 06 22 PM" src="https://github.com/user-attachments/assets/883d88de-367b-441f-83db-9d5e2ae3994f" />


```r
#Find sum of total sales
total_sales_all_months <- sum(monthly_sales$TotalSales)

#Filter the months for peak season (Sep-Nov)
sep_nov_sales <- monthly_sales %>%
  filter(Month %in% c("09", "10", "11"))
total_sales_sep_nov <- sum(sep_nov_sales$TotalSales)

#Find the proportion
proportion <- total_sales_sep_nov / total_sales_all_months
proportion*100

cat("Total Sales for All Months: ", total_sales_all_months, "\n")
cat("Total Sales from September to November: ", total_sales_sep_nov, "\n")
cat("Proportion of Sales from November and December: ", proportion*100, "\n")
```

<img width="501" alt="Screenshot 2025-02-22 at 4 07 32 PM" src="https://github.com/user-attachments/assets/f2d8a331-3b0d-44d4-8b3a-760a730c0f32" />


**3. Which products generate the highest revenue?**

The column `TotalUnitCost` can help to answer this question.
```sql
SELECT *
FROM `ecommerce-data`
ORDER BY TotalUnitCost DESC;
```

<img width="761" alt="Screenshot 2025-02-22 at 4 09 42 PM" src="https://github.com/user-attachments/assets/0c40b5e5-1bea-4c52-98b9-ca593673da99" />

**4. What are the highest and lowest revenue-generating products?**

We found the highest revenue-generating products from the last analysis. We can use the same technique to find the lowest revenue-generating products. 
```sql
SELECT *
FROM `ecommerce-data`
ORDER BY TotalUnitCost ASC;
```

<img width="752" alt="Screenshot 2025-02-22 at 4 11 13 PM" src="https://github.com/user-attachments/assets/50f6aa87-dec6-4248-b938-915700958265" />

***
