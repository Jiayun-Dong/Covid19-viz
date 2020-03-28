Data Sources
------------

In this project, we use the data from [The COVID Tracking
Project](https://covidtracking.com) and [Johns Hopkins
dataset](https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data/csse_covid_19_time_series).
We also use US states population data (uploaded in Github) in order to
understand the spread and testing of the virus from the per capita
perspective.

``` r
dat = as.data.frame(fromJSON("https://covidtracking.com/api/states/daily")) %>%  
  select(state, date, positive, negative, pending, death, total) %>%
  mutate(date = as.Date(as.character(date), format = "%Y%m%d"),
         death = if_else(is.na(death), 0, as.double(death)),
         pending = if_else(is.na(pending), 0, as.double(pending)),
         negative = if_else(is.na(negative), 0, as.double(negative))) %>%
  arrange(state, date)
dat_pop = read.csv(file="StatePopulations.csv", head = TRUE, sep =",") %>% 
  mutate(state_abbrev = as.character(state_abbrev)) %>%
  select(state = state_abbrev, population = X2018.Population)
```

Overview of The Spread of Covid-19 in the US
--------------------------------------------

``` r
overview = dat %>%
    group_by(date) %>%
    summarise_if(is.numeric, sum, na.rm=TRUE) %>% # aggregate numeriac variables at national level
    mutate(totalTestResults = total - pending,  # excluding tests with pending results
           positiveDailyIncrease = positive - lag(positive),
           testResultsDailyIncrease = totalTestResults - lag(totalTestResults),
           positiveDailyIncrease = replace_na(positiveDailyIncrease, 0), # the first day has no lag: set as zero
           testResultsDailyIncrease = replace_na(testResultsDailyIncrease, 0))
```

``` r
  # time series of positive cases 
  ggplot(data = overview, aes(x = date)) +
    geom_line(aes(y = positive, color = "Positive Cases")) +
    geom_bar(stat = "identity", aes(y = positiveDailyIncrease, fill = "Daily Increase in Positive Cases")) +
    scale_x_date(date_minor_breaks = "1 day") +
    scale_y_continuous(labels = scales::comma) +
    scale_color_manual(values = "darkred") +
    scale_fill_manual(values = "darkblue") +
    theme_minimal() +
    theme(legend.position = "bottom", legend.title = element_blank(), 
          axis.title.x = element_blank(), axis.title.y = element_blank()) +
    ggtitle("Overview of Covid-19 in the US: Positive Cases")
```

![](Visualizing-Covid-19-Data_files/figure-markdown_github/unnamed-chunk-3-1.png)

``` r
  # time series of testing
  ggplot(data = overview, aes(x = date)) +
    geom_line(aes(y = totalTestResults, color = "Total Test Results")) +
    geom_bar(stat = "identity", aes(y = testResultsDailyIncrease, fill = "Daily Increase in Test Results")) +
    scale_x_date(date_minor_breaks = "1 day") +
    scale_y_continuous(labels = scales::comma) +
    scale_color_manual(values = "darkred") +
    scale_fill_manual(values = "darkblue") +
    theme_minimal() +
    theme(legend.position = "bottom", legend.title = element_blank(), 
          axis.title.x = element_blank(), axis.title.y = element_blank()) +
    ggtitle("Overview of Covid-19 in the US: Tests")
```

![](Visualizing-Covid-19-Data_files/figure-markdown_github/unnamed-chunk-4-1.png)