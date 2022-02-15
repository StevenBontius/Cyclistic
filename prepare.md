# Prepare

The data has been made available by Lyft Bikes and Scooters, LLc which operates the City of Chicago's Divvy bicycle sharing service. Some of the data, that is owned by the City of Chicago, has been made publicly available. The data is considered to be first party data and free from any privacy data. The licence for the data can be found here <https://ride.divvybikes.com/data-license-agreement>

Only the data from 2020 is used during this analysis. Data can be found here <https://divvy-tripdata.s3.amazonaws.com/index.html> and the data of each month is contained in a separate file.

The data has been combined into one file without altering its contents using rbind() in R.

![skim_raw](pictures/skim_r_raw.jpg)

The data set contains 5,559,063 observations containing 14 columns, which are all unique given their ride ID being unique for the whole data set.

Details of column names

|Column name   |Data type     |   Description                                             | 
|:-------------|:-------------|:----------------------------------------------------------| 
| ride_id      | chr          |unique string of characters and numbers used as primary key|
| rideable_type| chr          |type of ride(bikes in this case) that is used              |

| started_at [chr] = date time when the ride started
| ended_at [chr] = date time when the ride ended
| start_station_name [chr] = name of the station where the bike ride started
| start_station_id [chr] = identification code of the station where the bike ride started
| end_station_name [chr] = name of the station where the bike ride ended
| end_station_id [chr] = identification code of the the station where the bike ride ended
| start_lat [num] = latitude position of where the bike ride started
| start_long [num] = longitude position of where the bike rider started
| end_lat [num] = latitude position of where the bike ride ended
| end_long [num] = longitude positon of where the bike ride ended
| member_casual [chr] = indication of the ride was done by a annual member or a casual rider