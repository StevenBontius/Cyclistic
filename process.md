# Process

## Ride duration

The first task is to calculate the ride duration in minutes. This can be done by subtracting the started_at form the ended_at times. These times are currently stored as a character data type and need to be converted to a datetime data type (POSIXct). After calculating the ride duration the value is stored as a difftime data type. It needs to be cast to number in order to work with it in the future.


```{r convert_date_time}
bike_rides_2021 <- bike_rides_2021 %>% 
  mutate(started_at = as_datetime(started_at), ended_at = as_datetime(ended_at),
         ride_duration_min = as.numeric(difftime(ended_at, started_at, units = "mins")))
```

![ride_duration_skim_r](pictures/skim_r_duration.jpg)

It is noticeable that there are rides with a negative ride duration (146 observations) and rides that took exactly 0 minutes to complete (377 observations). 

```{r negative_zero_duration}
negative_duration <- bike_rides_2021 %>% 
  filter(ride_duration_min < 0)

zero_duration <- bike_rides_2021 %>% 
  filter(ride_duration_min == 0)
```

These trips have been identified to have a incorrect duration and in total 523 have an incorrect trip duration and since this is a small amount they will be removed from the data set.

```{r removing_negative_zero_duration}
bike_rides_2021 <- anti_join(bike_rides_2021, negative_duration)
bike_rides_2021 <- anti_join(bike_rides_2021, zero_duration)
```

## Date and time

### Al rides started in 2021?
The first check is to see if all bike trips have started in 2021, and this is the case.
```{r in_2021}
unique(year(bike_rides_2021$started_at))
```
![2021](pictures/2021.jpg)



## Data transformations
* Converted started_at en ended_at to date time with as_datetime()
* Calculated the ride duration ride_duration_min with difftime() 
* Converted ride_duration_min to numeric data type

## Data cleaning remarks
* Removed the bike rides with a with negative and zero time duration (removed 523 obs)