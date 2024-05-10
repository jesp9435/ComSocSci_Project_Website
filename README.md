By Jesper Lund, 214639 and Frederik Bæk, s214618

### We all know the iconic yellow taxicab from New York City. With more than 13,000 of these yellow taxis spread across five boroughs, we wanted to dwelve deeper into the underlying patters and trends within this taxi-network. More specifically, we wondered if the amount of precipitation has an effect on the tip recieved by the cap driver, as well as investigating from a textual analysis what factors could contribute to the patters in the data.

> #### The Dataset:  
> The dataset consisted of three main parts; Yellow Taxi Trip Records for the five boroughs of NYC, Weather Data, and Wikipedia Pages for each of the five boroughs. The Taxi data consisted of severel million rows of trip records with information about the pickup and dropoff locations as well as the tip amount. In the Weather data, we focused on the amount of precipitation and wanted to figure out which period had the most inconsistent weather. Finally, the Wikipedia pages contained information about and descriptions of the five different boroughs of NYC.
> The different datasets can be downloaded here:  
> - [**Taxi Data**](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)  
> - [**Weather Data**](https://www.wunderground.com/history/daily/us/ny/new-york-city/KLGA/date)  
> - **Wikipedia:***
>   - [Bronx](https://en.wikipedia.org/wiki/The_Bronx)
>   - [Brooklyn](https://en.wikipedia.org/wiki/Brooklyn)
>   - [Manhatten](https://en.wikipedia.org/wiki/Manhattan)
>   - [Queens](https://en.wikipedia.org/wiki/Queens)
>   - [Staten Island](https://en.wikipedia.org/wiki/Staten_Island)
> 
> *See the code in the Explainer notebook for all URLs
>
> When creating the network and adding edges, it is important to count the sum of the tips recorded between two taxi zones and average them based on the amount of trips. The reason for this is that the amount of trips recorded in 2013 vs 2017 on May 5th is not the same, so it is not comparable. Furthermore, the tips needs to be adjusted for inflation, in this project we made the tips in 2013 adjusted to inflation to 2017 (by 5%). In general, dictionaries have been used frequently to keep everything in a orderly matter so it is easy to work with, which is crucial since there are so much data that needs to be handled. 

After having scraped the wikipedia text, we had to apply some Natural Language Processing techniques to clean up the data before we could begin to analyse it. This consisted of removing punctuation and stopwords, and afterwards performing tokenization, which is the act of breaking a text into individual words or tokens, as well as lemmatization, reducing words to their base or dictionary form to normalize variations of words and improve analysis accuracy. We decided to manually remove certain stopwords, primarily proper names, as these would dominate the text for each borough.
  
The Taxi data was stored in parquet files, that we downloaded and then importet into a Pandas Dataframe in Python. Initially, we downloaded trip data from the last 10. Since each seperate dataframe had the same naming for the columns, we renamed the columns to include the year for each dataframe and then concatenated them into one dataframe with all years. The next step was to do some pre-processing on the data. Due to the sheer size of the dataset, with several million rows of data, we decided to only use a subpart of the total dataset to make computational tasks feasible. 

The taxi data from May 5th 2013 consists of roughly 490k trip records, whilst the taxi data from May 5th 2017 consists of roughly 363k trip records. 

The weather data is saved in a file called "transformed_data.json". It is a dictionary containing the years from 2013 to 2023, and each year contains the days in May 1-31, and each day has all recorded data on the given day. The amount of time stamps taken varies from day to day, but in total 9963 weather time stamps were taken between 2013 and 2023. Since we are limited to May 5th in 2013 and 2017, we will only use 84 of these weather time stamps. 

The following is the amount of words scraped from Wikipedia about the respective borough:
<br>
Bronx: 65493 
<br>
Brooklyn: 108013 
<br>
Manhattan: 191659 
<br>
Queens: 73886 
<br>
Staten Island: 43905 
<br>

> #### Analysis:  
> From working with the weather data, we found out that the two days with the most variety in precipitation was the 5th of May 2013 and 2017, where 2017 had the most rainfall and 2013 the least. The taxi data from May 5th 2013 consists of roughly 490k trip records, whilst the taxi data from May 5th 2017 consists of roughly 363k trip records. 

![Tip_amount](docs/assets/Combined.png)

![Degdist](docs/assets/Degdist.png)

![Histogram](docs/assets/Histogram.png)

![Wordcloud](docs/assets/Wordclouds.png)

### The network:  
Below are the two networks from the Taxi trip data, may 5th 2013 and 2017. 
![Network](docs/assets/Network.jpg)
