# Zuber Chicago Taxi Trips Analysis

## Project Description

This project involves analyzing taxi trip data in Chicago for Zuber, a new ride-sharing company launching in the city. The goal is to identify patterns in passenger preferences and the impact of external factors on trip frequency. By working with a database, we will analyze competitor data and test a hypothesis about the impact of weather on trip frequency.

## Data Description

A database with information about taxi trips in Chicago:

* **`neighborhoods` table:** data on city neighborhoods
    * `name`: neighborhood name
    * `neighborhood_id`: neighborhood code
* **`cabs` table:** data on taxis
    * `cab_id`: vehicle code
    * `vehicle_id`: technical vehicle ID
    * `company_name`: vehicle owner company
* **`trips` table:** data on trips
    * `trip_id`: trip code
    * `cab_id`: vehicle code operating the trip
    * `start_ts`: trip start date and time (time rounded to the hour)
    * `end_ts`: trip end date and time (time rounded to the hour)
    * `duration_seconds`: trip duration in seconds
    * `distance_miles`: trip distance in miles
    * `pickup_location_id`: pickup neighborhood code
    * `dropoff_location_id`: dropoff neighborhood code
* **`weather_records` table:** weather data
    * `record_id`: weather record code
    * `ts`: record date and time (time rounded to the hour)
    * `temperature`: temperature when the record was taken
    * `description`: brief description of weather conditions, e.g., "light rain" or "scattered clouds"

### Table Schema

![Table Schema](image)

**Note:** There is no direct connection between the `trips` and `weather_records` tables in the database. However, you can still use `JOIN` and link them using the time the trip started (`trips.start_ts`) and the time the weather record was taken (`weather_records.ts`).

## Project Completion Instructions

### Step 1. Data Scraping

Write code to analyze weather data in Chicago for November 2017 from the website:

[https://practicum-content.s3.us-west-1.amazonaws.com/data-analyst-eng/moved_chicago_weather_2017.html](https://practicum-content.s3.us-west-1.amazonaws.com/data-analyst-eng/moved_chicago_weather_2017.html)

### Step 2. Exploratory Data Analysis (SQL)

* Find the number of taxi trips for each taxi company from November 15th to 16th, 2017. Name the resulting field `trips_amount` and display it along with the `company_name` field. Sort the results by the `trips_amount` field in descending order.
* Find the number of trips for each taxi company whose name contains the words "Yellow" or "Blue" from November 1st to 7th, 2017. Name the resulting variable `trips_amount`. Group the results by the `company_name` field.
* In November 2017, the most popular taxi companies were Flash Cab and Taxi Affiliation Services. Find the number of trips for these two companies and assign the resulting variable the name `trips_amount`. Combine the trips from all other companies into the "Other" group. Group the data by taxi company names. Name the field with taxi company names `company`. Sort the result in descending order by `trips_amount`.

### Step 3. Hypothesis Testing (SQL)

Test the hypothesis that the duration of trips from the Loop to O'Hare International Airport changes on rainy Saturdays.

* Retrieve the neighborhood IDs for O'Hare and Loop from the `neighborhoods` table.
* For each hour, retrieve weather condition records from the `weather_records` table. Using the `CASE` operator, divide all hours into two groups: "Bad" if the `description` field contains the words "rain" or "storm" and "Good" for others. Name the resulting field `weather_conditions`. The final table should include two fields: date and time (`ts`) and `weather_conditions`.
* Retrieve from the `trips` table all trips that started in the Loop (neighborhood_id: 50) and ended in O'Hare (neighborhood_id: 63) on a Saturday. Get the weather conditions for each trip. Use the method you applied in the previous task. Also, retrieve the duration of each trip. Ignore trips for which no weather condition data is available.

### Step 4. Exploratory Data Analysis (Python)

In addition to the data you retrieved in the previous tasks, you have been given a second file. You now have these two CSVs:

* `project_sql_result_01.csv`. Contains the following data:
    * `company_name`: taxi company name
    * `trips_amount`: number of trips for each taxi company on November 15th and 16th, 2017.
* `project_sql_result_04.csv`. Contains the following data:
    * `dropoff_location_name`: Chicago neighborhoods where trips ended
    * `average_trips`: average number of trips that ended in each neighborhood in November 2017.

For these two datasets, you now need to:

* Import the files.
* Study the data they contain.
* Ensure that the data types are correct.
* Identify the top 10 neighborhoods in terms of dropoffs.
* Create graphs: taxi companies and number of trips, top 10 neighborhoods by number of dropoffs.
* Draw conclusions based on each graph and explain the results.

### Step 5. Hypothesis Testing (Python)

`project_sql_result_07.csv`: the result of the last query. Contains data on trips from the Loop to O'Hare International Airport. Remember, these are the field values from the table:

* `start_ts`: pickup date and time
* `weather_conditions`: weather conditions at the time the trip started
* `duration_seconds`: trip duration in seconds

Test the hypothesis: "The average duration of trips from the Loop to O'Hare International Airport changes on rainy Saturdays."

Set the significance level (alpha) value on your own.

Explain:

* How you formulated the null and alternative hypotheses.
* What criterion you used to test the hypotheses and why.
