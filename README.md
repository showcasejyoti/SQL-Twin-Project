# SQL-Learning Projects

## 🧾 Project Overview
In 2007, during the global recession when the stock market witnessed a severe collapse, a strategic shift in business operations led to the establishment of AtliQ Hardware, focusing primarily on the distribution of computer peripherals. Over time, the company experienced a consistent surge in sales performance, revenue generation, and overall business growth, which in turn resulted in a massive increase in the volume of data being recorded and maintained in Excel spreadsheets. 
However, by 2018, the limitations of Excel became evident as the system grew unstable, frequently crashed, and ultimately reached a point of complete failure. This critical challenge prompted the organization to migrate from a spreadsheet-based system to a more robust and scalable relational database management system (RDBMS) — MySQL. 
The company realized that in the modern digital economy, data is not merely information but a strategic asset, often referred to as digital gold, that can drive decision-making, competitive advantage, and sustainable growth. Recognizing the growing importance of data as a strategic business asset, the company went a step further by establishing a dedicated Data Analytics team which will empower AtliQ Hardware to harness data-driven insights for better decision-making, optimize operations, forecast market trends, and maintain a competitive edge.


The entire project has provided end to end experience. I worked on this project by following the Codebasics SQL Course, Link to the course is [here]https://codebasics.io/courses/sql-beginner-to-advanced-for-data-professionals

## 🗂️ Data Sources

AtliQ Hardware has provided two SQL databases and four Excel files for analysis.

**Database: gdb041**

**Fact Tables:**
- ```fact_forecast_monthly``` – Monthly sales forecasts.
- ```fact_sales_monthly``` – Actual monthly sales data.

**Dimension Tables:**

- ```dim_customer``` – Customer details.
- ```dim_market``` – Market segmentation.
- ```dim_product``` – Product information.

**Database: gdb056**

**Financial & Cost Data Tables:**

- ```post_invoice_deductions``` – Discounts applied after invoicing.
- ```pre_invoice_deductions``` – Discounts and adjustments before invoicing.
- ```freight_cost``` – Logistics and shipping costs.
- ```gross_price``` – Product pricing before discounts.
- ```manufacturing_cost``` – Production expenses.

**Time Frame & Fiscal Year**
AtliQ’s fiscal year runs from September to August.
The dataset includes actual sales data from September 1, 2017, to December 31, 2021.


## ✅ Notable SQL Projects
________________________________________
### 📒 Project -1
Report on top N Products per Division (with a stored procedure)

#### 🔍 Purpose of the Assignment:
To identify and rank the top-selling products within each division based on total quantity sold.
This helps the business focus on high-performing products for inventory optimization and sales strategy.

#### 🧠 Key Concepts Covered
- Joins – Used INNER JOIN to combine fact_sales_monthly and dim_product tables.
-	Aggregate Functions – Applied SUM() to calculate total quantity sold per product.
-	Window Functions – Implemented DENSE_RANK() to rank products within each division.
-	Common Table Expressions (CTEs) – Used to structure multi-step logic and simplify query readability.
-	Stored Procedure – Encapsulated the logic into a reusable stored procedure with parameters (fiscal_year, top_N).
-	Generated Column – Created a fiscal_year column for repeated use in queries.
-	Filtering and Ranking Logic – Applied filters to display only the Top N products per division.
-	Data Validation – Ensured proper data types and relationships before analysis.
-	Data Documentation – Exported final results as tabular reports for business insight.

#### 🛠 Approach:
-	Imported and validated data in MySQL, ensuring correct data types.
-	Added a generated column (fiscal_year) in the fact_sales_monthly table for repeated use across queries.
-	Performed an INNER JOIN between fact_sales_monthly and dim_product tables to combine sales and product information.
-	Aggregated data using SUM(sold_quantity) to calculate total sales quantity per product.
-	Applied a window function (DENSE_RANK()) partitioned by division to rank products by total quantity sold.
-	Filtered the results to return only the Top N products per division.
-	Used CTEs (Common Table Expressions) to simplify complex query logic and improve readability.
-	Encapsulated the logic inside a stored procedure with input parameters:
    + in_fiscal_year → to specify the year
    + in_top_n → to define the number of top products per division
-	Tested the stored procedure with different input values to ensure flexibility and accuracy.
-	Exported the final results as a PDF report for documentation and presentation.

  STORED PROCEDUR FOR TOP N PRODUCT PER DIVISION
  <img width="1920" height="991" alt="MySQL Workbench 05-09-2025 23_39_48" src="https://github.com/user-attachments/assets/9f868721-5ddc-4c07-9b0b-2e5b8f6eb77a" />

WHEN THE INPUT: in_fiscal_year=2021, in_top_n=5
<img width="1920" height="991" alt="MySQL Workbench 05-09-2025 23_41_49" src="https://github.com/user-attachments/assets/7744c2d0-1d2d-4793-814d-ad86c56cc7a3" />

#### 📈  View Exported Result





<img width="1920" height="1020" alt="Report-Top 5 product per division pdf - Adobe Acrobat Reader (64-bit) 11-11-2025 13_03_34" src="https://github.com/user-attachments/assets/e358fc08-b00a-4694-8f29-8652f3e748ea" />




### 📒 Project-2
Report on Customer whose forecast accuracy has dropped from 2020 to 2021

#### 🔍 Purpose of the Assignment:
To analyze and compare customer forecast accuracy between two fiscal years (2020 and 2021) and identify customers whose forecast accuracy has declined.
This helps the business identify areas where forecasting performance has deteriorated and take corrective actions in demand planning.

#### 🧠 Key Concepts Covered
-	Table Merging – Created a helper table fact_act_est by merging fact_sales_monthly and fact_forecast_monthly using FULL OUTER JOIN.
-	Aggregate Functions – Used SUM() and ABS() to compute total sold and forecast quantities.
-	Temporary Tables – Created temporary tables (T1, T2) to store year-wise forecast accuracy results.
-	Analytical Calculations – Computed Net Error %, Absolute Error %, and Forecast Accuracy %.
-	Conditional Expressions – Used IF() logic for calculating and comparing accuracy values.
-	Joins – Joined temporary tables on customer_code to compare accuracy across years.
-	Filtering Logic – Filtered customers whose forecast accuracy declined in 2021 compared to 2020.
-	Performance Comparison – Ranked and sorted customers based on change in forecast accuracy.
-	Data Documentation – Exported final results as tabular reports for business insight.

#### 🛠 Approach:
-	Imported and validated sales and forecast data in MySQL Workbench.
-	Created a helper table (fact_act_est) by merging fact_sales_monthly and fact_forecast_monthly using a FULL OUTER JOIN.
    -	This unified table was necessary to compare forecasted vs actual sales quantities and calculate related accuracy metrics.-
- Used aggregate functions to calculate total sold quantity, total forecast quantity, and corresponding error metrics.
-	Created temporary tables (T1 and T2) to store intermediate results for each year (2021 and 2020).
-	Applied formulas to calculate:
    -	Net Error % = (Σ(forecast_qty - sold_qty) * 100) / Σ(forecast_qty)
    -	Absolute Error % = (Σ(ABS(forecast_qty - sold_qty)) * 100) / Σ(forecast_qty)
    -	Forecast Accuracy % = 100 - ABS Error %
-	Joined both temporary tables on customer_code to compare forecast accuracy between the two years.
-	Filtered the results to display only those customers where forecast accuracy decreased in 2021 compared to 2020.
-	Sorted the output by forecast accuracy for detailed comparison and insights.
-	Saved the output as a tabular report for documentation and business analysis.

 SQL QUERY TO RETRIEVE CUSTOMERS WHOSE FORCAST ACCURACY HAS DROPPED FROM 2020 TO 2021
 -Step-1
<img width="1920" height="991" alt="MySQL Workbench 04-09-2025 12_42_28" src="https://github.com/user-attachments/assets/a8a43477-3db4-4977-86f3-b73cb23be1eb" />
-Step-2
<img width="1920" height="991" alt="MySQL Workbench 04-09-2025 12_44_29" src="https://github.com/user-attachments/assets/9bb2357c-5393-49d7-8f30-ac4869985a69" />
-Final step
<img width="1920" height="991" alt="MySQL Workbench 04-09-2025 12_49_23" src="https://github.com/user-attachments/assets/efece484-6bd2-49d8-b322-888abf5e8712" />



#### 📈 View Exported Result



<img width="1920" height="1020" alt="Report-Forecast_Accuracy_drop pdf - Adobe Acrobat Reader (64-bit) 11-11-2025 13_03_19" src="https://github.com/user-attachments/assets/04deedc7-01c4-4246-8d56-9ebb2610648f" />








