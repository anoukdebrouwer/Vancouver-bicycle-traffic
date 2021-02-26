# Bicycle-counts
Personal data science project in Python visualizing and predicting bicycle counts in Vancouver, BC.

The City of Vancouver has bike counters along popular bike routes at 19 different locations in the city. The goal of this project is to predict bicycle counts using weather data and information about the day. 

<img src="https://payload.cargocollective.com/1/2/77118/4991800/2013-02-16%2017.39.02_o.jpg" width="600">

## Summary

The **bicycle count data** was obtained from the [City of Vancouver website](https://vancouver.ca/streets-transportation/how-we-collect-bike-volumes.aspx). Daily counts are available from August 1st, 2018. Of the 19 counters, the Burrard at Cornwall counter gets the most traffic, with on average about 4000 bicycles per day. I used this as the target variable.

<img src="/Bike-counts_2019_Burrard-at-Cornwall.png" width="600">

The **weather data** can be downloaded from the [Government of Canada climate website](https://climate.weather.gc.ca/historical_data/search_historic_data_e.html). I chose to use the data from the Vancouver Airport weather station, because the data from the Vancouver Harbour weather station (closer to the city) had a lot of missing values. The dataset contains daily information about temperature (mean, min and max), precipitation (total rain, total snow, total precipitation, and snow on the ground), and wind (speed and direction of maximum gust). 

<img src="/Temperature_2019.png" width="380"> <img src="/Precipitation_2019.png" width="375">

Because the bicycle count data is available from August 1st 2018, and the data from mid March 2020 might be affected by people working from home during the COVID-19 pandemic, I chose to use the 2019 data as the **training set**, and the 2020 data up to March 15th as the **test set**. Since the training set is small, I don't expect any of the models to perform excellently.

I added several **features** to the training set: variables with the month, day of the month, day of the week,  a variable indicating whether it was a BC statutory holiday, as well as binary variables indicating whether there was any precipitation or snow on the ground on a given day (random forest model only). 

As a baseline model, I fitted a **linear regression model**. The mean absolute error for the predicted values in the test set was 482 bikes per day. 

I then fitted a **random forest regression model** to the data, determining the optimal tree depth using cross-validation. This model performed slightly better, with a mean absolute error of 407 bikes per day for the test set. The daily temperature (specifically the maximum daily temperature) turned out to be the single most important predictor of the bike counts.


## Contents

### Notebooks

* 01_Data-preparation - load and combine bicycle count data and weather data
* 02_Data-exploration - create a train and test set, add features for modelling, and visualize the data
* 03_Data-modelling - set up a processing pipeline and fit linear regression and random forest regression models

### Data files

* Bicycle-volume-data.xlsx - raw bicycle count data downloaded from the [City of Vancouver website](https://vancouver.ca/streets-transportation/how-we-collect-bike-volumes.aspx). 

* Climate-daily_VancouverAP-2018.csv, Climate-daily_VancouverAP-2019.csv, Climate-daily_VancouverAP-2020.csv - raw weather data downloaded from the [Government of Canada climate website](https://climate.weather.gc.ca/historical_data/search_historic_data_e.html)

* raw.csv - combined bicycle count and weather data

* train.csv and test.csv - train and test set
