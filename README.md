# COVID-19 in the Netherlands
_Author: Jay Lee_  
<i>Last update: Sat, Dec 11, 2021  4:51:10 PM</i>

Table of Contents
=================

* [Links and notes](#links-and-notes)
* [Netherlands](#netherlands)
   * [National trend](#national-trend)
   * [Hospital occupancy trends](#hospital-occupancy-trends)
   * [Within NL cities/towns/provinces](#within-nl-citiestownsprovinces)
* [Trends in nearby countries](#trends-in-nearby-countries)
* [Covid by age](#covid-by-age)
   * [Cases by age group](#cases-by-age-group)
      * [Delay of age data](#delay-of-age-data)
   * [Hospitalization by age group](#hospitalization-by-age-group)
* [Risk calculations](#risk-calculations)
   * [Hospitalization risk](#hospitalization-risk)
   * [Personal risk](#personal-risk)
      * [Summary](#summary)
      * [The (wonky) math](#the-wonky-math)
* [Appendix](#appendix)
   * [Global and other countries](#global-and-other-countries)
   * [USA](#usa)
   * [Maths](#maths)
      * [Personal risk calculation math](#personal-risk-calculation-math)
      * [Basis for hospitalization risk](#basis-for-hospitalization-risk)
      * [Hospitalization risk by age](#hospitalization-risk-by-age)
   * [Code](#code)

  
  
  
# Links and notes  
  
* [121021:] [Report now on GitHub](https://github.com/JaySLee/covid/blob/main/README.md)  
  - But the inline math is bottom-aligned, so a bit ugly.  
* This document will be updated every few days or so.  
* <ins>New additions:</ins>  
  - 20.11.21 - [Hospitalization risk by age](#hospitalization-risk-by-age)  
  - 17.11.21 - [Covid by age](#covid-by-age)  
  
  
  
  
  
# Netherlands  
## National trend  
  
* Latest new cases = 17712 (RIVMc), 17828 (RIVMn) &rarr; +266  
  - RIVMc is computed from the cumulative file while RIVMn is specifically new cases data. Not sure why there's a difference.  
* We're ~~25%~~ ~~50% higher~~ nearly double than the last highest peak (Christmas/New Years 2020-21).  
* ~~While the numbers have dropped since yesterday (Friday, Nov. 19, 2021),~~ there's usually a drop in the reported numbers around the weekend, and then a surge in Monday/Tuesday.  
* Just remember: there are about 10x as many infectious ~~zombies~~ people wandering about compared to the latest reported daily new cases.  
  - ~~For NL on Nov. 15, 2021, this is 19054\*10 = \~200K (or over 1% of the NL population).~~  
  - Nov. 18, 2021, 23591*10 = ~236K = 1.35% of NL population  
  - [112121:] Looking at the infectious estimates produced by RIVM (that they kept updated until July, 2021), it seems this multiplier is more like 15x -- 20x.  
* The figures below show raw new case counts (no moving average) and deaths (7 day moving average).  
* Red line indicates last count; green line = 7 day moving average  
  
<p align="center"> <img src="/fig/cv_nl_nat.png" width="80%"> </p>  
  
<p align="center"><img src="/fig/cv_nl_nat_60.png" width="40%"><img src="/fig/cv_nl_deaths.png" width="40%"></p>  
  
* Source: RIVM _(releases updated data daily at 15:15 CET)_  
  
  
  
## Hospital occupancy trends  
* [121021:] A few days ago, LCPS split ICU numbers by NL and "International" (i.e. in beds in Germany). Those are combined here.  
  - The latter includes "the number of COVID patients moved abroad from the Netherlands. This currently concerns COVID IC patients who have gone from the Netherlands to a hospital in Germany."  
* [112721:] Hospitalizations are &#128543;.  
* [111621:] Hospitalizations are not as dire as earlier this year and last year, but almost there :-/.  
  
  
  
<p align="center"><img src="/fig/cv_lcps.png" width="80%"></p>  
  
<p align="center"><img src="/fig/cv_lcps_60.png" width="40%"></p>  
  
* Source: LCPS _(releases data daily between 1pm-2pm CET)_  
  
  
  
## Within NL cities/towns/provinces  
  
* More new cases per capita in the smaller towns than national level.  
* Last 60 days only (otherwise, the plot becomes messy).  
* Both plots show 7 day moving average.  
* Cities ordered from worst to best (within those displayed).  
* Left plot: worst cities; right plot: Largest cities in NL (top 5%)  
* [NEW 121021:] Lower plot: provinces  
  
<p align="center"><img src="/fig/cv_nl_top_60.png" width="40%"><img src="/fig/cv_nl_05_60.png" width="40%"></p>  
<p align="center"><img src="/fig/cv_nl_prov_60.png" width="40%"></p>  
  
* Source: RIVM  
  
  
# Trends in nearby countries  
  
* As for countries near us: Belgium, Germany, Austria, and Denmark are also experiencing their own massive peaks, record-breaking for Germany and Austria. France is experiencing a minor surge.  
  
<p align="center"><img src="/fig/cv_nearby.png" width="80%"></p>  
<p align="center"><img src="/fig/cv_nearby_60.png" width="40%"></p>  
  
* Source: CSSE (data is one day behind the RIVM and LCPS data)  
  
  
  
# Covid by age  
  
## Cases by age group  
* Just the age groups of our students, at 3 levels of measurement.  
  - National (NL)  
  - Province (Zuid-Holland)  
  - Local (GGD Rotterdam)  
* RIVM groups ages by decade.  
* Smooth curves fit the data points (loess).  
* Upper plots show 7-day moving average.  
* Lower plots no moving average (but dates are more restricted for zooming).  
* Left plots shows **relative** proportion across all age groups.  
* Right plots shows absolute percentages within population of the age group.  
  - Also, in the right plots: <red>**_the last/rightmost 6-8 points are incomplete (data), thus the sharp drop._**</red>  
  - On Nov 15, 2021, ~0.15% of all NL 20-29 year-olds have covid.  
    + They also constitute ~18% of the infected on the same date.  
* GGD Rotterdam throws up some extreme values for last date.  
* <ins>Observations:</ins>  
  - A recent relative uptick of cases in the two relevant age groups.  
  - The percentages within age groups are more striking.  
  
<p align="center"><img src="/fig/cv_age_case.png" width="40%"> <img src="/fig/cv_age_case2.png" width="40%"></p>  
<p align="center"><img src="/fig/cv_age_case3.png" width="40%"> <img src="/fig/cv_age_case4.png" width="40%"></p>  
  
  
  
<img align="right" src="fig/cv_age_delay.png" width="30%">  
  
### Delay of age data  
  
  
  
* Dates of case/age data are offset by +3 days in the plot below.  
* So two kinds of delays:  
  - RIVM country totals data (of all new cases) is behind the age data by 3 days.  
  - But comprehensive age data for the past week is incomplete/delayed significantly.  
  
  
  
## Hospitalization by age group  
  
* _Hospitalization data is updated once a week, Wednesdays_.  
* [112421:] _There was a bug in my code that made these graphs inaccurate; fixed now._  
* Age groups of just EUR students and lecturers shown here.  
* LCPS groups age in 5-year bins.  
* LCPS releases these on a weekly basis.  
* First two plots show 7-day moving average.  
* Upper left plot shows relative proportion across all age groups.  
  - Young age groups are merged due to misalignment between hospital and case data.  
  - _Relative proportion generally going down largely because of (relatively) more hospitizalizations in the older (not shown) age groups._  
* Upper right plot shows ratio of hospitalizations to number of cases.  
  - These proportions is an upper bound, as there are far more contagious cases thanindicated by a daily case number and also considering not all cases are registered by RIVM.  
  - _Under that assumption, there is currently < 1% chance of hospitalization after infection._  
  - _The diminishing curves for the older age groups may be indicative of the vaccine's effectiveness._  
* The lower two plot shows _percentage_ within population of each age group.  
  - The right plot shows a LOESS regression fit.  
  - Because the recent week's LCPS age data (i.e. most recent date) are incomplete, points are omitted in these two plots.  
  - _Hospitalizations are going up for all age groups._  
  
  
<p align="center"><img src="/fig/cv_age_hosp.png" width="40%"> <img src="/fig/cv_age_hosp_covid.png" width="40%"></p>  
<p align="center"><img src="/fig/cv_age_hosp2.png" width="40%"> <img src="/fig/cv_age_hosp_loess.png" width="40%"></p>  
  
  
# Risk calculations  
## Hospitalization risk  
  
<ins>**tl;dr:**</ins> (based on Nov 13, 2021 numbers)  
* Risk of getting covid, while being double vaxxed = 0.27%  
* Risk of hospitalization, given getting covid and vaxxed = 1.26% -- 2.53%  
* Risk of ICU, given getting covid and vaxxed = 0.40%  
  
These calculations are based on Nov. 13, 2021 numbers and some simplifying assumptions, that perhaps render the numbers below as upper bounds.  
  
* Probability of getting covid (![](https://latex.codecogs.com/svg.latex?C)), given being double vaxxed (![](https://latex.codecogs.com/svg.latex?V)) vs. non-double vaxxed (![](https://latex.codecogs.com/svg.latex?\sim\\!\\!&space;V)):    
![](https://latex.codecogs.com/svg.latex?p(C|V)=0.27\%)  
![](https://latex.codecogs.com/svg.latex?p(C|\sim\\!\\!&space;V)=0.66\%)  
* For ages 10-19: ![](https://latex.codecogs.com/svg.latex?1.00\%,&space;2.50\%) (see `f.cv.bayesv2()`)  
  - Based on Nov. 15, 2021 (peak for age/case data)  
  - Vacc/age v. Case/age groups don't perfectly align (consider interpolation or better data)  
  
  
  
* Probability of ending up hospitalized (![](https://latex.codecogs.com/svg.latex?H)), given being (double) vaxxed and having covid:    
![](https://latex.codecogs.com/svg.latex?p(H|V\\&C)&space;=&space;1.26\%&space;-&space;2.53\%)  
![](https://latex.codecogs.com/svg.latex?p(H|\sim\\!\\!&space;V\\&C)&space;=&space;1.29\%&space;-&space;2.58\%)   
   - The ranges are nearly equivalent largely b/c there are more people vaxxed than not. When hospital numbers -- between vax and non-vaxxed -- are near even but the vaxxed rate in the population goes higher, this means the vax is offering diminishing protection.  
   - Range is based on (perhaps severe) uncertainty over how many covid cases could be bound for hospital at any given time (10x v. 5x current new cases).  
  
* Probability of ending up in the ICU (![](https://latex.codecogs.com/svg.latex?I)), given being vaxxed and having covid:    
![](https://latex.codecogs.com/svg.latex?p(I|V\\&C)&space;=&space;0.40\%)  
![](https://latex.codecogs.com/svg.latex?p(I|\sim\\!\\!&space;V\\&C)&space;=&space;0.61\%)  
  
<ins>Assumptions:</ins>  
* Does not take into account clusters/heterogeneity of contacts and other factors, e.g., sociodemographics (namely **age**), students' self-quarantining, etc.  
* The above numbers are based on Nov 13, 2021 covid and hospitalization numbers.  
  - ![](https://latex.codecogs.com/svg.latex?n_C&space;=&space;13743\text{,&space;}n_{H|C}&space;=&space;(353+1402))  
* Unless stated otherwise, I use the assumption of there being 10x as many actual infectious people as reported by RIVM (which in its data shows this to be much higher).  
* Also, Google reported 67.6% of the NL population double vaxxed (when I last checked this number); the 83+% reported by NL times is based on the eligible population.  
  - As of 20.11.21, the vaccination proportion is 0.723.  
* Effectiveness of vaccine (given delta and time) has reportedly dropped to ~60% (pessimistic estimate).  
* ![](https://latex.codecogs.com/svg.latex?p(V|H)&space;=&space;.45); ![](https://latex.codecogs.com/svg.latex?p(V|I)&space;=&space;.65) (optimistic estimates) based on the following excerpt from an NL times report:  
  
> In October, just over half of all Covid-19 patients in the hospital were not or only partially vaccinated ... In ICU, the proportion of unvaccinated patients dropped from over 80 percent in September to about 70 percent in October.  
  
  
  
## Personal risk  
  
<ins>**_Caveats:_**</ins>  
* Some simplifying assumptions used here.  
* Covid numbers from Nov. 13, 2021.  
  
### Summary  
  
<ins>tl;dr: (too long didn't read):</ins>  
  
For those with 2 tutorials, the risk is a **18.1%** chance of catching covid over 8 weeks, conditioned on your being vaxxed.  
For those with 3 tutorials &rarr; **24.5%** risk.  
For JdV with 4 tutorials &rarr; **29.7%** risk.  
  
**85.0% chance at least one of the tutorial instructors will get covid sometime throughout Term 2.**  
* Remember these are pessimistic/upper bounds and don't fully consider students' self-quarantining.  
* Also, this doesn't take into account that none of us has yet gotten covid by week 2.  
  
### The (wonky) math  
  
1. First, we have the population of NL:  
![](https://latex.codecogs.com/svg.latex?n_\text{pop}&space;=&space;17.44M)  
2. Next, the reported number of new cases (on Nov. 13, 2021):  
![](https://latex.codecogs.com/svg.latex?n_\text{c0}&space;=&space;13743)  
![](https://latex.codecogs.com/svg.latex?m&space;=&space;5) ... the multiplier that accounts for the number days a person could be infections and unreported cases; I'm conservative here as the rule of thumb is more like 10x.  
3. This gives us conservative estimate of total covid infectious people:  
![](https://latex.codecogs.com/svg.latex?n_\text{c}&space;=&space;n_\text{c0}&space;\times&space;m)    
4. Yielding the proportion of infectious people which estimates the probability of running into an infections person; this doesn't account for clusters of infection (e.g., Limburg):  
<img src="https://latex.codecogs.com/svg.latex?\begin{align*}p_\text{c}&space;&=&space;\frac{n_\text{c}}{n_\text{pop}}\\&=&space;0.00394\end{align*}"/>
  
5. Next, we have the probability of covid's being transmitted (![](https://latex.codecogs.com/svg.latex?T)) from an infected individual (![](https://latex.codecogs.com/svg.latex?C)). I use a more conservative number than the 0.632 reported (for a closed room):  
![](https://latex.codecogs.com/svg.latex?p(T|C)&space;=&space;0.2)  
6. So then, the probability of catching covid is (from any one person):  
![](https://latex.codecogs.com/svg.latex?p_\text{C1}&space;=&space;p(T|C)\times&space;p(C)&space;=&space;p(T|C)p_c)  
  
7. The personal chances of catching covid over a period of time with multiple contacts:  
![](https://latex.codecogs.com/svg.latex?p_\text{C}&space;=&space;(1-(1-p_\text{C1})^k)) ... where ![](https://latex.codecogs.com/svg.latex?k) is number of people I run into.  
   - The inner part of the equation represents the chances of never running into covid -- after running into ![](https://latex.codecogs.com/svg.latex?k) people -- and having it be transmitted. The more enumerated version of this where I consider tramission probability for every ![](https://latex.codecogs.com/svg.latex?k) contact, i.e. chances with 1 contact, chances with 2 contacts, etc. ends up being equal to the above equation (math is funny!).  
  
8. <ins>Aside:</ins> let's see what the avg number of contacts across NL would be then:  
![](https://latex.codecogs.com/svg.latex?(n_\text{pop}&space;-&space;n_\text{c})(1-(1-p_\text{C})^a)&space;=&space;2n_\text{C}) ... where ![](https://latex.codecogs.com/svg.latex?a) is avg number of daily social contacts (avged across all of NL) and ![](https://latex.codecogs.com/svg.latex?2n_C) is est. of newly infected daily people (2x b/c of unreported)  
This gives us an average number of contacts (for all in NL):  
![](https://latex.codecogs.com/svg.latex?a\approx2) ... which seems to be a reasonable avg.  
  
9. If I am proximal to 20 people (inc. students) every time I come to campus over 8 weeks (i.e. 8 instances), my personal risk is:  
![](https://latex.codecogs.com/svg.latex?(1-(1-p_\text{C})^{(20\times8)})&space;=&space;.118&space;=&space;11.8\%) ... this is my chance -- assuming my vax status is unknown -- of catching covid during Term 2, giving the once-a-week recap lecture.  
   - This doesn't take into account that I'm vaccinated, in which case my risk is 6.0\%.  
   - _This is likely an upper bound as I don't consider students' self-quarantining._  
   - See [appendix](#personal-risk-calculation-math) for the math on the calculations of that 6.0\%.  
  
_For those with 2 tutorials:_  
- A conservative estimate of number of proximal contacts would be 20 (students) + 20 (extra people you might be proximal to each time you commute) = 40 people per week &rarr; **18.1%** chance of catching covid over 7 tutorial week, conditioned on your being vaxxed.  
- Overall risk (for both vaxxed and non-vaxxed) is 35.7%  
  
_For those with 3 tutorials_ &rarr; **24.5%** risk.  
- Overall risk (for both vaxxed and non-vaxxed) is 48.4%.  
  
_For JdV with 4 tutorials_ &rarr; **29.7%** risk.  
- Overall risk (for both vaxxed and non-vaxxed) is 58.5%  
  
_Across all 8 tutorial instructors_, average risk is:  
![](https://latex.codecogs.com/svg.latex?(.181\times5+.245\times2+.297\times1)/8&space;=&space;.211) or 21.1\% // this approach is rough  
![](https://latex.codecogs.com/svg.latex?1-(1-.211)^8) = .850 = **85.0% chance at least one of the tutorial instructors will get covid**.  
* But remember this is an upper bound.  
* ![](https://latex.codecogs.com/svg.latex?(1-.211)^8&space;=&space;.150) &rarr; probability that none of the 8 ISA tutorial instructors get covid.  
  
  
# Appendix  
  
## Global and other countries  
  
* Left plot is top 25 countries (in descending order), over the last 60 days.  
* Right plot contains various countries that came to my attention (e.g., being in the news) or of personal interest.  
  - Ordered by when the country came to my attention, and not by new cases.  
* The orange denotes the latest NL moving average (7 day) and not the latest daily new cases.  
* Both plots use 7-day moving average ("7day").  
   
<p align="center"><img src="/fig/cv_glob_60.png" width="40%"> <img src="/fig/cv_cos_60.png" width="40%"></p>  
  
## USA  
  
  
  
* Top plot:  
  - New infections per 100K  
  - 7 day moving average, last 60 days, top 25 states  
  - The <red>red</red>, <div class="OutlineText" display:inline>white</div>, <blue>blue</blue> horizontal line is the national average.  
* Lower left plot:  
  - New infections per 1M  
  - 7 day moving average, whole pandemic (for which there is data)  
* Lower right plot  
  - Same as previous but with deaths data.  
  
<p align="center"><img src="/fig/cv_usa.png" width="80%"></p>  
  
<p align="center"><img src="/fig/cv_nl_v_usa.png" width="40%"> <img src="/fig/cv_nl_v_usa_deaths.png" width="40%"></p>  
  
  
## Maths  
  
### Personal risk calculation math  
  
Given probability of risk, whether or not I'm vaxxed:  
![](https://latex.codecogs.com/svg.latex?(1-(1-p_\text{C})^{(20\times8)})&space;=&space;.118&space;=&space;11.8\%)  
  
We know the ratio of acquiring covid given vaxxed/non-vaxxed:  
![](https://latex.codecogs.com/svg.latex?\frac{p(C|V)}{p(C|\sim\\!\\!&space;V)}&space;=&space;\frac{.27}{.66})  
  
Let ![](https://latex.codecogs.com/svg.latex?\frac{x}{y}&space;=&space;\frac{.27}{.66})  
Then ![](https://latex.codecogs.com/svg.latex?x&space;=&space;\frac{.27y}{.66})  
Now, leting ![](https://latex.codecogs.com/svg.latex?a&space;=&space;\frac{.27}{.66})  
We get ![](https://latex.codecogs.com/svg.latex?x&space;=&space;ay)  
  
  
We also realize the weighted sum using population ![](https://latex.codecogs.com/svg.latex?p(V)) numbers should result in that ![](https://latex.codecogs.com/svg.latex?.118):  
![](https://latex.codecogs.com/svg.latex?(1-p(V))x&space;+&space;p(V)y&space;=&space;.118)  
Given ![](https://latex.codecogs.com/svg.latex?p(V)&space;=&space;.676) // proportion of population vaxxed  
![](https://latex.codecogs.com/svg.latex?(1-p(V))ay&space;+&space;p(V)y&space;=&space;.118)  
![](https://latex.codecogs.com/svg.latex?(1-.676)ay&space;+&space;.676y&space;=&space;.118)  
![](https://latex.codecogs.com/svg.latex?ay&space;-&space;(.676)ay&space;+&space;.676y&space;=&space;.118)  
![](https://latex.codecogs.com/svg.latex?(a&space;-&space;.676a&space;+&space;.676)y&space;=&space;.118)  
![](https://latex.codecogs.com/svg.latex?y&space;=&space;.146)  
![](https://latex.codecogs.com/svg.latex?x&space;=&space;.060)  
  
My risk over 8 weeks is ![](https://latex.codecogs.com/svg.latex?.060&space;=&space;6.0\%)  
  
  
### Basis for hospitalization risk  
_112021_  
  
Vaccine effectiveness = proportion of covid among unvaxxed minus proportion of covid among vaxxed, all divided by proportion of covid among unvaxxed.  
* ![](https://latex.codecogs.com/svg.latex?n_\text{c0}) = number of unvaxxed people with covid  
* ![](https://latex.codecogs.com/svg.latex?n_\text{c1}) = number of vaxxed people with covid  
* ![](https://latex.codecogs.com/svg.latex?n_C) = number of covid infections  
* ![](https://latex.codecogs.com/svg.latex?p(V)) = proportion of population vaxxed (really should be ![](https://latex.codecogs.com/svg.latex?\text{Pr}(V)))  
* ![](https://latex.codecogs.com/svg.latex?n) = NL population  
* ![](https://latex.codecogs.com/svg.latex?E) = vaccine effectiveness percentage, as a probability. Originally touted to be ~95%, I've reason to assume -- based on some reports -- that it's dropped to 60% due to the delta variant, so that's the value I use here.  
  
Let ![](https://latex.codecogs.com/svg.latex?p(C)&space;=&space;\frac{n_C}{n}) // proportion of population with covid. One could just use ![](https://latex.codecogs.com/svg.latex?n_C) in lieu of ![](https://latex.codecogs.com/svg.latex?np(C)) below; not sure why I didn't do just that.  
![](https://latex.codecogs.com/svg.latex?E&space;=&space;\left(&space;\frac{n_\text{c0}}{n(1-p(V))}&space;-&space;\frac{n_\text{c1}}{np(V)}&space;\right)&space;/&space;\left(&space;\frac{n_\text{c0}}{n(1-p(V))}&space;\right)) // vaccine effectiveness  
We now want to solve for number of infections within the vaxxed and unvaxxed, ![](https://latex.codecogs.com/svg.latex?n_\text{c1}) and ![](https://latex.codecogs.com/svg.latex?n_\text{c0}), respectively.  
![](https://latex.codecogs.com/svg.latex?E&space;=&space;1&space;-&space;\frac{n_\text{c1}}{np(V)}&space;/&space;\frac{n_\text{c0}}{n(1-p(V))}) // use a known E to solve for ![](https://latex.codecogs.com/svg.latex?n_\text{c0})  
Let ![](https://latex.codecogs.com/svg.latex?K&space;=&space;\frac{np(V)(1-E)}{n(1-p(V))})  
Yielding ![](https://latex.codecogs.com/svg.latex?n_\text{c1}&space;=&space;Kn_\text{c0})  
Given ![](https://latex.codecogs.com/svg.latex?np(C)&space;=&space;n_\text{c1}&space;+&space;n_\text{c0})  
Then ![](https://latex.codecogs.com/svg.latex?n_\text{c0}&space;=&space;\frac{np(C)}{1+K}) // calculated unvaxxed count given known ![](https://latex.codecogs.com/svg.latex?E,&space;n,&space;p(V),&space;p(C))  
and &nbsp; <img src="https://latex.codecogs.com/svg.latex?\begin{align*}n_\text{c1}&space;&=&space;np(C)&space;-&space;n_\text{c0}\\&=&space;\frac{Knp(C)}{K+1}\end{align*}"/>
  
Probability of infection (![](https://latex.codecogs.com/svg.latex?C)), given vax (![](https://latex.codecogs.com/svg.latex?V)) or non-vax (![](https://latex.codecogs.com/svg.latex?\sim\\!\\!&space;V)):  
![](https://latex.codecogs.com/svg.latex?p(C|V)&space;=&space;\frac{n_\text{c1}}{np(V)})  
![](https://latex.codecogs.com/svg.latex?p(C|\sim\\!\\!&space;V)&space;=&space;\frac{n_\text{c0}}{n(1-p(V))})  
  
Calculating probability of hospitalization (![](https://latex.codecogs.com/svg.latex?H)) given vax and covid infection:  
![](https://latex.codecogs.com/svg.latex?p(V,C)&space;=&space;p(C|V)p(V)) // both are now known  
![](https://latex.codecogs.com/svg.latex?p(V|H,C)&space;=&space;p(V|H)&space;=&space;0.45) // from NL Times and also we're talking just about covid hospitalizations, i.e. we don't have to worry about non-covid hospitalizations since we have the numbers for covid hospitalizations. This makes ![](https://latex.codecogs.com/svg.latex?p(V|H)&space;=&space;p(V|H,C)). The rest are known.  
<img src="https://latex.codecogs.com/svg.latex?\begin{align*}p(H|V,C)&space;&=&space;\frac{p(V|H,C)p(H,C)}{p(V,C)}&space;\\&=&space;\frac{0.45\times&space;p(H|C)p(C)}{p(C|V)p(V)}\end{align*}"/>
  
  
### Hospitalization risk by age   
_112021_  
  
* Does not include vax status, yet.  
  
Probability of hosp given age and covid  
- LCPS=112021, hage=101121-111521, summed and normed,  
- page=`f.cv.age()`, cage=111521-112021, summed and normed  
- ![](https://latex.codecogs.com/svg.latex?a) = age group 10-19  
  
<img src="https://latex.codecogs.com/svg.latex?\begin{align*}p(H|A=a,C)&space;&=&space;p(A=a|H,C)p(H,C)&space;/&space;p(A=a|C)&space;\\&=&space;(0.003750493+0.009080142)*(432+1785)/(21873)&space;/&space;.164&space;\\&=&space;0.007929789\\p(H|A=a)&space;&=&space;(0.003750493+0.009080142)*(432+1785)/(17.44e6)/(0.055+0.060)&space;\\&=&space;1.418305e-05\end{align*}"/>
  
Same as above but for ![](https://latex.codecogs.com/svg.latex?a) = ages 50-59  
<img src="https://latex.codecogs.com/svg.latex?\begin{align*}p(H|A=a,C)&space;&=&space;(0.050927754+0.060205290)*(432+1785)/(21873)&space;/&space;.135&space;\\&=&space;0.08343856&space;\\p(H|A=a)&space;&=&space;(0.050927754+0.060205290)*(432+1785)/(17.44e6)&space;/(.074+.072)&space;\\&=&space;9.676305e-05\end{align*}"/>
  
* Given ![](https://latex.codecogs.com/svg.latex?A,C): 10.5x worse than 10-19 stud, more C among studs makes ratio worse  
  - ![](https://latex.codecogs.com/svg.latex?\frac{p(H|C,A=a_\text{teach})}{p(H|C,A=a_\text{students})})  
* Given just ![](https://latex.codecogs.com/svg.latex?A): only 6.8x worse b/c more people my age brings this down  
* For vacc, just use the above number and realize the ![](https://latex.codecogs.com/svg.latex?p(C|V,A)&space;=&space;0.01) and ![](https://latex.codecogs.com/svg.latex?p(C|\sim\\!\\!&space;V,A)&space;=&space;0.025).  
  - But not so straightforward given ![](https://latex.codecogs.com/svg.latex?p(V|H)&space;=&space;.45).  
  
  
## Code  
  
* `f.cv.plot.sav()` // defaults to all modes 0-4  
* `f.cv.bayesv(n=17.44e6,pC=NULL,pVH=.35,pVC=NULL,pV=.676,pE=0.6,npC=13743*5,nH=353+1420)`  
* `f.cv.plot.sav()`  
* ~~`electron-pdf cv.html cv.html.pdf`~~  
* `cp_cv -ci` // Chrome then copy to isa  
* `f.cv.bayesv2()`  
  
