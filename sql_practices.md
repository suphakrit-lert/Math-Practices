Ex. Summarize Rows into Columns 1
Tips: Summarize rows with sum(case when col = ‘val1’ then 1 else 0 end) as val1_count to create a new column
Assume you're given the table on user viewership categorized by device type where the three types are laptop, tablet, and phone. 

Write a query that calculates the total viewership for laptops and mobile devices where mobile is defined as the sum of tablet and phone viewership. Output the total viewership for laptops as laptop_reviews and the total viewership for mobile devices as mobile_views.
 
There are a total of 2 laptop views and 3 mobile views.
select 
  sum(case when device_type = 'laptop' then 1 else 0 end) as laptop_views,
  sum(case when device_type in ('tablet', 'phone') then 1 else 0 end) as mobile_views
from viewership

Ex. Summarize Rows into Columns 2
Tips: Summarize rows with sum(case when col = ‘val1’ then 1 else 0 end) as val1_count to create a new column
Write a query to calculate the click-through rate (CTR) for the app in 2022 and round the results to 2 decimal places.
Definition and note: Percentage of click through rate (CTR) = 100.0 * Number of clicks / Number of impressions
 
Consider an example of App 123. This app has a click-through rate (CTR) of 50.00% because out of the 2 impressions it received, it got 1 click.
with event_count as (
  select 
    app_id
    , sum(case when event_type = 'click' then 1 else 0 end) as click_count
    , sum(case when event_type = 'impression' then 1 else 0 end) as impression_count
  from events
  where date_part('year', timestamp) = 2022
  group by app_id
)

select 
  app_id
  , round((click_count * 100.0 / impression_count), 2)  as ctr
from event_count

Ex. Summarize Rows into Percentage
Tips: Summarize rows with sum(case when col = ‘val1’ then 1 else 0 end) as val1_count to create a new column
Write a query to obtain a breakdown of the time spent sending vs. opening snaps as a percentage of total time spent on these activities grouped by age group. Round the percentage to 2 decimal places in the output.
 
 
with frequency as (
  select 
    age_breakdown.age_bucket
    , sum(case when activity_type = 'send' then time_spent else 0 end) as send_time
    , sum(case when activity_type = 'open' then time_spent else 0 end) as open_time
  from activities
  inner join age_breakdown
  on activities.user_id = age_breakdown.user_id
  group by age_breakdown.age_bucket
)

select
  age_bucket
  , round(send_time * 100.00 / (send_time + open_time), 2) as send_perc
  , round(open_time * 100.00 / (send_time + open_time), 2) as open_perc
from frequency
order by age_bucket asc




Ex. Find Duplicate
Tip: Find duplicate  select count(dup_col) group by 1, 2, 3 + having > 1
Write a query to retrieve the count of companies that have posted duplicate job listings. Duplicate job listings are defined as two job listings within the same company that share identical titles and descriptions. 
 
There is one company ID 345 that posted duplicate job listings. The duplicate listings, IDs 945 and 164 have identical titles and descriptions.
with duplicate_listings as (
  select distinct
    company_id
    , title
    , description
    , count(job_id) as duplicate_job_count
  from job_listings
  group by company_id, title, description
  having count(job_id) > 1
)

select count(1) as duplicate_companies
from duplicate_listings;


Ex. Histogram
Write a query to obtain a histogram of tweets posted per user in 2022. Output the tweet count per user as the bucket and the number of Twitter users who fall into that bucket. In other words, group the users by the number of tweets they posted in 2022 and count the number of users in each group.
Tip: Histogram = Double group by: 
1) 1st group by: Count the frequency of each category in CTE
2) 2nd group by: Create frequency histogram
 Based on the example output, there are two users who posted only one tweet in 2022, and one user who posted two tweets in 2022. The query groups the users by the number of tweets they posted and displays the number of users in each group.
with total_tweet as (
  select 
    user_id, 
    count(user_id) as count_post
  from tweets
  where date_part('year', tweet_date) = 2022
  group by user_id

  /*
  user_id count_post
      111          2
      148          1
      254          1
  */
)

select 
  count_post as tweet_bucket,
  count(count_post) as users_num
from total_tweet
group by count_post


Ex. Want to find candidates who are proficient in Python, Tableau, and PostgreSQL. Write a query to list the candidates who possess all of the required skills for the job. Sort the output by candidate ID in ascending order.
 
Candidate 123 is displayed because they have Python, Tableau, and PostgreSQL skills. 345 isn't included in the output because they're missing one of the required skills: PostgreSQL.

select candidate_id
from candidates
where skill in ('Python', 'Tableau', 'PostgreSQL')
group by candidate_id
having count(candidate_id) = 3
order by candidate_id asc

Ex. The objective is to generate data to populate a histogram that shows the number of unique queries run by employees during the third quarter of 2023 (July to September). Additionally, it should count the number of employees who did not run any queries during this period. Display the number of unique queries as histogram categories, along with the count of employees who executed that number of unique queries.
 
 
 
with employee_queries as (
  select 
    employees.employee_id
    , count(queries.query_id) as unique_queries
    
  from employees
  left join queries
  on employees.employee_id = queries.employee_id
    and queries.query_starttime >= '2023-07-01T00:00:00Z'
    and queries.query_starttime < '2023-10-01T00:00:00Z'
  group by employees.employee_id
)

select unique_queries, count(employee_id) as employee_count
from employee_queries
group by unique_queries
order by unique_queries asc


Ex. Rolling Average
Tips: Rolling Avg = avg(col) over (partition by id order by date rows between 1 preceding and 1 following)
Given a table of tweet data over a specified time period, calculate the 3-day rolling average of tweets for each user. Output the user ID, tweet date, and rolling averages rounded to 2 decimal places.
 

select 
  user_id
  , tweet_date
  , round(avg(tweet_count) over (
    partition by user_id
    order by tweet_date
    rows 2 preceding
  ), 2) as rolling_avg_3d
from tweets



Ex. Date Difference
Tip: Date difference between two rows = group by id & max(date) – min(date)
For each user who posted at least twice in 2021, write a query to find the number of days between each user’s first post of the year and last post of the year in the year 2021. Output the user and number of the days between each user's first and last post.

 
select 
  user_id,
  abs(max(post_date::date) - min(post_date::date)) as days_between
from posts
where date_part('year', post_date::date) = 2021
group by user_id
having abs(max(post_date::date) - min(post_date::date)) > 0
order by user_id asc


Ex. Write a query to obtain the third transaction of every user. 
Tip: Transaction Order = rank over (partition by id order by date asc) as ranking
 
with ranked_transaction as (
  select 
    user_id
    , spend
    , transaction_date
    , rank() over (
      partition by user_id
      order by transaction_date asc
    ) as transaction_order
  from transactions
)

select
  user_id
  , spend
  , transaction_date
from ranked_transaction
where transaction_order = 3
