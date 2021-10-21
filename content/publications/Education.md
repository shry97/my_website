---
date: "2018-09-28"
description: I used the Current Population Survey (CPS) data from 2017 to look at the difference in education level for adults 25 years or older living in metropolitan areas and non-metropolitan areas. 

fact: Interesting little tidbit shown below image on summary and detail page
featured: true
image: /img/edu1.png
link: https://gist.github.com/shry97/6f0ea2e80b41b21c9fed0792e3b6e9c8#file-homework-1-ss154-sherington-anton-amarapala
pubtype: Stata Project
sitemap:
  priority: 0.8
tags:
- Stata
- Education
- Current Population Survey
- Regression
- United States
title: 'Difference in degree attainment between metropolitan and non-metropolitan areas'
weight: 400
---

**Research Question**

I want to look at the difference in education level for adults 25 years or
older living in metropolitan areas and non-metropolitan areas. I hypothesize is that there is a
difference in the percentage of adults with a college or university degree between metropolitan
and non-metropolitan areas. The main problem of causal inference is the identification problem which is the difficulty of separating causation and association. I assume that whether or not a
person lives in a metropolitan area is influenced by the same variables that influence whether or
not a person has a degree or not, for instance, income, parents education level, distance to
universities, and access to financial aid . Therefore, I can assume that metropolitan status is a
good indication of the probability of having a degree or not.


**Descriptive Statistics**

I cleaned the data so that my sample only consists of adults aged 25 and above. I also created a
binary variable named degree, that is based on the variable indicating Educational Attainment
(a_hga), that indicates whether or not an individual has a degree. The pie charts show the
percentage of people with and without a degree based on metropolitan status. These pie charts
clearly indicate that for the sample population there is a difference in the probability of having a
degree or not based on metropolitan status.


**Results**

Chart 1 shows the Elspot prices for Oslo from 2012 to 2017. I have indicated the seasonal variety
that we see, where prices are the highest during the winter due to increased electricity
consumption and are the lowest during summer months due to low electricity consumption and
people on vacation . The water reservoirs are usually filled up during periods of heavy rain 4
during fall and spring. During the summer, this leads to low energy prices because supply is high
and demand is low, however, during the winter, the demand increases more than the increase in
reservoirs can handle. 

![](/img/edu2.png)

**Joint Probability Table**

Table 1 is a joint probability table for the sample showing the probability of a random person in
the sample falling into one of four categories and the number of people within each category.
This table can be contrasted with Table 2 in the Appendix, that is illustrated by the pie charts on
the previous page, showing the conditional probability of a person having a degree or not based
on the metropolitan status.

![](/img/edu3.png)


**Hypothesis Testing**

My research question is whether or not there is a difference in the percentage of adults with a
college or university degree between metropolitan and non-metropolitan areas. My claim is that
there is a significant difference between the means . To perform a hypothesis test, I first need to 
define my null hypothesis, H0 and alternative hypothesis, Ha.
![](/img/edu4.png)

I am doing a t-test to check if the probability distribution of the difference in means for the
sample is around the mean of 0 or not. If it is, the alternative hypothesis will be true, whereas if it is not, the null hypothesis is true . This is a two-tailed test because I am not making any claims as 7 to which metropolitan status has the highest probability of an individual having a degree. I am performing a 95% significance test, where the null hypothesis is rejected if the t-value falls within the two tails. The critical value for the left-tail is αl=0.025 and the critical value for the right-tail is αr=0.975 because the 5% alpha level is split between the two tails.

![](/img/edu5.png)

I run a simple linear regression in Stata with the dependent variable being degree and
independent variable being metropolitan status.

![](/img/edu6.png)
The regression table, Table 3 gives us the t-score t = -30.08, coefficient β ≈ -0.112 and a 95%
confidence interval of [-0.119, -0.105]. The t-score t= -30.08 falls outside the rejection region
-1.96 < t < 1.96 and therefore the null hypothesis is accepted.

**Conclusion**
The table and pie charts under descriptive statistics show that there is a difference in the
percentage of people having degrees and not based on their metropolitan status. However, this
does tell us anything about the significance of the difference. After performing the hypothesis
test, I can say that there is a significant difference in the probability of having a degree or not,
given metropolitan status, and that there is a 95% chance that a sample mean will fall within
[-0.119, -0.105]. I estimate that there is an 11.2% higher chance of having a degree for a random
individual living in a metropolitan area compared to a random individual living in a
non-metropolitan area.







