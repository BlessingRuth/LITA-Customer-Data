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

  EDA invloved exploring the sales data to answer key questions, such as:

  - The most popular subscription
  - The average subscription duration
  - Total number of customers from each region
  - Customers who canceled their subscription within 6 months
  - Customers with subscription longer than 12 months
  - Total revenue by subscription type
  - Top 3 regions by subscription cancelation
  - Total number of active and canceled subscription

# Data Analysis

### Excel Analysis

- Subscription trend: Pivot table was used to find subscription pattern by summarizing Subscription start by count of canceled,Region by count of Subscription type, count of subscriber for each subscription type.
- New Columns( Subscription duration): Calculated the time difference between subscription start and subscription end for each subscriber.
- Revenue and loss:
Region by sum of revenue, Subscription type by count of canceled,subscription type by total sum of revenue.
- The most popular subscription type was gotten by analyzing the sum of revenue gotten from each subscription type and the by count of the subscription types scubscribed to.

  ### SQL Analysis
After Loading the dataset to our database management, it was previewed, the duplicates were removed using distinct and a view was created to work with the clean data.
  
  We query the database to analyse the dataset and the following analyzes were gotten:
  1. The total number of customers in each region
  2. The most popular subscription type
  3. subscriptions that were canceled within 6 months
  4. Average Subscription duration
  5. Subscription duration longer than 6 months
  6. Total revenue by subscription type
  7. Top 3 regions by subscription cancelation
  8. Total number of active and canceled subscriptions
  9. Most canceled subscription type.

     Some of the interesting codes we worked with:
     ''' sql
     select *
     '''
     


  




 
