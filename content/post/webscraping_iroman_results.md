+++
title = 'Webscraping Ironman Triathalon Results'
draft = false
date = 2024-12-12T14:48:13-06:00
tags = [
    "Personal Projects",
    "Python",
    "Webscraping",
    "Sports"
]
thumbnail = "images/ironmanlogo.png"

+++

# Overview
Ironman race results data was scraped from a [third-party website](https://www.coachcox.co.uk/imstats/) for the purpose of EDA. All the data and code used for extracting results data can be found in the following links:

**GitHub Repository** [here](https://github.com/miguswong/IronmanScraper)\
**Kaggle Dataset** [here](https://www.kaggle.com/datasets/miguswong/ironman-140-6-results-dataset-2002-2024)

# Methodology
Web scraping was accomplished mainly through 2 packages within Python:

* [BeautifulSoup4](https://beautiful-soup-4.readthedocs.io/en/latest/) for statically loaded content.
* [Selenium](https://www.selenium.dev/) for dynamic content.
