---
date: "2019-02-12"
description: In August 2018, Norway's highest-earning billionaire, Einar Aas, lost his entire fortune and declared bankruptcy after betting wrong in the Nordic energy market. In this project, I am performing Holt-Winters Triple Exponential Smoothing technique to come up with a forecast for elspot prices in Oslo, and show where Einar Aas's model went wrong.
fact: Interesting little tidbit shown below image on summary and detail page
featured: true
image: /img/vann.png
link: https://gist.github.com/shry97/1a77e49c9c5ad59aa15bfd0b945b3134#file-project-on-forecasting-b166-sherington-anton-amarapala
pubtype: R Project
sitemap:
  priority: 0.8
tags:
- R
- R Studio
- Elspot
- Holt-Winters Triple Exponential Smoothing
- Seasonality
- Nordic
title: 'Analysis of Elspot prices in the Nordics'
weight: 400
---

**Introduction**

Norway’s highest-earning billionaire, Einar Aas, lost his entire fortune and
declared bankruptcy after betting wrong in the Nordic energy market in August 2018. Einar Aas made
his fortune trading in the Nordic energy market and is well known for his accurate electricity spot (elspot) price forecasts. He based his trades on his
forecast that the spread between Nordic and German elspot prices would narrow. However, due
to heavy rainfall in the Nordics, which filled the hydroelectric reservoirs, the spread instead
increased, and Nasdaq had to liquidate his position due to Mr. Aas being over-leveraged. This
incident illustrate the importance of accurate forecasting, but also that regardless of how well
you forecast, uncertainty can lead to a different outcome than expected, even when you make the
best decisions possible with the information at hand.

Elspot prices in Norway are seasonal due to energy production being primarily based on
hydropower. During periods of heavy rain, usually during the late fall, the water reservoirs fill
up, and electricity prices go down as a result. Then the elspot prices gradually increase as the
reservoirs get used up during periods of little rain. We also have big difference in price based on
the season because electricity demand increases during the cold winter months due to the use of
electric heaters. For this project, I am performing Holt-Winters Triple Exponential Smoothing
technique to come up with a forecast for elspot prices in Oslo.

**Method**

I first had to find data for elspot prices in Norway. I found monthly data at Nord Pool, the largest
electricity trade market in Europe. The data was separated into spreadsheets by year, using
Norwegian number formatting . I spent time aggregating data from 2012-2017 into one 3
spreadsheet and used excel clean up the formatting. I then upload the “.csv” file to R, converted
the data to an R time-series object, and then wrote the code for Holt-Winters Triple Exponential
Smoothing.

**Results**

Chart 1 shows the Elspot prices for Oslo from 2012 to 2017. I have indicated the seasonal variety
that we see, where prices are the highest during the winter due to increased electricity
consumption and are the lowest during summer months due to low electricity consumption and
people on vacation . The water reservoirs are usually filled up during periods of heavy rain 4
during fall and spring. During the summer, this leads to low energy prices because supply is high
and demand is low, however, during the winter, the demand increases more than the increase in
reservoirs can handle. 

![](/img/elspot_1.png)

Chart 2 shows the triple exponential forecast for the next eight periods, January to August 2018.
The blue line is the predicted values whereas the shaded areas are the upper and lower bound
given the error. The forecast predicts prices to peak during the winter months and decreases
towards the summer, similar to what we historically see in the elspot market. R automatically optimizes the parameters to give me the smallest error. The chart shows the that it is possible to
forecast elspot prices, but there is a limit to the accuracy primarily due to external factors not
expressed by the historical data such a weather uncertainty. 

![](/img/elspot_2.png)
