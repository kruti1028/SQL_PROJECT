Answer the following questions and provide the SQL queries used to find the answer.

Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
```sql
    SELECT city, country, sum(total_transactionrevenue) AS "Transaction Revenue" 
    FROM public.all_session 
    WHERE total_transactionrevenue IS NOT NULL and city <> 'not available in demo dataset' 
    GROUP BY city, country 
    ORDER BY "Transaction Revenue" 
    DESC limit 10
```
Answer: The united state is the country which has the highest level of transaction revenue on site


Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```sql

    SELECT DISTINCT country, city, avg(total_ordered) as avg_num_product 
    FROM sales_reports slr 
    JOIN all_session als 
    ON slr."productSKU" = als."productSKU" 
    WHERE city <> 'not available in demo dataset' and country <> '(not set)' 
    GROUP BY city, country, total_ordered
```
Answer: here is the result of the average number of the product ordered from visitors in each city and country where India, South Korea and unite state has the highest average number of product ordered.


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```sql
    SELECT "v2ProductCategory", city, country 
    FROM public.all_session als 
    WHERE city <> '(not set)' AND city <> 'not available in demo dataset' AND country <> '(not set)' 
    GROUP BY "v2ProductCategory", city, country 
    ORDER BY country
```
Answer: I discovered that the Home/Apparels category is among the top categories for shopping and most ordered product.


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**

SQL Queries:
```SQL
    SELECT "productSKU", 
    RANK() OVER(PARTITION BY COUNT("productSKU"),country, city ORDER BY "productSKU") AS productrank,
    "v2ProductName", 
    country, 
    city,
    COUNT("productSKU") AS productcount 
    FROM public.all_session 
    WHERE country <> 'not available in demo dataset' AND city <> '(not set)' AND city <> 'not available in demo dataset' 
    GROUP BY "productSKU", "v2ProductName", country, city 
    ORDER BY productcount DESC 
    LIMIT 10;
```
Answer: According to the data, Google Men's T-shirts appear to be among the top-selling products by country, with a significant number of purchases originating from the United States.


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```SQL
        SELECT p.name, als.city, als.country, sum(als."productPrice" * p.orderquantity) as revenue 
        FROM all_session als 
        JOIN products p 
        ON als."productSKU" = p.productsku 
        WHERE city is not null 
        GROUP BY p.name, als.city, als.country 
        ORDER BY revenue desc;
```
Answer: Based on the data, a significant portion of the product revenue is generated in the United state. Mountain View shows a strong preference for purchasing the "Cam Indoor Security Camera - USA."










