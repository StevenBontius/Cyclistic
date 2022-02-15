# Prepare

The data has been made available by Lyft Bikes and Scooters, LLc which operates the City of Chicago's Divvy bicycle sharing service. Some of the data, that is owned by the City of Chicago, has been made publicly available. The data is considered to be first party data and free from any privacy data. The licence for the data can be found here <https://ride.divvybikes.com/data-license-agreement>

Only the data from 2020 is used during this analysis. Data can be found here <https://divvy-tripdata.s3.amazonaws.com/index.html> and the data of each month is contained in a separate file.

The data has been combined into one file without altering its contents using rbind() in R.

![skim_raw](pictures/skim_r_raw.jpg)