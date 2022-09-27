# MAVEN DATA CHALLENGES
# Introducing the Maven Pizza Challenge
 # 	Here are some questions that we'd like to be able to answer:

•	What days and times do we tend to be busiest?

•	How many pizzas are we making during peak periods?

•	What are our best and worst selling pizzas?

•	What's our average order value?

•	How well are we utilizing our seating capacity? (we have 15 tables and 60 seats)


# About the dataset

•	This dataset contains 4 tables in CSV format
•	The Orders table contains the date & time that all 5,238 table orders were placed
•	The Order Details table contains the different pizzas served with each order in the Orders table, and their quantities
•	The Pizzas table contains the size and price for each distinct pizza in the Order Details table, as well as its broader pizza type
•	The Pizza Types table contains details on the pizza types in the Pizzas table, including their name as it appears on the menu, the category it falls under, and its list of ingredients

# Data Extraction 

Downloaded the dataset from Maven Analytics data playground. Link of the website below -
https://www.mavenanalytics.io/blog/maven-pizza-challenge?utm_source=linkedin&utm_campaign=pizzachallengelaunch_bp20220921 

# ETL 
After successful ETL process tables are loaded in Power BI.

![image](https://user-images.githubusercontent.com/16399584/192463787-b51460b4-3cd1-4937-aa1b-84979158468a.png)

 
# Data Model
![image](https://user-images.githubusercontent.com/16399584/192463989-6142a7df-890c-42f8-b66d-c936b244b9a7.png)


 
# Dashboard
 
 ![image](https://user-images.githubusercontent.com/16399584/192464059-ba7035cf-ef91-4e00-8768-ab41c71ab733.png)


# Measures and DAX 
Revenue = 
SUMX(order_details,order_details[quantity] * RELATED(pizzas[price]))

Average Order $ = [Revenue]/COUNT(orders[order_id])

Times Of the Day = 
VAR HOUR_PART= TIME(HOUR(orders[time]), MINUTE(orders[time]), second(orders[time]))

 RETURN
 
SWITCH(
    TRUE(),
  HOUR_PART > time( 06, 00, 00) 
   && HOUR_PART < time( 06, 59, 00) , time( 06, 00, 00) ,  
    HOUR_PART > time( 07, 00, 00) 
   && HOUR_PART < time( 07, 59, 00) , time( 07, 00, 00) , 
    HOUR_PART > time( 08, 00, 00) 
   && HOUR_PART < time( 08, 59, 00) , time( 08, 00, 00) ,
    HOUR_PART > time( 09, 00, 00) 
   && HOUR_PART < time( 09, 59, 00) , time( 09, 00, 00) ,
    HOUR_PART > time( 10, 00, 00) 
   && HOUR_PART < time( 10, 59, 00) , time( 10, 00,00) ,
    HOUR_PART > time( 11, 00, 00) 
   && HOUR_PART < time( 11, 59, 00) , time( 11, 00, 00) ,
    HOUR_PART > time( 12, 00, 00) 
   && HOUR_PART < time( 12, 59, 00) , time( 12, 00, 00) ,
    HOUR_PART > time( 13, 00, 00) 
   && HOUR_PART < time( 13, 59, 00) , time( 13, 00, 00) ,
   HOUR_PART > time( 14, 00, 00) 
   && HOUR_PART < time( 14, 59, 00) , time( 14, 00, 00) ,  
    HOUR_PART > time( 15, 00, 00) 
   && HOUR_PART < time( 15, 59, 00) , time( 15, 00, 00) , 
    HOUR_PART > time( 16, 00, 00) 
   && HOUR_PART < time( 16, 59, 00) , time( 16, 00, 00) ,
    HOUR_PART > time( 17, 00, 00) 
   && HOUR_PART < time( 17, 59, 00) , time( 17, 00, 00) ,
    HOUR_PART > time( 18, 00, 00) 
   && HOUR_PART < time( 18, 59, 00) , time( 18, 00, 00) ,
    HOUR_PART > time( 19, 00, 00) 
   && HOUR_PART < time( 19, 59, 00) , time( 19, 00, 00) ,
    HOUR_PART > time( 20, 00, 00) 
   && HOUR_PART < time( 20, 59, 00) , time( 20, 00, 00) ,
    HOUR_PART > time( 21, 00, 00) 
   && HOUR_PART < time( 21, 59, 00) , time( 21, 00, 00) ,
   HOUR_PART > time( 22, 00, 00) 
   && HOUR_PART < time( 22, 59, 00) , time( 22, 00, 00) ,
    HOUR_PART > time( 23, 00, 00) 
   && HOUR_PART < time( 23, 59, 00) , time( 23, 00, 00) ,
     time( 24, 00, 00)
)




Week Day = WEEKDAY(orders[date],2)


