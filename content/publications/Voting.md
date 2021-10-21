---
date: "2018-09-28"
description: We wrote a decision memo on the implementation of E-voting in the European Union. Our memo was based running a genetic matching algorithm and extending the study conducted by Alvarez R. et al, which looks into citizens perception of e-voting in Salta, Argentina. We replicated their.

fact: Interesting little tidbit shown below image on summary and detail page
featured: true
image: /img/voting1.png
link: /r_htmls/voting.pdf
pubtype: Python Project
sitemap:
  priority: 0.8
tags:
- Python
- E-voting
- Argentina
- European Union
- Genetic Matching
title: 'Implementation of E-voting in the European Union - Genetic Matching'
weight: 400
---

**Code on github**

[Matching on Salta Data](https://gist.github.com/anonymous/a2fbfe3b75f85055a473e8c7235344af) | 
[Genetic Matching on Salta Data](https://gist.github.com/anonymous/3b0d757dc757560d24370144e0d087c9) | 
[Match Balance Comparioson Tables](https://gist.github.com/anonymous/31c35814bdc63b27a494fa7cf388474c)

### Decision Memo: Considerations Before Implementing
**Executive Summary**

The European Commission is considering whether or not to require electronic voting for
member countries of the European Union. Before making this decision, many factors have to be
taken into account, such as feasibility, cost, usefulness, etc. Us at Eurostat were asked by the
European Commission to look into how e-voting affects citizens perception of the voting process.
The paper “Voting Made Safe and Easy: The Impact of e-voting on Citizen Perceptions” by
Alvarez R. et al. looks into citizens perception of e-voting in Salta, Argentina. We replicated their
results and extended their analysis using genetic matching and came to the conclusion that
e-voting is perceived positively by citizens, but there are some concerns about the secrecy of
their votes. We, therefore, recommend the European Commission to look further into how
ballot secrecy can be ensured when implementing e-voting and how to ensure that citizens feel
that their vote is kept secret.


**Introduction**

The paper [Voting Made Safe and Easy: The Impact of e-voting on Citizens Perceptions](https://www.cambridge.org/core/journals/political-science-research-and-methods/article/abs/voting-made-safe-and-easy-the-impact-of-evoting-on-citizen-perceptions/A96562BA348433894BED1F2BA8BC3761) written
by Alvarez, M. R., et al. was published in The European Political Science Association journal in
June 2013. The paper uses data from the partial implementation of e-voting in Salta, Argentina,
during the 2003 election to assess the impact of e-voting on how citizen perceive the voting
process. The implementation of e-voting was not randomized at the voter level but at the
voting-station level. Voting stations covering some districts implemented e-voting, whereas other
districts used the traditional paper ballot method. After voting, voters were asked to fill out a
survey where they answered questions about their demographics and voting experience.

Alvarez et al. used propensity-score matching to evaluate the effect of introducing e-voting on
the voting experience. We replicate their results by first running their code and confirming their
results. Alvarez et al. use the MatchIt package in R (Ho, D. et al., 2011) but the Matching
package (Sekhon, J., 2011) can also be used. Therefore, we replicate their results using the
Matching package in R as well, to see if that improves the match-balance and leads to more
accurate results. Because of the fundamental flaws of propensity score matching we extended Alvarez et al.’s paper by using multivariate genetic matching, as outlined by Alexis Diamond
and Jasjeet Sekhon (2013), instead of propensity score matching. 

**Part 1 - Verifying the original methods by Alvarez et al.**

We were able to replicate their code in R using the data set and code provided by Harvard
Dataverse (n.d.). Our replication gives us the same results as Alvarez et al. present in the paper.
(See Appendix 1) Their code runs properly and the data set provided is complete. Their main
finding is that e-voting is perceived as easier to use than the traditional paper ballot and most
e-voters support substituting traditional voting with e-voting. However, people assigned to
e-voting were also more concerned about the secrecy of their vote. 

![](/img/voting2.png)

**Part 2 - Replicating the results using the Match() function**

Many of the balance statistics provided by the original paper have MatchBalance() p-values well
below 1, indicating a large difference between the control and the treatment group, which leaves large space for confounding variables potentially biasing the result. On the contrary, a more
desirable p-value of 1 for each covariate would indicate identical treatment and control groups,
and thus perfect balance. While the paper applied all tools correctly, we decided to verify the
procedure by matching the dataset with a different package, called Matching. To account for the
same settings as used in the paper, we set the caliper to 0.05, indicating a small standard
deviation distance for each covariate and lower acceptance of observations. This leaves 23
observations but should result in a higher p-value as the matches are of higher quality.
Furthermore, we used propensity score matching as used in the paper, to fairly compare the two
methods.

Using the Match() function from the Matching package for propensity score matching did not
outperform MatchIt, as the balance statistics performed poorer, with lower p-values (see Table
2). The higher the p-value, the lower the statistical significance for the difference between the
two groups, which indicates better matching for that covariate. The p-value was generated using
a T-test for binary variables, and the Kolmogorov-Smirnov test for ordinal variables, since it is a
more precise measure of differences in two distributions. The Match() function from the
Matching package alone was not able to outperform MatchIt, as the balance statistics performed
poorer, with lower p-values (see Table 2). For example, MatchIt was able to balance age group
with a p-value of 1.00, while Match() decreased the initial p-value of 0.53 to 0.04. Nonetheless, 
the real advantage of Matching lies in its extensions of MatchBalance, which allows for evaluation of the matched sets in detail, as well as GenMatch, which runs genetic matching
generating more reliable matching results.

![](/img/voting3.png)

Propensity score matching estimates the effect of e-voting on the voting experience by matching
based on the probability of receiving the treatment, which is defined by the covariates. The goal
is to reduce the bias induced by confounding variables that could affect the treatment effect
based on whether or not a unit received treatment instead of control due to their characteristics.
Gary King and Richard Nielson argue that propensity score matching can increase imbalance,
inefficiency, model dependence, and bias (2016). They recommend using other matching
methods instead because propensity score matching “attempts to approximate a completely
randomized experiment, rather than, as with other matching methods, a more efficient fully
blocked randomized experiment” (King, G. & Nielson, R., 2016). Propensity score matching
makes the assumption that the variables affecting the data generation process are known. This is
usually not the case, and you should, therefore, not use that assumption as the basis for matching. Based on the criticism of propensity score matching we decided to extend their analysis using
multivariate genetic matching.

**Part 3 - Extending with multivariate genetic matching**

Genetic matching is “a multivariate matching method, that uses an evolutionary search algorithm
to determine the determine the weight each covariate is given” (Diamond, A. et al., 2012).
Quickly explained, an evolutionary algorithm uses a cost function, which is the balance
achieved, to grade the population and decides which units to keep and which ones to discard. It
uses random mutations to change parts of the “gene” and crossover to mix the “genes” of the
already existing population. The gene, in this case, is the set of weights for each of the
covariates. After multiple iterations, the balance improves and if the algorithm runs for enough
iterations, you will achieve an optimal balance. If the matching improves the covariate balance,
we can conclude that the method is better than the propensity-score matching used by Alvarez et
al.

We use the Matching and rgenound packages to run genetic matching on the balance matrix they
use to check their match balance. We included demographic variables for our genetic matching
such as age group, education, use of technology, where they get political info from, job data, and
gender. We run the GenMatch function with e-voting as the treatment to get the covariate
weights. We used a population size of 500 to ensure that we get the optimal balance. The caliper
is set to 0.05, the same as in the original paper, to ensures that the matching does not happen if
units are further than 0.05 standard units away to prevent a decrease in matchbalance. We then run nine different matching functions, one for each of the nine outcomes, using the weight 
matrix we got from running the genetic algorithm.

The estimated effect of e-voting obtained by our genetic matching model is similar to the results
in the original paper (See Table 3). Our standard deviation for all the outcomes is lower than in
the original paper which gives us smaller confidence intervals. All the p-values are under 0.05
which means that all our estimates pass our 0.05 significance test. The lowest p-value is for
“speed of voting process” at 0.026. The genetic matching function only found matches for 487 of
the original 1054 observations, however a lower quantity of data does not necessarily mean
lower quality of the results if the data can provide more insight. Despite the lower number of
observations, we can assume our results are valid since our matches are very high with p-values
of 1 and the estimates prove statistically significant with p-values of <0.05. We do a balance test
to see how the genetic matching function performs in improves the covariate balance. Before the
matching nine of the 16 variables in the balance are statistically different between the treatment
and control group. After the genetic matching, none of the variables have a statistically
significant difference between the treatment and control group. Actually, there is no difference
between the treatment and control group after the genetic matching in implemented (See Table
2). All the p-values are 1.00 which indicates a perfect match on the covariates between the two
groups. This indicates that by running genetic matching, we can remove all possible confounding
cause by the observed covariates. It is important to note that we do not know anything about the
unobserved covariates and whether or not they influence the treatment effect.

![](/img/voting4.png)

**Conclusion**

Given the decreased confidence in ballot secrecy for electronic voting, the European
Commission should with priority investigate how to ensure ballot secrecy, as well as its
perception by citizens. The other indicators suggest that electronic voting positively influenced
the perception of voting, making it less difficult and made people feel more confident their vote
was counted. These results align with the original paper’s conclusions. However, the data these
two papers are based on stems from a survey held in 2003. Since then, technologies and people’s
perception of it changed greatly, therefore we recommend to supplement these findings with
newer methods and analyses if the budget for allows it.


