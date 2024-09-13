# Cyclistic Bike Share Analysis
## How do annual members and casual riders use cyclistic bikes differently

## Objective
This project aims to analyze and recognize the usage patterns of casual riders versus annual members.
The primary goal is to uncover significant differences in how these 2 groups use Cyclistic bike differently

## Data Source
Cyclistic bike share data has been used, This is a public dataset that you can use to explore how different customer types are using Cyclistic bike.
[Click here to View/Dpwnload RAW data](https://github.com/PrateekSharma8368/cyclistic-bike-sharing-analysis/tree/main/RAW%20data)

## Tools Used
* *SQL(BigQuery):* For data cleaning and processing.
* *GoogleSheets:* For lightweight analysis.
* *Tableau Public:* For visualizing data.
* *GitHub:* For Project Sharing.

## Data Preparation
Key Steps Included -
*1) Verification of data types -* Crucial for maintaining data integrity and ensuring accurate processing.
*2) Combining data sets -* All 6 months of data is combined for comprehensive analysis.
*3) Data Quality Check -* Various quality cheks were performed to identify null values and inconsistencies.

[Click here to View complete SQL Data Preparation code](https://github.com/PrateekSharma8368/cyclistic-bike-sharing-analysis/blob/main/SQL_code_file/Preparaing_and_Processing_SQL_queries.txt)

## Data Cleaning
Key Steps Included -
*1) Creation-* A new table was created by removing all null values and duplicates.
*2) Add-* Additional columns for ride length, day of week, and start hour were added.
*3) Verification-* After cleaning, I verified the data to ensure it met the required conditions and to check for any remaining anomalies.

[Click here to View complete SQL Data Cleaning Queries](https://github.com/PrateekSharma8368/cyclistic-bike-sharing-analysis/blob/main/SQL_code_file/Preparaing_and_Processing_SQL_queries.txt)

 ## Data Analysis
*1. Average Ride Length by Member Type -*
Casual riders tend to have longer average ride durations compared to annual members.
SQL Query
```
SELECT member_casual,
  AVG(ride_length_minute) as Avg_ride_length
FROM `ornate-apricot-435209-g7.tripdata.clean_tripdata`
GROUP BY member_casual;
```

*2. Ride Frequency by Member Type -*
Annual members take more frequent but shorter trips.
SQL Query
```
SELECT member_casual,
  COUNT(*) as num_rides
FROM `ornate-apricot-435209-g7.tripdata.clean_tripdata`
GROUP BY member_casual;

```

*3. Hourly Usage Patterns -*
Peak hours for casual riders differ from those of annual members, with casual riders preferring weekends and afternoons.
SQL Query
```
SELECT member_casual,
  start_hour,
  count(*) as num_rides
FROM `ornate-apricot-435209-g7.tripdata.clean_tripdata`
GROUP BY member_casual, start_hour
ORDER BY member_casual, start_hour;

```

*4. Weekly Usage Patterns -*
Annual members use the service consistently throughout the week, while casual riders show a spike in usage on weekends.
SQL Query
```
SELECT member_casual,
  day_of_week,
  count(*) as num_rides
FROM `ornate-apricot-435209-g7.tripdata.clean_tripdata`
GROUP BY member_casual, day_of_week
ORDER BY member_casual, day_of_week;
```

*5. Monthly Trends -*
There is an upward trend in bike usage during warmer months, with casual riders showing more fluctuation.
 SQL Query
```
SELECT member_casual,
  EXTRACT(MONTH FROM started_at) as month,
  EXTRACT(YEAR FROM started_at) as year,
  COUNT(*) AS num_rides
FROM `ornate-apricot-435209-g7.tripdata.clean_tripdata`
GROUP BY member_casual, month, year
ORDER BY member_casual, month, year;
```
[Click here to visit complete Data Analysis SQL Queries](https://github.com/PrateekSharma8368/cyclistic-bike-sharing-analysis/blob/main/SQL_code_file/Complete_analysis_SQL_queries.txt)

## Key Findings
* *Longer rides:* Casual riders have longer ride durations than annual members.
* *Ride frequency:* Annual members use bikes more frequently, but for shorter trips.
* *Peak times:* Casual riders prefer weekends, while annual members ride consistently throughout the week.
* *Seasonal variations:* Casual rider activity increases during warmer months.
  
## Recommendations
* *Targeted marketing:* Offer promotions or discounts to casual riders on weekends to encourage membership sign-ups.
* *Incentives for longer rides:* Provide benefits for annual members who take longer rides, promoting higher usage.
* *Seasonal offers:* Roll out marketing campaigns during warmer months to capitalize on increased casual rider activity.
