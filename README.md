# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
My project objective is to efficiently clean up this data and generate insightful analysis.


## Process
(your step 1)
1. input CSV file into pg admin
2. trying to understand all given table
3. wrote down data manipulation SQL queries for cleaning data, and making it in a readable format(i.e. changing the time integer to time.)
4. wrote down data SQL queries to solve the assignment.
5. wrote down my data analysis question and solved it using PGADMIN.
6. tried to create an ERD diagram but there are a lot of sufficient data so it's hard to connect them 


## Results
As per my analysis, I discovered that the majority of revenue was generated in the United States with $13,154  and the second is Israel where revenue was generated at $602. 
then I discovered that most of the products sold in the United States with the product category "Home/Apparel/Men's/Men's-T-Shirts".


## Challenges 
First and foremost, I encountered challenges while importing data into the admin, and if any mistakes were made, I had to delete the entire table and repeat the import process, which proved to be time-consuming.

Secondly, during the data cleaning phase, I faced the challenge of handling numerous null values in the dataset, which required extra attention and effort.

Additionally, while creating primary keys in the tables to establish foreign keys and construct my ERD diagram, I discovered multiple duplicate fullvisitorids. This posed a challenge as it meant that some sessions did not have a primary key. However, I realized that by utilizing the "all session" table, I could effectively join all the tables together.

Certain values were found to be present in some tables but missing in others, creating inconsistencies across the dataset.

## Future Goals

Given the opportunity, I would strive to clean the data by normalizing it to at least the second normal form (2NF), or ideally the third normal form (3NF). 
This process would involve creating primary keys and eliminating all null values, resulting in a more structured and organized dataset. 
By achieving normalization, I would enhance the accuracy of data analysis.
