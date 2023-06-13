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

1. Redundant columns in all_session. by using below function.
   ```sql
      Alter table all_session
      Drop column productrefundamount
      Drop column itemquantity,
      Drop column itemrevenue
      Drop column search keyword
   ```

2. For all_session table I used below function for remove duplicates.
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

1. For removing duplicate in analytics i used below function.
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


   
   
   
   
   
