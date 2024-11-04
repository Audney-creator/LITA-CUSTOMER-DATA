### LITA-CUSTOMER-DATA
### CUSTOMER SEGMENTATION FOR A SUBSCRIPTION SERVICE
---

[PROJECT OVERVIEW](project-overview)

[Tools Used](tools-used)

[Project Steps And Analysis](project-steps-and-analysis)

[Excel Analysis](excel-analysis)

[SQL Analysis](sql-analysis)

[Power BI Dashboard](power-bi-dashboard)

[Conclusions](conclusions) 

## PROJECT OVERVIEW
---
This project analyzes customer data from a subscription service to identify customer segments and subscription trends. The objective was to understand customer behavior, track popular subscription types, and identify trends in cancellations and renewals.

## Tools Used
---
- Excel: For initial data exploration and pivot table analysis.

- SQL: For deeper data querying and trend analysis.
  
- Power BI: For visualizing insights through an interactive dashboard.

## Project Steps And Analysis
---
## Excel Analysis
# - Objective:
Explore subscription patterns and calculate key metrics.

# - Steps Taken:
   - Created pivot tables to analyze subscription durations and identify popular subscription types.
     
   - Calculated the average subscription duration and determined the most common subscription types.
     
   - Generated charts and other visuals to illustrate trends in subscription types and duration.

     
# - Key Findings:
  - The most popular subscription type was # Basic.
    
  - The average subscription duration was # 365 days.
    
# Visuals: 

![Screenshot (35)](https://github.com/user-attachments/assets/c988ba5e-c4b0-4304-8b35-5a1bc20b5205)

![Screenshot (36)](https://github.com/user-attachments/assets/a134aa4f-faa2-447c-9f5e-292a52ba60ed)

![Screenshot (37)](https://github.com/user-attachments/assets/26ca79d2-aa1d-4619-9d24-8ed6ab6fa36b)



## SQL Analysis
# - Objective: 
Run queries to uncover trends and answer specific business questions.

## - Steps taken:
- Loaded the dataset into an SQL environment to run queries on customer behavior and subscription trends.
- Ran queries to find insights such as:
   - Total customers by region.
     
   - Most popular subscription type by customer count.
 
   - Customers who canceled within six months.
     
   - Average subscription duration.
     
   - Number of customers with long-term subscriptions (over 12 months).
     
   - Total revenue per subscription type.
     
   - Regions with the highest cancellation rates.
     
   - Counts of active vs. canceled subscriptions.
     
## - Key Insights:
1. The region with the most customers was [insert region].
   
2. The subscription type generating the highest revenue was [insert type].
   
3. The top three regions by cancellations were [insert regions].
 

## - QUERIES: 
```sql
CREATE DATABASE CUSTOMER_DATA_REPORT

SELECT *FROM[dbo].[CUSTOMERDATAR]

----TOTAL NUMBER OF CUSTOMER FOR EACH REGION---
SELECT REGION,COUNT(CUSTOMERID) AS TOTALCUSTOMER FROM CUSTOMERDATAR
GROUP BY REGION

----THE MOST POPULAR SUBSCRIPTION TYPE BY NUMBER OF CUSTOMERS---
SELECT TOP 1 SUBSCRIPTIONTYPE,COUNT(CUSTOMERID) AS TOTALCUSTOMER FROM CUSTOMERDATAR
GROUP BY SUBSCRIPTIONTYPE
ORDER BY TOTALCUSTOMER DESC

----CUSTOMERS WHO CANCELLED THEIR SUBSCRIPTION WITHIN 6 MONTHS----
SELECT CUSTOMERID,CUSTOMERNAME,REGION,SUBSCRIPTIONTYPE,SUBSCRIPTIONSTART,SUBSCRIPTIONEND,SUBSCRIPTION_DURATION FROM CUSTOMERDATAR
WHERE CANCELED = 1
AND SUBSCRIPTIONEND BETWEEN SUBSCRIPTIONSTART 
AND DATEADD(MONTH,6,SUBSCRIPTIONSTART)

---AVERAGE SUBSCRIPTION DURATION FOR ALL CUSTOMERS-----
SELECT CUSTOMERID,AVG(SUBSCRIPTION_DURATION) AS AVERAGESUBSCRIPTIONDURATION FROM CUSTOMERDATAR
GROUP BY CUSTOMERID

----CUSTOMERS WITH SUBSCRIPTIONS LONGER THAN 12 MONTHS---
SELECT CUSTOMERID,CUSTOMERNAME,REGION,SUBSCRIPTIONTYPE,SUBSCRIPTIONSTART,SUBSCRIPTIONEND,SUBSCRIPTION_DURATION FROM CUSTOMERDATAR
WHERE SubscriptionEnd IS NOT NULL
AND DATEDIFF(MONTH, SUBSCRIPTIONSTART, SUBSCRIPTIONEND) > 12

----TOTAL REVENUE BY SUBSCRIPTION TYPE----
SELECT SUBSCRIPTIONTYPE,SUM(REVENUE) AS TOTALREVENUE FROM CUSTOMERDATAR
GROUP BY SubscriptionType

----TOP 3 REGIONS BY SUBSCRIPTION CANCELATION---
SELECT TOP 3 REGION,COUNT(CANCELED) AS SUBSCRIPTIONCANCELATION FROM CUSTOMERDATAR
WHERE CANCELED = 1
GROUP BY REGION

----TOTAL NUMBER OF ACTIVE AND CANCELED SUBSCRIPTION----
SELECT 
CASE WHEN CANCELED = 1 THEN 'CANCELED' ELSE 'ACTIVE' END AS POSITION,
COUNT(*) AS TOTALNUMBER FROM CUSTOMERDATAR
GROUP BY CANCELED


```




## Power BI Dashboard
## - Objective:
Visualize the analysis and make insights easily accessible.

## - Steps taken:
- Created a dashboard with visuals to highlight customer segments, popular subscription types, and trends in cancellations and renewals.
  
- Included slicers for interactive filtering by region, subscription type, and customer status.
  
## - Key Visuals:
- Subscription Overview: Displays overall subscription trends and most popular types.
- Cancellation and Renewal Trends: Visualizes cancellation rates across regions.
- Regional Analysis: Highlights customer segments by region.

## - Visuals:

![Screenshot (29)](https://github.com/user-attachments/assets/eefa74f8-9ce2-4554-8302-e8159ec75a1f)

![Screenshot (30)](https://github.com/user-attachments/assets/000cc75c-47f8-40f6-961c-c04f4ab3f99b)



## Conclusions 
---
This analysis provided a detailed view of subscription patterns, popular customer segments, and areas with high cancellation rates, helping the business understand customer retention and product popularity.and to make business decisions around service improvements.


