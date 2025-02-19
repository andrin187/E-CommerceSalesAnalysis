# 🛍️ E-CommerceSalesAnalysis
### E-Commerce Sales Analysis: Identifying Revenue Trends & Customer Insights

## 💡 Data Cleaning 
Let's have a look at the dataset. 
```sql
SELECT *
FROM `ecommerce-data`
```
<img width="706" alt="Screenshot 2025-02-19 at 4 09 03 PM" src="https://github.com/user-attachments/assets/232ca069-f132-4a5f-b996-c3f406595958" />


The dataset contains data on customer e-commerce transactions; the invoice number, the stock code of each product, the quantity bought by that customer, the date and time of purchase , unit price, unique customer ID, and country.
The dataset contains over 24,000+ unique values.

Check for missing values:
```sql
SELECT *
FROM `ecommerce-data`
WHERE InvoiceNo IS NULL 
   OR StockCode IS NULL 
   OR Description IS NULL 
   OR Quantity IS NULL 
   OR InvoiceDate IS NULL 
   OR UnitPrice IS NULL 
   OR CustomerID IS NULL 
   OR Country IS NULL;
```
<img width="554" alt="Screenshot 2025-02-19 at 3 54 12 PM" src="https://github.com/user-attachments/assets/553507f7-8f79-487b-a47b-1837e3c4e1cd" />


There are no missing values.

## 💡 Data Transformation
Let's transform the dataset. The column `InvoiceDate` seems to include the time. Let’’s remove the time from the column and update the whole dataset.

```sql
UPDATE `ecommerce-data`
SET InvoiceDate = STR_TO_DATE(InvoiceDate, '%m/%d/%Y %H:%i');

UPDATE `ecommerce-data`
SET InvoiceDate = DATE(InvoiceDate);
```
Let's check the updated dataset. The `InvoiceDate` should be modified. 

<img width="687" alt="Screenshot 2025-02-19 at 3 59 14 PM" src="https://github.com/user-attachments/assets/a00ac6e9-e276-4e2b-907d-6f0b2445c21d" />


Let us create a new column `TotalUnitCost`, calculating the total cost the customer paid for the amount of products they bought where `TotalUnitCost` = `Quantity` × `UnitPrice`.
```sql
ALTER TABLE `ecommerce-data` 
ADD COLUMN TotalUnitCost DECIMAL(10,2);

UPDATE `ecommerce-data`
SET TotalUnitCost = Quantity * UnitPrice;
```

The dataset should now be transformed and ready for analysis.

<img width="768" alt="Screenshot 2025-02-19 at 4 05 19 PM" src="https://github.com/user-attachments/assets/8bc5bd19-19c7-4973-b2a8-a28404dd864b" />

***

