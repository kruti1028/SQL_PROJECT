What are your risk areas? Identify and describe them.

1. Removing Duplicates: The analytics and all_session had quit no duplicate.

2. Handling Missing Data: The all_session table had missing data in the country and the city like "not available in demo dataset.

3. Correcting Typos: in all_ sessions there is a column name type that has only upper case values available I changed it with the proper case.

4. Removed unwanted and irrelevant columns

**QA Process:**
Describe your QA process and include the SQL queries used to execute it.

**Analytics** : 
1. There are many duplicate values in analytics full visitor id and visitor id had multiple duplicate values but visitor numbers were different.

2. Then I took revenue data from both tables. The revenue column from the analytics table had more data than the revenue column from all_session.

3. Userid column is completely null and doesn't have any relevance here. Removed the column for more visibility by using the below query.

```sql
  Alter table analytics
  Drop column user_id

```
4. I had to change time_on_site values because that was given in integer value I changed them with time by using the below query.
```sql
  ALTER TABLE all_sessions 
  ALTER COLUMN time TYPE TIME USING (TIME '00:00:00' + (interval '1 second' * time::integer))
```

**All_session**
1. Few columns like produtrefundamount, itemquantity, itemrevnue, searchkeyword are competly null and don't have any relevance there, so i removed all 4 columns.
   ```sql
    Alter table all_session
    Drop column productrefundamount
    Drop column itemquantity,
    Drop column itemrevenue
    Drop column search keyword
  ```

3. There are almost many columns has missing values, so replace them with zero where are integer values and N/A where are VARCHAR.

4. I have noticed many countries have cities that are not relevant to the country. for example, the country's name is The 'united sate' and its city name is 'France'.

5. I changed some of the column name by using the below function:
```sql
   ALTER TABLE public.all_session
   RENAME COLUMN eCommerceoption TO Ecommerce_option
```

**Sales_report**

1. In the sales report, I noticed that there are duplicate product names. However, each product has a unique SKU (Stock Keeping Unit), which allows for differentiation among multiple products. Considering this, I made the decision to retain the product names in the report.

2. There are null values in the ratio column I changed with the given function:
```sql
UPDATE public.products
SET sentimentmagnitude = CASE WHEN sentimentmagnitude IS NULL THEN 0 ELSE sentimentmagnitude END
WHERE sentimentmagnitude IS NULL;
``` 

**Sales_by_sku**

There aren't any null or duplicate values

**Products**

There aren't duplicate values in the products table.









