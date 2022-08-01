# Sales-dashboard

In this project i used sql queries in mysql to get a overview of data and to analyse data of a  hardware company's sales & PowerBI for ETL(Extract,Transform,and Load) and Visualization to develop meaningful insights 
The database contains 5 tables: customers, date, markets, products, and transactions;

# Data Analysis Using SQL
checking the type of data present in vairious tables.

1. Show all customer records

SELECT * FROM customers;

2.Show total number of customers

SELECT count(*) FROM customers;

3.Show transactions for Mumbai market (market code for Mumbai is Mark002

SELECT * FROM transactions where market_code='Mark002';

4.Show distrinct product codes that were sold in Mumbai

SELECT distinct product_code FROM transactions where market_code='Mark002';

checking for uniformity in the curerrency data. 

5.Show transactions where currency is US dollars

SELECT * from transactions where currency="USD"

6.Show transactions in 2020 join by date table

SELECT transactions , date 
FROM transactions 
INNER JOIN date 
ON transactions.order_date=date.date where date.year=2020;

after thorough checking i came to know that there are two types of data in currency one in rupees and other in usd.

7.Show total revenue in year 2020,

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";

8.Show total revenue in year 2020, January Month,

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");

9.Show total revenue in year 2020 in Chennai

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";

# Data Analysis Using Power BI

1.importing data from sql into power bi. 

2.using transform data tool to check for errors present in the database. 

3.Formula to create norm_amount column

= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)

4.deleting the old column

 = Table.RemoveColumns(#"Filtered Rows1",{"sales_amount"})
 
5. revising new column
 = Table.TransformColumnTypes(#"Renamed Columns",{{"sales_amount", type number}})
6. ![sales dashboard](https://user-images.githubusercontent.com/101324556/157646400-d0b6ab51-e1eb-4d1b-a053-73d6d6ad69ee.png)
