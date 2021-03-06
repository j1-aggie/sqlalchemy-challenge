# SQLAlchemy Homework - Surfs Up!

For this homework, we are going to Honolulu, Hawaii! To help with the trip planning, we had to do some climate analysis on the area. The following outlines what I did.

## Step 1 - Climate Analysis and Exploration

To begin, I used Python and SQLAlchemy to do basic climate analysis and data exploration of the provided climate database. All of the following analysis were completed using SQLAlchemy ORM queries, Pandas, and Matplotlib.

* Ibcreated a panda notebook (climate_starter.ipynb) and used the provided [hawaii.sqlite](Resources/hawaii.sqlite) files to complete climate analysis and data exploration.

* I picked a start date and end date for the trip. The trip was within the suggested window of 3-15 days total.

* Used SQLAlchemy `create_engine` to connect to sqlite database.

* Used SQLAlchemy `automap_base()` to reflect tables into classes and saved a reference to those classes called `Station` and `Measurement`.

### Precipitation Analysis

* Designed a query to retrieve the last 12 months of precipitation data.

* Selected only the `date` and `prcp` values.

* Loaded the query results into a Pandas DataFrame and set the index to the date column.

* Sorted the DataFrame values by `date`.

* Ploted the results using the DataFrame `plot` method.

* Used Pandas to print the summary statistics for the precipitation data.

 ![CLIMATE](https://user-images.githubusercontent.com/66078772/95894182-56cfc800-0d4e-11eb-9cd0-5d3d116dec3f.png)



### Station Analysis

* Designed a query to calculate the total number of stations.

* Designed a query to find the most active stations.

  * Listed the stations and observation counts in descending order.

  * Annonated which station has the highest number of observations?

  * Used the hint: You will need to use a function such as `func.min`, `func.max`, `func.avg`, and `func.count` in your queries.

* Designed a query to retrieve the last 12 months of temperature observation data (TOBS).

  * Filtered by the station with the highest number of observations.

  * Ploted the results as a histogram with `bins=12`.
  
  ![frequency](https://user-images.githubusercontent.com/66078772/95898956-6dc5e880-0d55-11eb-8828-a9e7dffb0d7e.png)


 - - -

## Step 2 - Climate App

Once I completed the initial analysis, I designed a Flask API based on the queries that I developed.

* Used Flask and created my routes.

### Routes

* `/`

  * Home page.

  * List all routes that are available.

* `/api/v1.0/precipitation`

  * Convert the query results to a dictionary using `date` as the key and `prcp` as the value.

  * Return the JSON representation of your dictionary.

* `/api/v1.0/stations`

  * Return a JSON list of stations from the dataset.

* `/api/v1.0/tobs`
  * Query the dates and temperature observations of the most active station for the last year of data.
  
  * Return a JSON list of temperature observations (TOBS) for the previous year.

* `/api/v1.0/<start>` and `/api/v1.0/<start>/<end>`

  * Return a JSON list of the minimum temperature, the average temperature, and the max temperature for a given start or start-end range.

  * When given the start only, calculate `TMIN`, `TAVG`, and `TMAX` for all dates greater than and equal to the start date.

  * When given the start and the end date, calculate the `TMIN`, `TAVG`, and `TMAX` for dates between the start and end date inclusive.

## Hints

* You will need to join the station and measurement tables for some of the queries.

* Use Flask `jsonify` to convert your API data into a valid JSON response object.

- - -

## Bonus: Other Recommended Analyses



### Temperature Analysis I

* Hawaii is reputed to enjoy mild weather all year. Is there a meaningful difference between the temperature in, for example, June and December?

* Used SQLAlchemy to perform this portion.

* Identified the average temperature in June at all stations across all available years in the dataset. Did the same for December temperature.

* Used the t-test to determine whether the difference in the means, if any, is statistically significant. Will you use a paired t-test, or an unpaired t-test? Why?

Ttest_indResult(statistic=31.355036920962423, pvalue=4.193529835915755e-187).
It is a statistically significant difference in means (p-value of less than 0.05).
Very small value - means of these two populations are significantly different.
Lower probability that the difference is random.
Reject the null hypothesis.
Null hypothesis - there is no meaningful difference between the temperature in June and December in Hawaii.

![June vs December Scatter Plot](https://user-images.githubusercontent.com/66078772/95900342-5be54500-0d57-11eb-8485-9541874bda01.png)

![june_dec_histogram](https://user-images.githubusercontent.com/66078772/95900523-a5ce2b00-0d57-11eb-8dc8-2b93173095e0.png)


### Temperature Analysis II

* Used the function called `calc_temps` that will accept a start date and end date in the format `%Y-%m-%d`. The function returned the minimum, average, and maximum temperatures for that range of dates.

* Used the `calc_temps` function to calculate the min, avg, and max temperatures for my trip using the matching dates from the previous year.

* Plotted the min, avg, and max temperature from your previous query as a bar chart.

  * Used the average temperature as the bar height.

  * Used the peak-to-peak (TMAX-TMIN) value as the y error bar (YERR).

  ![avg_temp](https://user-images.githubusercontent.com/66078772/95900794-08272b80-0d58-11eb-8e6e-27d6856e2520.png)

### Daily Rainfall Average

* Calculated the rainfall per weather station using the previous year's matching dates.

* Calculated the daily normals. Normals are the averages for the min, avg, and max temperatures.

* I was provided with a function called `daily_normals` that will calculate the daily normals for a specific date. This date string will be in the format `%m-%d`. Be sure to use all historic TOBS that match that date string.

* Created a list of dates for your trip in the format `%m-%d`. Use the `daily_normals` function to calculate the normals for each date string and append the results to a list.

* Loaded the list of daily normals into a Pandas DataFrame and set the index equal to the date.

* Used Pandas to plot an area plot (`stacked=False`) for the daily normals.


 ![daily_normals](https://user-images.githubusercontent.com/66078772/95900666-d8782380-0d57-11eb-86e3-af1507e00b73.png) 
