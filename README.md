# Customer-Segmentation
This repository contains a comprehensive analysis of customer data for a subscription service to identify  segments and trends. I utilized Excel, SQL and Power BI to identify trends, patterns and correlations to uncover actionable insights that would drive business decisions.

## TABLE OF CONTENT

[OVERVIEW](#overview)

[GUIDE](#guide)

[DATA FILES](#data-files)

[EXCEL FILES](#excel-files)

[SQL QUERIES](#sql-queries)

[POWER BI REPORT](#power-bi-report)

[DOCUMENTATION](#documentation)

### OVERVIEW
---

The dataset contained 75,000 records and was analyzed using Excel, SQL and Power BI. 

#### KEY FEATURES

- Sales Performance Metrics (Revenue, Sales Growth)
- Sales Channel Analysis (Product, Region)

#### DATA SET 

The dataset was given by the incubator hub and contains 50,000 sales record from the past year.

#### METHODOLOGY

The dataset was given in an excel workbook alongside another dataset, I transferred to a new workbook and then I checked for duplicates. 

I used the **conditional formatting function which is found in the styles group on the Home tab** to check for duplicate values, it highlighted the whole table but to be completely certain, I used the **COUNTIFS** function which also proved to me that i had rows with the same records. 

I proceeded to remove duplicate by using the **remove duplicate function under the data tools group in the DATA tab**. I was left with 9921 rows which I used to perform my analysis. I ensured that all duplicates had been removed by using the **COUNTIFS** function again and it returned only 1 record for each series of criterias thereby proving that I now had a clean dataset.

I created a column for subscription duration, created a Revenue Tier column  I used the **PIVOT TABLE** to summarize my findings. 

At the end of my excel analysis, I exported my main dataset to another workbook which I saved as a CSV file, so that I could import it easily into my **SQL management studio**. At the management studio, I wrote different querries using the SQL OPerators (Logical, comparison and arithmetic). I also utilized the SQL Join to write my querries. I created a view to enable write my querries in a simpler form. 

I went further to import my data into my **POWER BI DESKTOP** work space and went ahead to transform my data. At the transform data page, I checked my column quality which was 100%, column distribution which showed that I had no empty rows or columns and column profile which gave a summary of my columns. I went further to add two conditional columns for Revenue Tier Sort, Cancelled Sort. I created measures for **Churn rate, Revenue, Count of canceled(True), Customer Life Value**. At the end of my analysis, I went ahead to create an interactive dashboard of 2 pages. 

#### INSIGHTS AND RECOMMENDATION

**Key Insights**
