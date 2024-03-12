# TODO
> Edit this file to add your answeres to each TODO item. Its okay to link to external documentation as well, just remember to ensure that our reviewers has access.
> When you're ready to submit, click **Commit changes...** and save your responses to a new branch titled 'implementation' and create a pull request.

>Before you start reading, please configure your environment as described in the "Before you get started" README section of your GitHub repository.*

In this task, you will work with the [Chicago Crime Dataset](https://console.cloud.google.com/marketplace/product/city-of-chicago-public-data/chicago-crime) to figure out some insights regarding the crimes commited in Chicago.

Here are some examples of the columns you will work with:

|Variable|Description|
|----:|-----|
|primary_type |What type of crime was committed|
|location_description |Description of the location where the crime was committed|
|arrest|If the crime led to an arrest or not|

Feel free to explore the dataset and try out different queries using the BigQuery interface.
Once you have a query that answers the question, add the code snippet to the specific question as well any supportive reasoning/comment that you may have.  

## Task 1 

From what date is the oldest data point in the data set? 

> TODO: 2001-01-01 01:00:00 UTC
SELECT distinct 
date
FROM `bigquery-public-data.chicago_crime.crime` 
order by date 

LIMIT 1000;

## Task 2

Which year had the largest amount of crimes and how many crimes were committed that year?

> TODO: The year is 2002 and the number of crimes is 486815
SELECT
year,
COUNT(unique_key) as Number_of_crimes
FROM `bigquery-public-data.chicago_crime.crime` 
group by 1
order by 2 desc


## Task 3

Let's define "Arrest Rate" as the share of crimes that led to an arrest.
What were the five most common crimes in 2020? Which of those has the highest and lowest arrest rate?

> TODO: The five most common crimes were : BATTERY,THEFT,CRIMINAL DAMAGE,DECEPTIVE PRACTICE and ASSAULT.
The highest is BATTERY with a arrest rate of 16.66% and the lowest is DECEPTIVE PRACTICE with an arrest rate of 2.1%.

SELECT primary_type,
       COUNT(*) AS total_crimes,
       SUM(CASE WHEN arrest = true THEN 1 ELSE 0 END) AS total_arrests,
       SUM(CASE WHEN arrest = true THEN 1 ELSE 0 END) / COUNT(*) AS arrest_rate
FROM `bigquery-public-data.chicago_crime.crime`
WHERE year = 2020
GROUP BY primary_type
ORDER BY 2 
DESC
LIMIT 5;
 


## Task 4

What year had the highest arrest rate? Plot the number of crimes per year and comment on the trend.

> TODO: The year with the highest arrest rate is 2005 with a rate of 31.06%.
 The link to the plot :
 https://docs.google.com/spreadsheets/d/1gIJozo0uMOimKvFI8jvuqzgff7FE-B4Ni5mpLkek-O4/edit?usp=sharing
COMMENT ON THE PLOT: As the years increase, we can see the crime rate is reducing.
SQL QUERY : SELECT year,
       COUNT(*) AS total_crimes,
       SUM(CASE WHEN arrest = true THEN 1 ELSE 0 END) AS total_arrests,
       SUM(CASE WHEN arrest = true THEN 1 ELSE 0 END) / COUNT(*) AS arrest_rate
FROM `bigquery-public-data.chicago_crime.crime`

GROUP BY year
ORDER BY 4 DESC
;



## Task 5

Which year had the most number of crimes leading to an arrest? How many arrests were made during that year? Plot the trend for total number of arrests per year.

> TODO: The year that had the most number of crimes leading to an arrest is 2005 having 140925 arrests.

SQL QUERRY:SELECT year,
       COUNT(*) AS total_crimes,
       SUM(CASE WHEN arrest = true THEN 1 ELSE 0 END) AS total_arrests,
       SUM(CASE WHEN arrest = true THEN 1 ELSE 0 END) / COUNT(*) AS arrest_rate
FROM `bigquery-public-data.chicago_crime.crime`

GROUP BY year
ORDER BY 4 DESC
;
PLOT LINK:https://docs.google.com/spreadsheets/d/1A638iBcr0STpDXC-Q5uKQJAXS78MrMrXggzSLf2Z6Sc/edit?usp=sharing
COMMENT ON PLOT: Over the years, there has been a  decrease in the total number of arrests, indicating a potential shift in law enforcement strategies or societal norms regarding crime.

## Task 6

How has the arrest rate looked like over time? 
- Plot the trend of the arrest rate.
- Between which years can you see the biggest change in "Arrest Rate"?
- Can you point at specific reasons to why the Arrest Rate dropped between those years? Comment on your conclusions.

> Since the data set is constantly updating, disregard the year 2021 and later for the analysis in this question.

> TODO: 
PLOT LINK:https://docs.google.com/spreadsheets/d/1bfqgvLitZ9v_yuB8Tcqi7n7gMstBG5V2uAb_kZkZdpg/edit?usp=sharing

The years you can see a big change is from 2015 to 2016.
Between 2015 and 2016, there was a decrease in total crimes and total arrests in Chicago. However, while the total number of crimes decreased, there was a more significant decrease in total arrests , leading to an apparent drop in the arrest rate from 26.45% in 2015 to 19.65% in 2016. Some of the factors that may have caused this change are :changes in law enforcement strategies, policies and crime patterns. 
