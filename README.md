# Covid19-viz

This is a demo of my recent data analysis work about Covid-19 data.
  
* `Visualizing-Covid-19-Data.md` is the latest full-version of the analysis.
* `Visualizing-Covid-19-Data.Rmd` contains the `code`.
* The pdf files with dates are earlier versions.

Below is a summary of the key take-away. Please let me know your comments and suggestions.

1. *There are different trajectories of the spread of the Coronavirus in different countries and regions. The spread has been controled or limited to a controlable rate in some of the Asian places. The disease is spreading at a concerning rate in the US and European countries. However, the growth in the number of cases has slowed down recently.*

![Overview](https://github.com/Jiayun-Dong/Covid19-viz/blob/master/Visualizing-Covid-19-Data_files/figure-gfm/unnamed-chunk-7-1.png)

2. *The recent slowdown of the growth in the number of cases is partially associated with inadequate testing. The constant positive rate of tests and increasing death rate in the recent days support this statement.*

The growth of cases shifts from the exponential rate in late March to the linear rate in April. In particular, the daily increments in cases are roughly constant in April.

![PosRate](https://github.com/Jiayun-Dong/Covid19-viz/blob/master/Visualizing-Covid-19-Data_files/figure-gfm/unnamed-chunk-8-1.png)

The daily numbers of tests performed and the positive rate of the tests are both constant in April, which is directly associated with the observed linear growth in April. Death rate has increased from 3% to 5% in April. Assume the virus has not become more deadly and the healthcare quality does not decrease, there must be people infected yet not confirmed, which is another signal of inadequate testing. (Please refer to the full analysis for figures and details.)

```
Metrics definition:
  positive rate = positive test results / (positive test results + negative test results)
  death rate = number of deaths / number of positive cases
```

3. *Direct cross-state comparison of the number of cases does not tell which state has more severe spread of Covid-19. After all, no one is confirmed as infected if no test is performed. I argue that comparisons are still possible by jointly analyzing positive rate and number of tests per million population.*

```
Metrics definition:
  tests per million population = number of tests / total population * 1,000,000
```

Presumably, tests are done for people with symptoms and prioritize those with severe symptoms who are more likely to be infected. If two states have the same number of tests per million population, they have "sampled" the same proportion of their "high risk population" (in terms of the likelihood to be infected.) If a state has higher positive rate, its "high risk population" is "riskier", which is a signal for a potential higher infection rate.

The figure visualizes such comparisons. For example, NJ and WA have similar numbers of tests per million population, while the positive rate is much higher for NJ. This could suggest more people in NJ are infected. The top 10 states in terms of the number of cases (red) tend to have higher positive rate than other states with similar number of tests per million population.

![CrossComparison](https://github.com/Jiayun-Dong/Covid19-viz/blob/master/Visualizing-Covid-19-Data_files/figure-gfm/unnamed-chunk-18-1.png)

4. *A projection of the death trajectory of Covid-19 is done based on a simplified version of [IHME's](https://covid19.healthdata.org/united-states-of-america) method. Similar results are reproduced.*

Two examples are given below.

![NY](https://github.com/Jiayun-Dong/Covid19-viz/blob/master/Visualizing-Covid-19-Data_files/figure-gfm/unnamed-chunk-24-1.png)
![NJ](https://github.com/Jiayun-Dong/Covid19-viz/blob/master/Visualizing-Covid-19-Data_files/figure-gfm/unnamed-chunk-25-1.png)

Please refer to the full-version for more analysis and figures.
