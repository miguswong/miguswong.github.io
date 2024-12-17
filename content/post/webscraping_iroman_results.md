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
# Introduction
Ironman race results data was scraped from a [third-party website](https://www.coachcox.co.uk/imstats/) for the purpose of EDA. All the data and code used for extracting results data can be found in the following links:

**GitHub Repository** [here](https://github.com/miguswong/IronmanScraper)\
**Kaggle Dataset** [here](https://www.kaggle.com/datasets/miguswong/ironman-140-6-results-dataset-2002-2024)

![Ironman Triathalon Logo](/images/ironmanlogo.png)

# Overview
The following files (mainly the Jupyter notebook and Python script) were used to scrape 140.6 Ironman race results ranging from 2002 to 2024 (as of 12-05-2024). Note,  the data was not scraped from the official Ironman website, but a [proxy-website](https://www.coachcox.co.uk/imstats/) not owned by Ironman. 

The notebook and scripts were designed in a way that generated 3 CSVs that follow the format of a standard relational database and can be joined together utilizing various IDs and could be readily uploaded to a SQL database.

## How to run
Web scraping begins in [*IronMan Scraping (Scrape Only).ipynb*](https://github.com/miguswong/IronmanScraper/blob/main/IronMan%20Scraping%20(Scrape%20Only).ipynb). All cells should be run in order from top to bottom and should result in series and race data being generated. 

### The case for parallel processing
Individual race results data is dynamically loaded onto the webpage meaning that BeautifulSoup4, which was used to scrape other information from the website, cannot be used here. Instead, [Selenium](https://selenium-python.readthedocs.io/) allows for automated browser testing (and in this scenario, actual data loading). The main caveat here is that the process of dynamically loading result data and launching a physical browser onto the computer is not only slow but *painfully slow* testing showed that on average, Selenium was able to process ~12 rows of data per second and with over 1,000,000 rows of data, this process would have taken around 25 hours to complete furthermore, utilizing the notebook to scrape results data meant that at any point if the script failed, the cell would have to be restarted which could be problematic especially with these long processing times.

Instead, a Python script utilizing the [*subprocess*](https://docs.python.org/3/library/subprocess.html) package was utilized to launch multiple browsers and scrape races simultaneously. There are 2 .py files *master.py* and *worker.py*. 

* **Master.py** functions as the coordinator of web scraping and launches the instances of *worker.py*. Depending on the number of subprocesses requested, the script will partition the work equally (based on the number of races, not the number of rows to scrape) and kick off instances of *worker.py*. In the event that there are races that have already been scraped and a CSV file has already been generated, *master.py* will skip these races and removed them from consideration for scraping.

*  **Worker.py** is the script that actually handles browser launching, web scraping, and file generation. The script is passed index information from *Master.py* for what races the script will be responsible for and iterates through the list. There are instances in which Selenium may unexpectedly fail to scrape web pages and the worker instance may immediately exit. In these scenarios, master.py was rerun.

Below is an example of how the script can be used along with how to specify how many worker (in this case, 8) instances you want: 
````
python master.py --num_workers 8
````
Note, that increasing the number of workers does not necessarily linearly increase web scraping performance. There are diminishing returns for launching more browsers simultaneously, as around 10 workers dropped individual worker performance down to ~5 rows/second. Worker scripts will generate CSV files and place them in the following file path: "./IronManData/raceResultsData/". The Python notebook contains code to combine all these CSVs and place them in the same file path as the races and series data. 

````Python
#After each individual csv data has been created, they need to be combined into a single csv as our "master" csv

# Directory containing the CSV files
directory = './IronManData/raceResultsData'

# Initialize an empty list to store individual DataFrames
data_frames = []

# Iterate through all CSV files in the directory
for filename in os.listdir(directory):
    if filename.endswith('.csv'):
        file_path = os.path.join(directory, filename)
        # Read the CSV file
        df = pd.read_csv(file_path)
        # Append the DataFrame to the list
        data_frames.append(df)

# Concatenate all DataFrames in the list
combined_df = pd.concat(data_frames, ignore_index=True)

# Write the combined DataFrame to a new CSV file
combined_df.to_csv('./IronManData/sql/results.csv', index=False)

print("All CSV files combined successfully!")
````

## Resulting Dataset 
3 CSVs should be generated at this point and should contain all the relevant information about Ironman results from 2002-2024.

[**Series.csv**](https://www.kaggle.com/datasets/miguswong/ironman-140-6-results-dataset-2002-2024?select=series.csv)
| Column    | Description                    |
|-----------|--------------------------------|
| `id`      | Unique identifier for the series (Primary Key) |
| `location`| Location of the series         |
| `continent`| Continent where the series is held |
| `link`    | URL link to the series details |


[**Races.csv**](https://www.kaggle.com/datasets/miguswong/ironman-140-6-results-dataset-2002-2024?select=races.csv)
| Column           | Description                                |
|------------------|--------------------------------------------|
| `year`           | Year of the race                           |
| `link`           | URL link to the race details               |
| `totalkonaSlots` | Total Kona slots available                 |
| `maleKonaSlots`  | Kona slots available for males             |
| `femaleKonaSlots`| Kona slots available for females           |
| `male1st`        | Time of the first male finisher            |
| `female1st`      | Time of the first female finisher          |
| `finishers`      | Total number of finishers                  |
| `dnf`            | Number of Did Not Finish (DNF)             |
| `dq`             | Number of Disqualifications (DQ)           |
| `id`             | Unique identifier for the race (Primary Key)|
| `seriesID`       | Identifier for the series (Foreign Key)    |

[**Results.csv**](https://www.kaggle.com/datasets/miguswong/ironman-140-6-results-dataset-2002-2024?select=results.csv)
| Column          | Description                                |
|-----------------|--------------------------------------------|
| `bib`           | Bib number of the participant              |
| `name`          | Name of the participant                    |
| `athleteLink`   | URL link to the athlete's profile          |
| `country`       | Country of the participant                 |
| `gender`        | Gender of the participant                  |
| `division`      | Division category of the participant       |
| `divLink`       | URL link to the division details           |
| `divisionRank`  | Rank of the participant in their division  |
| `overallTime`   | Total time taken by the participant        |
| `overallRank`   | Overall rank of the participant            |
| `swimTime`      | Swim time of the participant               |
| `swimRank`      | Swim rank of the participant               |
| `bikeTime`      | Bike time of the participant               |
| `bikeRank`      | Bike rank of the participant               |
| `runTime`       | Run time of the participant                |
| `runRank`       | Run rank of the participant                |
| `finishStatus`  | Finish status of the participant           |
| `dnf`           | Did Not Finish status                      |
| `raceID`        | Identifier for the race (Foreign Key)      |
| `athleteID`     | Identifier for the athlete                 |
