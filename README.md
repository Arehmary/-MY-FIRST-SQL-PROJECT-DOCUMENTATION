# -MY-FIRST-SQL-PROJECT-DOCUMENTATION
This is where I started my tech Journey building my Portfolio while taking my Data Analysis class with the incubator hub
 # Project Overview
 In this project you are going to learn Fundamentals of SQL: how to create data base from scratch, import flat files(CSV),Modify Column ,how to number your query , select table and work on casestudy  (KMS Inventory) Problems and solutions queries and recommendation.
 # Table of Content for the Portfolio

   - 	Data Sources
   - 	Tools used
   - 	How to create data base
   - 	How to import Flat Files(CSV)
   - 	How to number your query
   -  Exploratory Data Analysis 
   - 	Case study problems and Solutions(Kultra Mega Store Inventory
   -	Recommendation


  ## Data Source
  The primary source of Data used here is CSV and this is an open source data that can be freely downloaded from an open source online or other data repository site.

  ## Tools Used
  Microsoft  SQL Server  Studio

  ## How To Create a Data Base

  To Create data base ,type on the white background
 Create Database KMSinventory_DB
Note when it shows red it means there is an error, once it does not give you error you can execute,You then get a message that commands has been completed. To confirm if database has been completed go to your database ,right click on it  and refresh, go to database button refresh it, you are going to se your new database created.

## How To Import Flat Files(CSV)
  Always confirm the source of data before you import your data to a destination, pay attention to the number of records. To import CSV File click on the database where you want your table to be saved .Go click on the  the  database you created ,right click on it,go to tasks from tasks navigate to import flat. files, review the files then modify the column by changing order id to int and changing sales, discount, profit, unit price shipping cost and any data type name float to be checked under allow null.

## How to Number Your Query

 Go to tools at the right the right from the left corner side you will see tool beside project, click on tools you will see options, scroll down and navigate to options ,once you click on the options navigate to text editor then move to transact SQL and navigate to Line number and click on it, automatically it will enable number  for you.


## Exploratory Data Analysis
EDA involved the exploring of the data to answer some question about the data such as :
1. Which product category had the highest sales? 
2. What are the Top 3 and Bottom 3 regions in terms of sales? 
3. What were the total sales of appliances in Ontario? 
4. Advise the management of KMS on what to do to increase the revenue from the bottom 
10 customers 
5. KMS incurred the most shipping cost using which shipping method?
 Case Scenario II 
6. Who are the most valuable customers, and what products or services do they typically 
purchase? 
7. Which small business customer had the highest sales? 
8. Which Corporate Customer placed the most number of orders in 2009 – 2012? 
9. Which consumer customer was the most profitable one? 
10. Which customer returned items, and what segment do they belong to? 
11. If the delivery truck is the most economical but the slowest shipping method and 
Express Air is the fastest but the most expensive one, do you think the company 
appropriately spent shipping costs based on the Order Priority? Explain your answer
 
## Case Study Problems and Solutions (Kultra Mega Store  inventory)

Case Scenario I 
1.	Which product category had the highest sales? 
GROUP BY, SUM (), AND ORDER BY CLAUSES ARE USED
Sequel Query:
select Product_Category, SUM(distinct Row_ID) as TotalSales
from Inventory
group by Product_category
order by TotalSales desc


2.	What are the Top 3 and Bottom 3 regions in terms of sales? 
 a.	Top 3 regions by sales
 Sequel Query Used:
 Select top 3 Region, SUM(Sales) AS TotalSales
 from Inventory
 group by Region
 order by TotalSales desc

  2b. Bottom 3 regions in terms of sales
  GROUP BY, SUM (), AND ORDER BY CLAUSES ARE USED
  Sequel query used:
  Select top 3 Region, SUM(Sales) AS TotalSales
  from Inventory
  group by Region
  order by TotalSales asc

   3. What were the total sales of appliances in Ontario? 
  GROUP BY, SUM (), AND ORDER BY CLAUSES ARE USED
  Sequel Query Used:
  SELECT Region,  Product_Sub_Category, SUM(Sales) AS TotalSales
  FROM Inventory
  WHERE Region = 'Ontario'
  AND Product_Sub_Category = 'Appliances' 
  GROUP BY Region,  Product_Sub_Category
  ORDER BY TotalSales desc

  4.	Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers 
  GROUP BY, SUM (), AND ORDER BY CLAUSES ARE USED
  Squel Query Used:
  Select top 10 Customer_Name, SUM(Sales) AS TotalSales
  from Inventory
  group by Customer_Name
  order by TotalSales asc

 5, KMS incurred the most shipping cost using which shipping method?
 GROUP BY, SUM (), AND ORDER BY CLAUSES ARE USED
 Sequel Query Used: 
 Select top 5 Ship_Mode, SUM(Shipping_Cost) AS TotalShipping_Cost
  from Inventory
  group by Ship_Mode
  order by TotalShipping_Cost desc


 Case Scenario II 
 6. Who are the most valuable customers, and what products or services do they typically purchase? 
 a. Who are the most valuable customers?
 Sequel Query Used
 SELECT top 5 Customer_Name, SUM(Order_Quantity*Unit_Price) AS TotalRevenue
 FROM Inventory
 GROUP BY Customer_Name
ORDER BY TotalRevenue DESC


 7. Which small business customer had the highest sales? 
 GROUP BY, SUM (), AND ORDER BY CLAUSES ARE USED
 Sequel Query Used:
 SELECT TOP 1 Customer_Segment, Customer_Name, SUM(Sales) AS TotalSales
 FROM Inventory
 WHERE Customer_Segment = 'Small Business'
 GROUP BY Customer_Segment, Customer_Name
 ORDER BY TotalSales desc


 8. Which Corporate Customer placed the most number of orders in 2009 – 2012? 
 Sequel Query Used

 SELECT top 1 Customer_Name, Customer_Segment,
 Count(Order_ID) AS TotalOrders
 FROM Inventory
 WHERE Customer_Segment = 'Corporate'
 AND Year (Order_Date) BETWEEN 2
 009 AND 2012
 GROUP BY Customer_Name, Customer_Segment
 ORDER BY TotalOrders desc;

 9. Which consumer customer was the most profitable one? 
 Sequel Query Used:
 SELECT top 1 Customer_Segment, Customer_Name, SUM(Profit) AS TotalProfit
 FROM Inventory
 Where Customer_Segment = 'Consumer'
 GROUP BY Customer_Name, Customer_segment
 ORDER BY TotalProfit DESC


 10. Which customer returned items, and what segment do they belong to? 
 Sequel Query Used:
 SELECT DISTINCT o.[Order_ID], o.[Customer_Name], o.[Customer_Segment]
 FROM Inventory o
 JOIN [dbo].[Order_Status] r 
 ON o.[Order_ID] = r.[Order_ID]
 WHERE r.Status = 'Returned';

  11, If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company     appropriately spent shipping costs based on the Order Priority? Explain your answer
  Sequel Query Used:
SELECT 
    Order_Priority,
    Ship_Mode,
    COUNT(Order_ID) AS orderCount,
    Round(SUM(Sales - Profit), 2) AS Estimatedshippingcost,
   AVG(DATEDIFF(day, [Order_Date], [Ship_Date])) AS AvgShipDays
   FROM Inventory
  GROUP BY Order_Priority, Ship_Mode
 ORDER BY Order_Priority, Ship_Mode desc

# Recommendation
Kultra Mega Stores (KMS) does not consistently align shipping methods with order priorities. A policy review is needed to ensure that:
1.	Standardize Shipping Rules:
Express Air only for Critical/High priority.
Delivery Truck for Low priority, but only if cheaper.
2.	Audit Delivery Truck Usage:
Costs are consistently higher, with no delivery speed advantage.
3.	Enforce Priority Labelling:
Avoid "Not Specified" to make informed shipping decisions.
4.	Optimize Cost-Effectiveness:
Favor Express Air when it is both faster and cheaper (as seen here).
Proper controls need to be put in place to reduce costs and match urgency with speed.
