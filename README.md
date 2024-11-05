# Customer-Segmentation
This repository contains a comprehensive analysis of customer data for a subscription service to identify  segments and trends. I utilized Excel, SQL and Power BI to identify trends, patterns and correlations to uncover actionable insights that would drive business decisions.

## TABLE OF CONTENT

[OVERVIEW](#overview)

[DATA](#data)

[SEGMENTATION MODEL](#segmentation-model)

- **Demographic Segmentation**

- **Behavioural Segmentation**

[REVENUE TREND](#revenue-trend)

[INSIGHTS AND RECOMMENDATION](#insights-and-recommendation)

[EXCEL FILES](#excel-files)

[SQL QUERIES](#sql-queries)

[POWER BI REPORT](#power-bi-report)

[DOCUMENTATION](#documentation)

- **Data Dictionary**

[MAINTAINERS](#maintainers)


### OVERVIEW
---

This repository contains the data, code and insights for my customer segmentation project. The goal of this project is to identity and understand the distinct customers groups based on demographics, behaviour and revenue. The insight gotten will enable data driven decisions for improving sales and generating productive product strategies. The dataset contained 75,000 records and was analyzed using Excel, SQL and Power BI. 

#### KEY FEATURES AND SCOPE

- Customer data from January 2022 to August 2024.
- Demographic Segmentation(Region by Subscription type).
- Revenue Tiers (Low, Medium, High).
- Behavioural Segmentation
- Subscription Trend

### DATA  
---

The dataset was given by the incubator hub and contained 75,000 customer subscription record from the 2022 to 2024. 

#### METHODOLOGY

The dataset was given in an excel workbook alongside another dataset, I transferred to a new workbook and then I checked for duplicates. 

I used the **conditional formatting function which is found in the styles group on the Home tab** to check for duplicate values, it highlighted the whole table but to be completely certain, I used the **COUNTIFS** function which also proved to me that i had rows with the same records. 

I proceeded to remove duplicate by using the **remove duplicate function under the data tools group in the DATA tab**. I was left with 33,787 rows which I used to perform my analysis. I ensured that all duplicates had been removed by using the **COUNTIFS** function again and it returned only 1 record for each series of criterias thereby proving that I now had a clean dataset.

I created a column for subscription duration, created a Revenue Tier column and I used the **PIVOT TABLE** to summarize my findings. 

At the end of my excel analysis, I exported my main dataset to another workbook which I saved as a CSV file, so that I could import it easily into my **SQL management studio**. At the management studio, I wrote different querries using the SQL OPerators (Logical, comparison and arithmetic). I also utilized the SQL Join to write my querries. I created a view to enable me write my querries in a simpler form. 

I went further to import my data into my **POWER BI DESKTOP** work space and went ahead to transform my data. At the transform data page, I checked my column quality which was 100%, column distribution which showed that I had no empty rows or columns and column profile which gave a summary of my columns. I went further to add two conditional columns for Revenue Tier Sort, Cancelled Sort. I created measures for **Churn rate, Revenue, Count of canceled(True), Customer Life Value**. At the end of my analysis, I created an interactive dashboard of 3 pages. 

#### TOOLS NEEDED

- Microsoft Excel [Download Here](https://www.microsoft.com/en-us/microsoft-365/excel)
    
- SQL - Structured Querry Language for querrying data [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)

- Power BI [Install](https://www.microsoft.com/en-us/download/details.aspx?id=58494)

### SEGMENTATION MODEL
---

 - **Demographic Segmentation**
The customers where segmented based on their regions and then analyzed. There are four regions used in this analysis.

      **EAST REGION**: This is the top performing region by revenue. There was no record of subscription cancellation in this region which showed that the customers where satisfied with the service in this region. The subscription type for all the customers in this region was Basic. This shows that the basic subscription package is the best performing package.

      **SOUTH REGION**: This is the top 2 region by revenue generated. This region has a churn rate of **60%**. 100% of the customers used the premium subscription package. In the second quarter of 2023, revenue dropped by 1.4% but by the fourth quarter it had increased by 1.1%.

      **WEST REGION**: Average Revenue Per User (ARPU) is 2,003 which is even higher than that of the customers in the East (1,998). Although the average customer spent more on his subscription, revenue was low because the churn rate was also **60%**. The high ARPU can also be explained because all the customers opted for the Premium subscription type. From the revenue trend, we can see a steady increase in revenue throughout the quarters.

      **NORTH REGION**: This is the least performing region. ARPU is 1,994 and the most popular package is the basic package.

 - **Behavioral Segmentation**
A revenue tier was created was created in other to analyze customer behaviour.

**LOW - VALUE CUSTOMERS**
- Revenue range: 0 - 1,500

- Characteristics: ARPU is 1,248; 

- Segment Size: 25% of the total customers.

- Revenue Contribution: 16% of total Revenue

**MEDIUM - VALUE CUSTOMERS**:

- Revenue range: 1,501 - 2,500

- Characteristics: ARPU is 2,001;

- Segment Size: 50% of the total customers.

- Revenue Contribution: 50% of total Revenue
  
**HIGH - VALUE CUSTOMERS**

- Revenue range: Above 2,500

- Characteristics: ARPU is 2,751; 

- Segment Size: 25% of the total customers.

- Revenue Contribution: 34% of total Revenue
  
### INSIGHTS AND RECOMMENDATION
---

**Key Insights**
- There are no active subscription as of 31st August 2024.
- Customer retention rate is **55%**.
- The highest revenue was generated in November 2023.
- 50% of the customers used the Basic subscription package, making it the most popular package.
- Average Revenue Per User is 1,999.


### EXCEL FILES
---
Attached is my excel workbook used for this analysis.
[Customer Data main.xlsx](https://github.com/user-attachments/files/17624342/Customer.Data.main.xlsx)

**CROSS SECTION OF EXCEL WORKSHEET**
<img width="929" alt="Excel Customer Data" src="https://github.com/user-attachments/assets/50ae382d-0024-4e14-97b3-4cb99827b5e0">


**PIVOT TABLE**
<img width="863" alt="pivot table CD" src="https://github.com/user-attachments/assets/36beb9ed-e5ef-4cee-bb42-a3f262d34725">


### SQL QUERIES
---
``` SQL
SELECT * FROM [dbo].[PROJECT_CustomerData]

CREATE VIEW VW_CustomerData
as
SELECT CustomerID, DATEDIFF(MONTH,subscriptionstart,subscriptionend)
AS [Month Difference] fROM [dbo].[PROJECT_CustomerData]

------------TOTAL NUMBER OF CUSTOMERS IN EACH REGION--------------
SELECT COUNT(CustomerID) AS [Total Number Of Customers], Region FROM [dbo].[PROJECT_CustomerData]
GROUP BY Region
ORDER BY 1 asc

-----------MOST POPULAR SUBSCRIPTION TYPE--------------
SELECT COUNT(CustomerID) AS [Count Of Customers], SubscriptionType FROM [dbo].[PROJECT_CustomerData]
GROUP BY SubscriptionType

-------------CUSTOMERS WHO CANCELED THEIR SUBSCRIPTION WITHIN 6 MONTHS---------------------
SELECT CustomerID, Suscription_Duration FROM [dbo].[PROJECT_CustomerData]
WHERE Suscription_Duration <= 183
                          ---OR---
SELECT CustomerID, [Month Difference] from [dbo].[VW_CustomerData]
WHERE [Month Difference] <= 6

--------------- AVERAGE SUBSCRIPTION DURATION--------------
SELECT CAST (AVG(Suscription_Duration) AS DECIMAL (5,2)) AS [AVG. DURATION] 
FROM [dbo].[PROJECT_CustomerData]

----------------CUSTOMERS WITH SUBSCRIPTION LONGER THAN 12 MONTHS-----------
SELECT CustomerID, [Month Difference] from [dbo].[VW_CustomerData]
WHERE [Month Difference] > 12

----------------TOTAL REVENUE BY SUBSCRIPTION TYPE ---------
SELECT SUM(Revenue) AS [Total Revenue], SubscriptionType 
FROM [dbo].[PROJECT_CustomerData]
GROUP BY SubscriptionType
ORDER BY 2 ASC

----------------TOP THREE REGION BY SUBSCRIPTION CANCELLATION-----------
SELECT TOP 3 Region, COUNT(Canceled) AS [Number Of Cancellation] 
FROM [dbo].[PROJECT_CustomerData ]
WHERE Canceled = 1
GROUP BY Region

----------------TOTAL NUMBER OF ACTIVE AND CANCELLED SUBSCRIPTION--------
SELECT COUNT(Canceled) AS Cancellations, Canceled 
FROM [dbo].[PROJECT_CustomerData ]
GROUP BY Canceled
```

### POWER BI REPORT
---
I created an interactive 3 pages dashboard.

**PAGE 1 - OVERVIEW**
<img width="670" alt="Overview - Page 1CD" src="https://github.com/user-attachments/assets/c1bb1dfc-46cf-44bd-80d0-4037945488bb">


**PAGE 2 - REVENUE TREND**
<img width="607" alt="Revenue Trend - Page 2" src="https://github.com/user-attachments/assets/4a2419d5-544a-4be2-96cb-d2bf2ef430b8">


**PAGE 3 - SUBSCRIPTION TREND**
<img width="611" alt="Subscription Trend - Page 3" src="https://github.com/user-attachments/assets/c4728a82-fcb7-4790-b63d-19d68b3c86e4">


### DOCUMENTATION
---
**DATA DICTIONARY**

My dataset contained 8 columns originally, during the process of analysis, four columns where added. These columns include;

- **Customer ID**: An original column that contained 3 digit code that was unique to the customer.

- **Customer Name**: An original column that contained the first name of the customer.

- **Region**: An original column that showed the region of the customer at the time of subscription.

- **Subscription Type**: An original column which showed the subscription package of the customer.

- **Subscription Start**: An original column which contained the date the customers subscription plan started. This was important in understanding the subscription trend.

- **Subscription End**: An Original column which showed the date the customers subscription ended or was cancelled.

- **Canceled**: An original column that showed customers that canceled their subscription.

- **Revenue**: An original column that shows the revenue generated by each subscription duration.

- **Subscription Length**: A calculated column added in excel that showed how long the customers subscription lasted. It was gotten by subtracting the subscription Start from the subscription End.

- **Revenue Tier**: A conditional column added in excel using the **IFS** function, to summarize the revenue into tiers for easy analysis. It was summarized into **LOW, MEDIUM and HIGH**. **Revenue <1500 was tagged LOW, >1501 is MEDIUM and revenue >2,500 was tagged HIGH**.

- **Revenue Tier Sort**: A conditional column created in the Power BI workspace. It was used to sort the Revenue Tier column.

- **Canceled Sort**: A conditional column created in the BI workspace.

 Various measure was created during the course of the analysis. They include:
- **Average Revenue Per User**

- **Canceled (True)**

- **Churn Rate**

- **Customer Lifetime Value**

- **Customer Retention Rate**

- **Revenue Lost To Churn**

- **Total Customers**

- **Total Revenue**


  #### INSIGHTS AND RECOMMENDATION
