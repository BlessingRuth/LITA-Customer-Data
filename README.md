# LITA-Customer-Data

### Table of content
- [project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools Used](#tools-used)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)



### Project Overview
---
This project analyzes customer data for a subscription service to identify segments and trends in behavior, subscription types, and cancellation patterns. The findings are presented in a Power BI dashboard for easy visualization and decision-making.

###Data Sources
---
Customer data:The primary data used for this analysis is "LITA Customerdata.Csv" file containing detailed information about the subcription pattern. 

###

Tools used 
---
- Excel - Data cleaning and Analysis [*Download here*](https://www.microsoft.com/en-ng/)
- Sql Server - Data Analysis [Download here] (
- Powerbi - Creating Reports - [Download here] (

  ### Data cleaning and Preparation
---
  In the initial data preparation phase, we performed the following task:
  1. Data loading/Inspection
  2. Delete duplicate data
  3. checked for missing values
  4. check for null values
  5. After Loading the dataset to our database management, it was previewed, the duplicates were removed using distinct and a view was created to work with the clean data.

  ### Exploratory Data Analysis
---
  EDA invloved exploring the sales data to answer key questions, such as:

  - The most popular subscription
  - The average subscription duration
  - Total number of customers from each region
  - Total revenue from each subscription type
  - Top 3 regions by subscription cancelation
  - Total number of active and canceled subscription

# Data Analysis

### Excel Analysis
---
- Subscription trend: Pivot table was used to find subscription pattern by summarizing Subscription start by count of canceled,Region by count of Subscription type, count of subscriber for each subscription type.
- New Columns( Subscription duration): Calculated the time difference between subscription start and subscription end for each subscriber.which was gotten Average subscription duration. 
- Revenue and loss:To get an insight of revenue made overtime and loss incurred. 
Region by sum of revenue, Subscription type by count of canceled,subscription type by total sum of revenue.
- The most popular subscription type was gotten by analyzing the sum of revenue gotten from each subscription type and the by count of the subscription types scubscribed to.

  ![Screenshot 2024-11-06 130834](https://github.com/user-attachments/assets/d08a6774-db5b-478b-a032-0a7c14510acf)
  ![Screenshot 2024-11-06 131500](https://github.com/user-attachments/assets/cb905d8e-443c-4ff4-8dd2-7e8142b9a3c6)



  ### SQL Analysis
  ---
After Loading the dataset to our database management, it was previewed, the duplicates were removed using distinct and a view was created to work with the clean data.
Some of the interesting codes we worked with in analysing our data are:

     
    
  create view VW_Customer_Data
as
select distinct * from [dbo].[LITA Capstone Customer Data]

select * from [dbo].[VW_Customer_Data]

### 1.Total number of customers from each region

```
select count(CustomerID) as No_ofcustomers, Region
from [dbo].[VW_Customer_Data]
group by region
```

### 2.Most popular subcription type by number of customer
```
select SubscriptionType,  count (CustomerID)
from [dbo].[VW_Customer_Data]
group by SubscriptionType
```

### 3.Customers whose subscription got canceled within 6 months---
```
select customerId, Canceled
from [dbo].[VW_Customer_Data]
where Canceled = 0 and Datediff(Month, Subscriptionstart, SubscriptionEnd) <=6
```

### 4.Average subscription duration for all customers---
```
select Avg(subcription_duration), CustomerID
 from [dbo].[VW_Customer_Data]
group by  customerid
```

### 5.Customers with subscription longer than 12 months---
```
select customerId,subcription_duration 
from [dbo].[VW_Customer_Data]
where subcription_duration >365
```
### 6.Calculate Total Revenue by Subscription type---
```
select sum(Revenue), SubscriptionType
from [dbo].[VW_Customer_Data]
group by subsription
```


### 7.Top 3 Regions by Subcription Cancellation---
```
select Top 3 count(canceled), region
from [dbo].[VW_Customer_Data]
where Canceled = 0
group by region
order by 1 desc
```
### 8.Total number of active and canceled subscriptions----
```
select count(canceled) 
from [dbo].[VW_Customer_Data]
where canceled = 0 
```
select count(canceled) 
from[dbo].[VW_Customer_Data]
where canceled = 1



### 9. Most canceled subcription type by number of customer--
```
select SubscriptionType,count (Canceled)
from [dbo].[VW_Customer_Data]
where Canceled = 0
group by SubscriptionType
```
select SubscriptionType,  count (CustomerID)
from [dbo].[VW_Customer_Data]
group by SubscriptionType


  
     ![Screenshot 2024-11-07 171816](https://github.com/user-attachments/assets/e58747e4-8995-4e2b-9b21-f9e2f4fe020f)


![Screenshot 2024-11-07 171816](https://github.com/user-attachments/assets/20aa4953-b687-417b-b466-7f6af48c1c77)

  




 
