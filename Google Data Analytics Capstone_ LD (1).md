# Google Data Analytics Capstone: Complete a Case Study
### Case Study 1: How does a bike-share navigate speedy success?

## Introduction


### About the company:
Cyclistic: A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. 

### Scenario:
I am a junior data analyst working in the marketing analyst team at Cyclistic. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, my team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, my team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so we must be backed up with compelling data insights and professional data visualizations.

### Business Task
Explore how annual members and casual riders utilize Cyclistic bikes to uncover valuable insights into their distinct preferences and patterns of usage and make data-driven strategic marketing decisions for Cyclistic.

### Data Structure
Each .csv file contains a table with 13 columns with varying data types as shown below. Each column stands for a field that describes how people use Cyclistic's bike-sharing service. Each row represents an observation with the details of every ride.

- ride_id = col_character(),
- rideable_type = col_character(),
- started_at = col_datetime(format = ""),
- ended_at = col_datetime(format = ""),
- start_station_name = col_character(),
- start_station_id = col_character(),
- end_station_name = col_character(),
- end_station_id = col_character(),
- start_lat = col_double(),
- start_lng = col_double(),
- end_lat = col_double(),
- end_lng = col_double(),
- member_casual = col_character()

## Process:
>In this phase, we will clean and transform data while maintaining the data’s integrity. Documenting the data-cleaning process is essential to keep track of the changes made to the dataset.

Here are the steps that I followed during this phase:
1.  Combined all the tables into one data table
2.	Check for null and duplicates
3.	Cleaned the data
4.	Additional columns and data transformation
5.	Extract data for analysis


#### Data Combination : 

Tables represting 12 .csv files have been uploaded to the tripdata_2023 dataset. The following SQL query is implemented to combine data from all the tables into a single table called 'all_tripdata'.
```
CREATE TABLE IF NOT EXISTS 
  `tripdata_2023.all_tripdata` AS
  (
    SELECT * FROM `tripdata_2023.tripdata_2023_01`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_02`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_03`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_04`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_05`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_06`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_07`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_08`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_09`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_10`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_11`
    UNION ALL
    SELECT * FROM `tripdata_2023.tripdata_2023_12`
  )
```
To check the number of null values in each column, the following SQL query is run.
```
SELECT
  COUNT(*) - COUNT(ride_id) AS missing_ride_id,
  COUNT(*) - COUNT(rideable_type) AS missing_rideable_type,
  COUNT(*) - COUNT(started_at) AS missing_started_at,
  COUNT(*) - COUNT(ended_at) AS missing_ended_at,
  COUNT(*) - COUNT(start_station_name) AS missing_start_station_name,
  COUNT(*) - COUNT(end_station_name) AS missing_end_station_name,
  COUNT(*) - COUNT(start_station_id) AS missing_start_station_id,
  COUNT(*) - COUNT(end_station_id) AS missing_end_station_id,
  COUNT(*) - COUNT(start_lat) AS missing_start_lat,
  COUNT(*) - COUNT(end_lat) AS missing_end_lat,
  COUNT(*) - COUNT(start_lng) AS missing_start_lng,
  COUNT(*) - COUNT(end_lng) AS missing_end_lng,
  COUNT(*) - COUNT(member_casual) AS missing_member_casual
FROM
  `tripdata_2023.all_tripdata`
```
From this, we saw that there are null values in start_station_name, end_station_name, end_station_id, start_station_id, end_lat and end_lng.

So to clean the data, we run the following SQL query and create a new 'cleaned_tripdata' table.
```
CREATE TABLE IF NOT EXISTS
`tripdata_2023.cleaned_tripdata` AS
  (SELECT *
  FROM `tripdata_2023.all_tripdata`
  WHERE start_station_name IS NOT NULL
  AND end_station_name IS NOT NULL
  AND end_station_id IS NOT NULL
  AND start_station_id IS NOT NULL
  AND end_lat IS NOT NULL
  AND end_lng IS NOT NULL)
```
We need to check how many rides are for more than 1 day ~ 24 hours. 
```
SELECT
  COUNT(*) AS trips_more_than_24_hours
FROM
  `tripdata_2023.cleaned_tripdata`
WHERE
  TIMESTAMP_DIFF(ended_at, started_at, HOUR) >= 24
```
Total 133 trips are equal or more than 24 hours.

We also need to check how many rides are less than 1 minute ~ 60 seconds.
```
SELECT
  COUNT(*) AS trips_less_than_1_minute
FROM
  `tripdata_2023.cleaned_tripdata`
WHERE
  TIMESTAMP_DIFF(ended_at, started_at, SECOND) <= 60
```
Total 88381 trips are less than 1 minutes.

To analyze the data with more proper data insights, we need to delete these data rows.
```
CREATE TABLE IF NOT EXISTS
`tripdata_2023.final_tripdata` AS
(SELECT *
FROM `tripdata_2023.cleaned_tripdata`
WHERE TIMESTAMP_DIFF(ended_at, started_at, HOUR) < 24
AND TIMESTAMP_DIFF(ended_at, started_at, SECOND) > 60)
```

## DATA ANALYSIS

- Number of trips per rider type
```
SELECT
  member_casual,
  COUNT(*) AS num_of_trips
FROM
  `tripdata_2023.final_tripdata`
GROUP BY
  member_casual
ORDER BY
  member_casual
```
- Number of trips per bike type per rider type
```
SELECT
  member_casual,
  rideable_type,
  COUNT(*) AS num_of_trips
FROM
  `tripdata_2023.final_tripdata`
GROUP BY
  rideable_type,
  member_casual
ORDER BY
  member_casual, num_of_trips
```
- Average ride length per rider type
```
SELECT
  member_casual,
  AVG(TIMESTAMP_DIFF(ended_at, started_at, MINUTE)) AS avg_ride_time
FROM
  `tripdata_2023.final_tripdata`
GROUP BY
  member_casual
```
- Average ride length per month per rider type
```
WITH cleaned AS
(SELECT
  *,
  EXTRACT(MONTH FROM started_at) AS month
  FROM `tripdata_2023.cleaned_tripdata`)

SELECT
  member_casual,
  month,
  AVG(TIMESTAMP_DIFF(ended_at, started_at, MINUTE)) AS avg_ride_time
FROM
  cleaned
GROUP BY
  member_casual,
  month
ORDER BY
  member_casual,
  month
```
- Average ride length per hour per rider type
```
WITH cleaned AS
(SELECT
  *,
  EXTRACT(HOUR FROM started_at) AS hour
  FROM `tripdata_2023.cleaned_tripdata`)

SELECT
  member_casual,
  hour,
  AVG(TIMESTAMP_DIFF(ended_at, started_at, MINUTE)) AS avg_ride_time
FROM
  cleaned
GROUP BY
  member_casual,
  hour
ORDER BY
  member_casual,
  hour
```
- No. of trips per month per rider type
```
WITH cleaned AS
(SELECT
  *,
  EXTRACT(MONTH FROM started_at) AS month
  FROM `tripdata_2023.cleaned_tripdata`)

SELECT
  member_casual,
  month,
  COUNT(*) AS num_of_trips
FROM
  cleaned
GROUP BY
  member_casual,
  month
ORDER BY
  member_casual,
  month
```
- No. of trips per day per rider type
```
WITH cleaned AS
(SELECT
  *,
  EXTRACT(DAYOFWEEK FROM started_at) AS day
  FROM `tripdata_2023.cleaned_tripdata`)

SELECT
  member_casual,
  day,
  COUNT(*) AS num_of_trips
FROM
  cleaned
GROUP BY
  member_casual,
  day
ORDER BY
  member_casual,
  day
```
- No. of trips per hour per rider type
```
WITH cleaned AS
(SELECT
  *,
  EXTRACT(HOUR FROM started_at) AS hour
  FROM `tripdata_2023.cleaned_tripdata`)

SELECT
  member_casual,
  hour,
  COUNT(*) AS num_of_trips
FROM
  cleaned
GROUP BY
  member_casual,
  hour
ORDER BY
  member_casual,
  hour
```
- Most popular start station per rider type
```
SELECT
  member_casual,
  start_station_name,
  AVG(start_lat) AS avg_start_lat,
  AVG(start_lng) AS avg_start_lng,
  COUNT(*) AS num_of_trips
FROM
  `tripdata_2023.cleaned_tripdata`
GROUP BY
  member_casual,
  start_station_name
ORDER BY
  member_casual,
  num_of_trips DESC
```
- Most popular end station per rider type
```
SELECT
  member_casual,
  end_station_name,
  AVG(end_lat) AS avg_end_lat,
  AVG(end_lng) AS avg_end_lng,
  COUNT(*) AS num_of_trips
FROM
  `tripdata_2023.cleaned_tripdata`
GROUP BY
  member_casual,
  end_station_name
ORDER BY
  member_casual,
  num_of_trips DESC
```
