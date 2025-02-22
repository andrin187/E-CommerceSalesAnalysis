# 🛍️ E-CommerceSalesAnalysis
### E-Commerce Sales Analysis: Identifying Revenue Trends & Customer Insights

## 💡 Data Cleaning with R

Upload the CSV:

```r
ecommercedata <- read.csv("~/Downloads/data-2.csv")
ecommercedata
```

<img width="1268" alt="Screenshot 2025-02-22 at 4 15 42 PM" src="https://github.com/user-attachments/assets/2eb49f42-6b45-4e4f-8a76-cb397e1691be" />


Update `InvoiceDate` column:

```r
ecommercedata$InvoiceDate <- as.Date(ecommercedata$InvoiceDate, format = "%m/%d/%Y %H:%M")
ecommercedata
```

<img width="1266" alt="Screenshot 2025-02-22 at 4 16 01 PM" src="https://github.com/user-attachments/assets/e1d87410-7b8f-4739-9875-0256d3bbf006" />

Create `TotalUnitCost` column:

```r
ecommercedata$TotalUnitCost <- ecommercedata$Quantity * ecommercedata$UnitPrice
ecommercedata
```

<img width="1268" alt="Screenshot 2025-02-22 at 4 16 50 PM" src="https://github.com/user-attachments/assets/0c263de6-8699-4dad-b3f0-0b78e851d853" />

The dataset is now ready for analysis.
