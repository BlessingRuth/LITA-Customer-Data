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

- The total revenue made is "$67,540,175"
- The count of total subscription is "33,788". we realized some subscriprions were canceled while some were retained and the total number of subscription that is active is 18613 while the total number of canceled subscription is "15,175". 45% of the subscription were canceled while 55% of the subscription was retained which isnt a good perfomance.For over 40% of the subscribers to cancel their subscriptions, it shows that a lot of people were displeased with the service which isnt a good thing for the company.
- Revenue made by each subscription type: Basic made $33,776,735, Premium made 16,899,064 while standard made 16,864,376. This ananlysis shows that Basic made the highest revenue, with premium and standard following behind by a huge gap. This shows that a lot of subscribers went for the basic because it was afordable.
- Revenue made by each  region: East made $16,958,763( 25%), South: $16,899,064 (25%), West $16,864,376 (24.9%), North: $16,817972(24.9%).
 which shows all the regions are in good standing and they did well with no region lagging behind another.
- After analyzing the data, we deduced that 45% subscriptions were canceled with 55% being retained
- Basic made up 33.3%, Premimum made up 33.3% and Standard made up 33.2% of canceled subscription. Even though the three subscription type had almost the same ratio of canceled subscription, the ratio of the subcribed customers is still different.
- The total rate of Basic subscription type canceled subscription is 30% while 70% was retained, The total rate of Premium subscription type canceled is 60% while 40% was retained, The total rate of Standard subscription type canceled subscription is 60% while 40% was retained.The rate at which both premium and standard subscription is being canceled is quite alarming and needs to be reviewed immediately to avoid being at a disadvantage with their competitor.Most subscribers of both Premium and Standard subscription type subscribed to it because it is believed to have more quality package compare to basic since it is more expensive but with the rate at which it is being canceled, it shows that the subscribers are not getting what they believed they subscribed to. Also, the 30% rate of canceled basic subscription type is still not off the hook, it needs to be controlled. 
- The total rate of canceled subscription in the East is 0%, North is 60%, South is 60% while West is 60%. This shows that something is being done right in the East that hasnt been discovers by other regions as almost all the retained subscribers are from the East.

  ### Recommendations
- A lot of of rebranding and repackaging should be done to the subscriptions to make customers retain their subscriptions more
- There  should also be a rebranding among the staff to give room for new ideas to yield different results.
- Both Premium and Standard subscription type should be upgraded to give people quality for their money
- What is being done right in the East should be observed and implemented in other regions.
- Advertisement should be invested heavily into to make subscribers and targeted subscribers know that the servicw has been rebranded.
-  Opinion of subscribers should be gotten through forms or questionaires to know how to be better. 
  
  





 
