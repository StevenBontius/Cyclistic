# Analyze

Just as a reminder, the business task is the following:

How do annual members and casual riders use Cyclistics bikes differently?

## Basic information

Fist some basic analysis will be done, starting with the split in number of rides per member and casual rider as well as the number of minutes on the bike.

### Number of rides
```{r pie_number_of_rides}
df <- bike_rides_2021 %>% 
  group_by(member_casual) %>% 
  tally(name = "number_of_rides") %>% 
  mutate(percentage = round(number_of_rides / sum(number_of_rides), digits = 2)) %>% 
  arrange(-percentage) %>% 
  mutate(labels = scales::percent(percentage))

ggplot(df, aes(x = "", y = percentage, fill = member_casual)) +
  geom_col(color = "white") +
  geom_text(aes(label = labels),
            position = position_stack(vjust = 0.5)) +
  coord_polar(theta = "y") +
  theme_void() + 
  labs(title = "Rides [5,585,206] per customer type") +
  guides(fill = guide_legend(title = "Member type"))
```
![pie_number_rides](pictures/rides_customer_type.png)

### Number of minutes on bike

```{r}
df <- bike_rides_2021 %>% 
  group_by(member_casual) %>% 
  summarise(minutes_on_bike = sum(ride_duration_min)) %>% 
  mutate(percentage = minutes_on_bike / sum(minutes_on_bike)) %>%
  arrange(percentage) %>% 
  mutate(labels = scales::percent(percentage))

ggplot(df, aes(x = "", y = percentage, fill = member_casual)) +
  geom_col(color = "white") +
  geom_text(aes(label = labels),
            position = position_stack(vjust = 0.5)) +
  coord_polar(theta = "y") +
  theme_void() + 
  labs(title = "Minutes [116.5 million] per customer type") +
  guides(fill = guide_legend(title = "Member type"))
```
![pie_minutes](pictures/minutes_customer_type.png)

#### Conclusions
* Members make more rides than casual riders
* Casual riders spend more minutes on the bike then members

## Starting the bike ride

When do the different customer types start their bike ride? On which day and hour? This section will dive into the when the ride was started.

### Day of the bike ride

Plotting the starting day in a bar graph, week days need to be in a vector to make sure that the bar graoh shows the week days in the correct order.

```{r number_rides_week_day}
week_days <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")

bike_rides_2021 %>%
  ggplot() +
  geom_bar(mapping = aes(x = factor(week_day_started, level = week_days))) +
  facet_wrap(~member_casual) +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  labs(title = "Number of bike rides", x = "Weekday", y = "Number of rides")
```
![rides_week_day](pictures/rides_week_days.png)

### Conclusions



## Conclusions
* Members make more rides than casual riders
* Cusual riders spend more minutes on the bike then members