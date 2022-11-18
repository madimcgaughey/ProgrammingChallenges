# SQL Challenge

The database contains two tables, store_revenue and marketing_data.  Refer to the two CSV
files, store_revenue and marketing_data to understand how these tables have been created.

store_revenue contains revenue by date, brand ID, and location:

 >  create table store_revenue (
 >     id int not null primary key auto_increment,
 >    date datetime,
 >    brand_id int,
 >    store_location varchar(250),
 >    revenue float  
 >  );

marketing_data contains ad impression and click data by date and location:

> create table marketing_data (
>  id int not null primary key auto_increment,
>  date datetime,
>  geo varchar(2),
>  impressions float,
>  clicks float
> );

### Please provide a SQL statement under each question.

* Question #0 (Already done for you as an example)
 Select the first 2 rows from the marketing data
​
>  select *
>  from marketing_data
> limit 2;
​
*  Question #1
 Generate a query to get the sum of the clicks of the marketing data

 > SELECT SUM(clicks) AS total_clicks
 > FROM marketing_data;
​
*  Question #2
 Generate a query to gather the sum of revenue by store_location from the store_revenue table

 > SELECT SUM(revenue) AS revenue_sum
 > FROM store_revenue
 > GROUP BY store_location;
​
*  Question #3
 Merge these two datasets so we can see impressions, clicks, and revenue together by date
and geo.
 Please ensure all records from each table are accounted for.

 > SELECT marketing_data.impressions, marketing_data.clicks, store_revenue.revenue
 > FROM marketing_data
 > FULL OUTER JOIN store_revenue ON marketing_data.date=store_revenue.date AND marketing_data.geo=store_revenue.store_location
 > GROUP BY marketing_data.geo 
 > ORDER BY marketing_data.date;

* Question #4
 In your opinion, what is the most efficient store and why?

In my opinion, the most efficient store is the Minnesota store (MN). I came to this conclusion by calculating and analyzing the click-through-rate (CTR) of the four different stores. I found that the MN store had a CTR of 4.5% compared to the other three stores whose CTR's ranged from around 1.2% to 1.4%. This means that more people who were exposed to the MN store's ads found those ads to be relevant and clicked on them. A higher CTR indicates a better chance at increasing conversions which will subsequently increase revenue. It also results in less wasted ad spend making it the most efficient.

* Question #5 (Challenge)
 Generate a query to rank in order the top 10 revenue producing states
​
> SELECT store_location
> SUM(revenue)
> FROM store_revenue
> ORDER BY revenue DESC
> limit 10;