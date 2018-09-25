# Joins & CTEs in SQL

1. What are the three longest trips on rainy days?

```
WITH
	short_dates
AS (
SELECT
	substring(start_date from 1 for 10) short,
	duration,
	trip_id
FROM
	trips)

SELECT
	short_dates.short,
	short_dates.trip_id,
	short_dates.duration,
	weather.events,
	weather.date
FROM
	short_dates
JOIN
	weather
ON
	short_dates.short = weather.date
WHERE
	events LIKE 'Rain'
ORDER BY
	duration
DESC
```
2. Which station is full most often?

```
SELECT
	station_id,
	COUNT(*)
FROM
	status
WHERE
	docks_available = 0
GROUP BY 1
ORDER BY count DESC
```
3. Return a list of stations with a count of number of trips starting at that station but ordered by dock count.

```
SELECT
	trips.start_station,
	stations.dockcount,
	COUNT(*) AS trip_count
FROM
	trips
JOIN
	stations
ON
	stations.name = trips.start_station
GROUP BY 1,2
ORDER BY
	dockcount
DESC
```

4. (Challenge) What's the length of the longest trip for each day it rains anywhere?
