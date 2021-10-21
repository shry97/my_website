---
date: "2021-09-26"
description: The Guardian newspaper had an election poll tracker for the 2021 German election. We scraped the list of the opinion polls data since January 2021 from Wikipedia and reproduced a graph similar to the one produced by the Guardian.
fact: Interesting little tidbit shown below image on summary and detail page
featured: true
image: /img/german_election.png
link: /r_htmls/homework1_groupb9_final.html
pubtype: R Project
sitemap:
  priority: 0.8
tags:
- R
- The Guardian
- Replication
- Scraping data
- Elections
- Germany
title: 'Replicating the German election opinion poll'
weight: 400
---

[The Guardian newspaper had an election poll tracker](https://www.theguardian.com/world/2021/sep/24/german-election-poll-tracker-who-will-be-the-next-chancellor) for the 2021 German election. We scraped the list of the opinion polls data since January 2021 from [Wikipedia](https://en.wikipedia.org/wiki/Opinion_polling_for_the_2021_German_federal_election) and reproduced a graph similar to the one produced by the Guardian. 

We used the tables function in R to scrape wikipedia and cleaned the data in order to create a ggplot of the opinion polls. 