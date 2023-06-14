Question 1: Retrieve repeated visitors in the month of May and in the year 2017

SQL Queries:
```sql
  select count("fullVisitorId") as repeated_visitor,"fullVisitorId",  extract(month from date) as visitingmonth, extract(year from date) as visitingyear
  from public.all_session
  where extract(month from date) ='05' and extract(year from date) = '2017' 
  group by date, "fullVisitorId"
  having count("fullVisitorId") >1 
```

Answer: There are only 21 visitors who visited repeatedly in the month of May and the year 2017

Question 2: Retrieve the top 5 unique visitors who visited products more than one time.

SQL Queries:
```sql
  select distinct "visitId", 
    count("v2ProductName") as multipulproducts, "v2ProductName"
  from public.all_session
  group by "visitId", "v2ProductName"
  having count("v2ProductName") > 1
  limit 5
```
Answer: Here is the top 5 customer who visited a one product more than one time.
    
<img width="587" alt="Screenshot 2023-06-13 at 4 26 44 PM" src="https://github.com/kruti1028/SQL_PROJECT/assets/126723087/3ee62829-d711-4358-be7f-9bc552b6923f">


Question 3: Retrieve the average time on site spent by the visitors who spent nearly 2 minutes.

SQL Queries:
```sql
  select avg(timeonsite),visitid
  from public.analytics
  where timeonsite != '01:59:00'
  group by visitid
```

Answer: There are 9 visitors who visited more than 1 minute

<img width="223" alt="Screenshot 2023-06-13 at 4 36 52 PM" src="https://github.com/kruti1028/SQL_PROJECT/assets/126723087/a803654f-1559-4cf4-8547-93ccb8ced27f">

Question 4: Retrieve the highest stock level products.

SQL Queries:
```sql
  select rank() over (partition by "stockLevel",name) as stocklevelrank, 
       name
  from public.sales_reports
  order by "stockLevel"
```
Answer: The stock level for alpine-style backpacks is currently at its peak.


