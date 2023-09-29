**What issues will you address by cleaning the data?**
1. Removing duplicate values
2. Removing null values in some columns
3. Fixing time and price in the proper format
4. Ensuring accurate data type
5. Fill in missing values
6. Transfor unit cost to decimal points

**Queries:**
Below, provide the SQL queries you used to clean your data.

**All_session**

1. Redundant columns in all_session. by using the below function.
   delete in all_session's productrefundamount, itemquantity, item revenue, and searchkeyword columns. because all those columns were fully null.
   ```sql
      Alter table all_session
      Drop column productrefundamount
      Drop column itemquantity,
      Drop column itemrevenue
      Drop column search keyword
   ```

3. For the all_session table I used the below function to remove duplicates.
   used this function to verify duplicate values.
```sql
   delete from public.all_session 
   where "fullVisitorId" in 
      (select "fullVisitorId", visitid, transactionid
      from (select "fullVisitorId", country, city, date, visitid,
                   row_number() over(partition by "fullVisitorId", country, city, date, visitid order by "fullVisitorId" ) as dup
                         from public.all_session) as uni
       where dup > 1)
```

**Analytics**

1. Removed redundant column
   I removed the user-id column because the column is fully null.
```sql
     ALTER TABLE analytics 
     DROP COLUMN userid;
```

1. For removing duplicates in analytics I used the below function.
```sql   
      select *, ctid
      from analytics
```
```sql
   delete from analytics
   where ctid in (select max(ctid)
   from public.analytics
   group by visitnumber, visitid, 
				visitstarttime, date, fullvisitorid, 
				 channelgroup, socialengagementtype, 
				unit_sold, pageview, timeonsite, 
				 bounces, revenue, unit_price
   having count(*) > 1)
```

3. Transfer unit price with division of 100,00,00
   My data type was an integer so I had to change the data type to decimal data type.
```SQL
   Alter table  "Analytics"
   Alter column revenue type decimal
   Using revenue :: decimal
```
Then I divided the unitprice into 100,00,00
```SQL
   update "Analytics" 
   set revenue = (revenue/1000000)
```
The unit price value has many decimal points so I round it with the given function.
```SQL
   UPDATE "Analytics"
   SET revenue = ROUND(revenue::numeric, 6)
```

**Products**

there were no duplicate values in the product table and no redundant column.

**Sales by SKU**

No need to clean/transform data. It was in good condition.

**Sles report**

No need to clean/transform data. It was in good condition.






   
   
   
   
   
