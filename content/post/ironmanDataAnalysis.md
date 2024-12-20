+++
title = 'Ironman Triathalon Data - Market Insights'
date = 2024-12-20T14:15:07-06:00
draft = false
tags = [
    "Personal Projects",
    "Python",
    "Data Analysis",
    "Data Visualization",
    "Sports"
]
thumbnail = "images/ironmanlogo.png"
featureImage = "images/ironmanlogo.png"
+++


<!-- TOC --><a name="project-background"></a>
## Project Background
The goal of this project is to investigate Ironman 140.6 race/performance data in order to provide recommendations on potential future budget marketing strategies.

**The IRONMAN Group** is a global organization that operates a wide range of endurance sports events. They are best known for their IRONMAN Triathlon Series, which includes full-distance and half-distance triathlons. The full IRONMAN race consists of a 2.4-mile swim, a 112-mile bike ride, and a 26.2-mile marathon run. This group is owned by Advance, a private, family-owned business, and Orkila Capital, a growth equity firm. They have grown significantly since their inception in 1978 and now host events in over 55 countries.

**The goal of this data analysis is to identify potential emerging demographic trends based on participant data.**

**Useful Resources**
Python Analysis Notebook: [here](https://github.com/miguswong/IronmanDataAnalysis/blob/main/IronMan%20Data%20Analysis.ipynb)
Kaggle Dataset: [here](https://www.kaggle.com/datasets/miguswong/ironman-140-6-results-dataset-2002-2024)
Webscraping Process: [here](https://github.com/miguswong/IronmanScraper)


<!-- TOC --><a name="dataset-structure"></a>
## Dataset Structure
![Database ER diagram ](https://github.com/user-attachments/assets/31da0771-93be-42cb-91b4-1c167e2d3e01)
*The process of data collection can be further explored in [this repository](https://github.com/miguswong/IronmanScraper)*

<!-- TOC --><a name="executive-summary"></a>
## Executive Summary
* Ironman participation continues to recover from pre-pandemic levels in European and North American locations. However, **Asia** has already reached pre-pandemic levels of participants and was the only continent to have consistently positive increase in participants since 2021. 
* Competing in Ironman competitions is at an all-time high for younger age groups. Both **18-24** and **25-29** age groups had more participants in 2024 compared to any year previously; including 2014 when Ironman was at the height of its popularity.
<!-- TOC --><a name="insights-deep-dive"></a>

## Insights Deep-Dive
<!-- TOC --><a name="shifts-in-the-global-market"></a>
### Shifts in the Global Market
Ironman races reached peak participant saturation around 2014 and saw steady participant numbers (which could be indicative that there was larger demand to participate in these races than there were spots available). However, with the COVID-19 Pandemic in 2020, a majority of races were shut down and deferred to later. Participants and races did not rebound until 2022 which saw a sharp increase in the number of races but participants remained lower than pre-pandemic levels. The most likely explanation here is that the effects of COVID-19 were still being felt; races that were supposed to happen in 2020 happened later in 2021 or 2022 and there were a significant portion of customers who opted for a ticket refund rather than a [deferred entry](https://www.ironman.com/covid-options-north-america) into their Ironman Race. 

2023 was the first year that operations were somewhat returned to "normalcy" and deferred races have occurred. Total participants have not yet recovered back to previous levels but there are indications that triathlon racing is returning to its original popularity. 
![](https://github.com/user-attachments/assets/21bcef7c-cae0-49fb-afc1-d6321a8f72fe)

While the total number of Ironman Races offerings have decreased, Europe saw the largest decrease in race offerings decreasing from 18 races in 2023 to just 14 this year. Despite this, there are no signs that Ironman is struggling to sell entries as for the number of races offered considering that the total number of participants in Ironman 2024 was nearly 5% *increase* from the previous year. This is reflected by the sharp increase of participants per race for Europe in the graph below.

![](https://github.com/user-attachments/assets/9eb5abc5-5aff-4419-847a-44980025ce4f)

![](https://github.com/user-attachments/assets/faf3318d-59f4-479b-82c9-d0336cc8c76a)

![](https://github.com/user-attachments/assets/05ad46be-bf2a-47e0-986f-3ed43ee4ae6a)


While Europe and North America have continued to dominate a large portion of Ironman Races in series, they are still nowhere near pre-pandemic levels. This is not the same story for **Asia** which could be seen as a quickly growing market. Despite having little to no change in the total number of offered races (from 7 to 8 races per year for the past 10 decade), Asia not only recovered but surpassed total participant levels even prior to Ironman's 2014 peak. This is likely a result of a quickly growing [middle-class](https://www.futuresplatform.com/blog/asia-growing-middle-class-reshaping-global-consumption#:~:text=Based%20on%20Pew's%20income%20classification,of%20the%20entire%20Chinese%20population.) who have more expendable assets to participate in these types of athleisure events. 


| Year | Continent     | Total Races | Participant Count | % Change in Participants |
|------|---------------|-------------|-------------------|--------------------------|
| 2022 | Asia Pacific  | 7           | 5191              |                          |
| 2023 | Asia Pacific  | 8           | 6739              | 29.82%                   |
| 2024 | Asia Pacific  | 8           | 7467              | 10.80%                   |
|------|---------------|-------------|-------------------|--------------------------|
| 2022 | Europe        | 24          | 34383             |                          |
| 2023 | Europe        | 18          | 26456             | -23.05%                  |
| 2024 | Europe        | 14          | 27946             | 5.63%                    |
|------|---------------|-------------|-------------------|--------------------------|
| 2022 | North America | 15          | 23885             |                          |
| 2023 | North America | 11          | 17324             | -27.47%                  |
| 2024 | North America | 10          | 17609             | 1.65%                    |


![](https://github.com/user-attachments/assets/733f21ce-5a21-4814-a4ad-a49f4ca0b54c)

<!-- TOC --><a name="changes-in-age-demographic-customers"></a>
### Changes in Age Demographic Customers
Competing in Ironman competitions is at an all-time high for younger age groups. Both 18-24 and 25-29 age groups had more participants in 2024 compared to any year previously; including 2014 when Ironman was at the height of its popularity - on the basis of participants. What has been generally (and really still is) a field dominated by athletes 30+, there appears to be a shift to younger generations investing their time and resources towards endurance events such as Ironman.
![](https://github.com/user-attachments/assets/b4a070a0-8cd2-4fc2-a85b-cfc4f9449c48)

| Year | Division | Count | Change |
|------|----------|-------|--------|
| 2024 | M18-24   | 2107  | 54.4%  |
| 2024 | M80-84   | 15    | 36.4%  |
| 2024 | M25-29   | 4559  | 28.3%  |
| 2024 | M70-74   | 212   | 18.4%  |
| 2024 | M30-34   | 6159  | 11.7%  |
| 2024 | M60-64   | 2037  | 9.8%   |
| 2024 | M65-69   | 644   | 8.1%   |
| 2024 | M55-59   | 3912  | 2.7%   |
| 2024 | M35-39   | 6264  | 1.3%   |
| 2024 | M50-54   | 6410  | -2.6%  |
| 2024 | M40-44   | 7084  | -3.3%  |
| 2024 | M45-49   | 6451  | -6.0%  |
| 2024 | M75-79   | 43    | -8.5%  |


<!-- TOC --><a name="recommendations"></a>
## Recommendations
* **Make Ironman races more accessible to younger generations:** Younger generations show a growing interest in participating in Ironman races, particularly the 18-25 age group. While other age groups are seeing a decline, this demographic is expanding. However, the [high cost](https://www.triathlonish.com/p/how-much-does-it-cost-to-do-an-ironman) of participation, with registration fees around $1,000, can be a significant barrier for these young athletes. This financial hurdle may deter many from participating despite their interest.
* **Host more Events in Asia:** Asian Markets show strong potential for continued increases in participation and should be a larger focus going forward. Being able to host more opportunites in Asia not only will bring exposure to the race itself, but could also be seen as an attractive offering for athletes looking for a "vacation race" destination. Especially those from Europe and North America.

<!-- TOC --><a name="clarifying-questions-assumptions-and-caveats"></a>
## Clarifying Questions, Assumptions, and Caveats
* Official Results from the Ironman Website were not used in this analysis. Instead, a proxy website was scraped to obtain all the triathalon results ([here](https://www.coachcox.co.uk/imstats/race/185/results/)).