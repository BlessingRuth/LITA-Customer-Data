# LITA-Customer-Data

### Table of content
- [project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools Used](#tools-used)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Insights](#insights)
- [Recommendations](#recommendations)
- [Data description](#data-description)



### Project Overview
---
This project analyzes customer data for a subscription service to identify segments and trends in behavior, subscription types, and cancellation patterns. The findings are presented in a Power BI dashboard for easy visualization and decision-making.

### Data Description

The dataset includes the following variables:

-CustomerID : A uniques identification of each customer

-Customer Name : Names of the customers
-Region : The regions where the subscriptions occured
-Subscription Type : Type of subscription purchased
-Subscription Start: The date of subscription
-Subscription End : the date of subscription expiration
-Canceled : If the subscription was canceled or not
-Revenue : The revenue generated from each purchased
-Subscription Duration : The duration of each purchased subscription

###Data Sources
---
Customer data:The primary data used for this analysis is "LITA Customerdata.Csv" file containing detailed information about the subcription pattern. 

###

Tools used 
---
- Excel - Data cleaning and Analysis [*Download here*](https://www.microsoft.com/en-ng/)
- Sql Server - Data Analysis [*Download here*](https://www.microsoft.com/EN-US/SQL-SERVER/SQL-SERVER-DOWNLOADS)
- Powerbi - Creating Reports - [*Download here*](https://powerbi.microsoft.com/desktop/)

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
- Subscription trend: Pivot table was used to find subscription pattern by summarizing Subscription start by count of canceled,Region by count of Subscription type, count of subscriber for each subscription type. hi
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

### Visualization analysis with powerbi dashboard

![Screenshot 2024-11-07 171816](https://github.com/user-attachments/assets/20aa4953-b687-417b-b466-7f6af48c1c77)

  ![Screenshot 2024-11-07 164935](https://github.com/user-attachments/assets/9be9a01c-5343-47b5-9579-d9aee9851e58)

### Insights
---
- The total revenue generated amounts to $67,540,175, with a total subscription count of 33,788. It is important to note that while some subscriptions were retained, others were canceled. Currently, there are 18,613 active subscriptions, and 15,175 have been canceled. This indicates that 45% of subscriptions were canceled, while 55% were retained. Such a high cancellation rate raises concerns about customer satisfaction and overall service quality, suggesting that a significant number of subscribers were dissatisfied.

- Breaking down revenue by subscription type, the Basic plan generated $33,776,735, while the Premium and Standard plans generated $16,899,064 and $16,864,376, respectively. The data indicates that the Basic plan is the most popular, likely due to its affordability compared to the other plans.

- When analyzing revenue by region, the results are as follows: the East generated $16,958,763 (25%), the South $16,899,064 (25%), the West $16,864,376 (24.9%), and the North $16,817,972 (24.9%). This distribution suggests that all regions are performing well, with no significant disparities among them.

- From our analysis, we confirmed that 45% of subscriptions were canceled and 55% were retained. The cancellation rates for each subscription type are as follows: Basic subscriptions accounted for 30% cancellations (70% retained), while both Premium and Standard subscriptions had a 60% cancellation rate (40% retained). The high cancellation rates for Premium and Standard subscriptions are concerning and warrant immediate review to maintain competitiveness. Subscribers often choose these higher-priced options expecting superior quality, yet the cancellation rates indicate that their expectations are not being met. 

- Additionally, the cancellation rates by region reveal that the East has a remarkable 0% cancellation rate, while the North, South, and West each have a 60% cancellation rate. This suggests that the East has implemented successful strategies that should be investigated further to enhance retention in other regions.



  ### Recommendations
---
- A significant rebranding and repackaging of the subscriptions is necessary to enhance customer retention.
- There should also be a rebranding among the staff to allow for new ideas that can lead to different outcomes.
- Both the Premium and Standard subscription types need to be upgraded to provide better value for customers.
- Strategies that are successful in the East should be analyzed and applied in other regions.
- There should be a strong investment in advertising to ensure that both current and potential subscribers are aware of the rebranding.
- It’s important to gather subscriber opinions through forms or questionnaires to identify areas for improvement.





 
