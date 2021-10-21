---
date: "2021-10-22"
description: Using data from [NASA’s Goddard Institute for Space Studies](https://data.giss.nasa.gov/gistemp/) we analyzed weather data from 1880-2020 in order to better understand how average and extreme temperatures have changed over the past century. 
fact: Interesting little tidbit shown below image on summary and detail page
featured: true
image: /img/weather_gen.png
link: /r_htmls/Homework2_groupB9_final-1.html
pubtype: R Project
sitemap:
  priority: 0.8
tags:
- R
- R Studio
- AirBnb
- Regression
- Australia
- Sydney
title: 'Climate change and temperature anomalies'
weight: 400
---

Using Combined Land-Surface Air and Sea-Surface Water Temperature Anomalies in the Northern Hemisphere data from [NASA’s Goddard Institute for Space Studies](https://data.giss.nasa.gov/gistemp/) we analyzed weather data from 1880-2020 in order to better understand how average and extreme temperatures have changed over the past century. 

**Time-series scatterplot**

We first created a time-series scatterplot (see image on the right) to see how temperature anomalies has been has been steadily increasing from the 1950-1980s base period, particularly after the 1970s. The overall data shows that the temperature anomalies represent higher temperature after the 1950s and lower before 1950s. This prompted us to investigate further

**Monthly view**

By grouping the ‘tidyweather’ data by month and creating a scatter plot with trend lines, we see that all months show increasing temperature deviations. An interesting observation is that the temperature deviations are closer to each other for certain months and show a higher year on year variability for other months. December to February shows a high variability from year to year whereas the year on year variations for May to September show less variability. In more recent years, we also see that the months December to February show the highest anomalies.

![](/img/weather_mon.png)

**Density plot**

The density plot shows us that the temperature deviations have been higher in more recent years, indicated by the ‘1981-2010’ and ‘2011-present’ distributions having higher median’s and the majority of observations being higher than the other intervals. The density plot also shows us that the temperature deviations are more spread out in the more recent distributions, indicating higher temperature variability compared to the base and older years.

![](/img/weather_den.png)

**Trendline and average annual annomaly**

The scatter plot of average annual temperature anomalies reaffirms our observations about an increase in temperature in more recent time compared to the base between ‘1951-1980’. Using both 'formula_ci' and bootstrapping we created a confidence interval. Both methods give us the lower 5th percentile mark at 1.01 degrees and the higher 95th percentile at 1.11, with a mean temperature anomaly of 1.06. 

![](/img/weather_ann.png)
