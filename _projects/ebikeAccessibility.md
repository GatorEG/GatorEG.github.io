---
layout: post
title: \[e]Bike Share Toronto
description: Factors Affecting e-bike Availability Across Bike Share Toronto
---

Ethan Goldstein, Rishabh Surana, Caitlin Zaragosa  
Group 132 Final Project, Winter 2023  
ISYE 7406 - Data Mining and Statistical Learning  

**Note to readers:**
This analysis was conducted before Bike Share Toronto [modernized its pricing structure in April 2023](https://bikesharetoronto.com/news/recommended-pricing-changes-2023/) and may no longer repersent e-bike availablilty in the downtown core. 

## Abstract
This project evaluated various data mining models on their ability to predict e-bike availability in
Toronto’s downtown core, with an emphasis on classification methods and procedures for
addressing unbalanced datasets. Logistic Regression, LDA, KNN, Naive Bayes, Random Forest,
and Gradient Boosting models were generated and compared on accuracy and testing errors.
These models were built on an unbalanced, base data set and repeated once the distribution
frequency of response variables was harmonized using a Synthetic Minority
Oversampling TEchnique (SMOTE).  

KNN and Random Forest had the highest performance amongst the training and testing datasets.
By utilizing LASSO on a balanced dataset, station id, time of day, and weather conditions were
determined to be the most important variables for predicting bike availability. These results and
models may be used by Bike Share Toronto and other bike share systems to enhance service
planning to meet/predict customer demand.

## Introduction
The increased popularity of bike sharing in large cities made it challenging to find suitable
transportation options and the exact timing required. Toronto, the largest city in Canada, faced
this issue in its most densely populated neighborhoods. The city’s public bike sharing service
allowed citizens and tourists to navigate the city while reducing congestion and cutting down on
CO2 emissions.  

Bike Share Toronto (BST) offered 2 types of bicycles for rent: mechanical bikes and pedal-assist
e-bikes. According to BST's open data set, mechanical bikes accounted for 92.7% of all available
bikes, with 6,619 bikes total compared with e-bikes, which only accounted for 7.3% of all
available bikes for rent, with 524 bikes system-wide. This was much lower than the 15-20% of
e-bikes widely regarded to be organically redistributed and recharged throughout the
bike-sharing network (Toronto Parking Authority, 2022). Additionally, anecdotal evidence
suggested that e-bike rentals were difficult to find, especially in the downtown core of the city,

## Objective 
Our objective is to conduct data analysis to assess how neighborhood type (commercial or residential) and other demographic factors influence bicycle availability in the network.

By doing so, we aim to provide individuals with the necessary information to make a more informed decision about when to rent a bike based on their preferences and the neighborhood they are in.

## Data Preparation & Cleaning
Bike Share Toronto (BST) provides an open data feed that contains information on the status of the system and the availability of bikes at each station. This data will be integrated with public GIS data to group the stations into neighborhoods.  

To create our data catalog, we will gather data every 15 minutes for an entire week, focusing on stations located in 28 distinct neighborhoods in the downtown region.  

Since our hypothesis is based on the suspicion that commercial focused neighborhoods and residential neighborhoods have different needs, we will add a flag to denote the type of population that lives there.

### Supplementary Data
Station Information
- Additional GBFS feed containing coordinates and features of each bike docking station.
- GBFS = General Bikeshare Feed Specification, an open data standard.

Hourly Weather Records
- Data recorded at Billy Bishop Toronto City Airport (YTZ).
- Retrieved from Environment and Climate Change Canada's Historic Data repository.

Sunrise and Sunset Times
- Calculated using a standardized algorithm, considered accurate to ±2 minutes.
- Provided by the National Research Council Canada.

Toronto Neighborhoods Map
- Details the common names of Toronto's neighborhoods and their geographic boundaries.
- Croud-sourced, published through Google Maps.
- Chosen over official maps as the crowd-sourced version better reflects city life and human movement.

### Data Processing
Neighborhood Map joined on station coordinates
- Merged with the station information feed in QGIS, an open-source GIS application.
- Data filtered to Downtown neighborhoods.
- Bloor St to the north, the Don River to the east, Lake Ontario to the south, and Bathurst St to the west.


Weather Records were joined on datetime
Sunrise / Sunset Data joined on datetime
- 6 potential factors imported from the dataset
- 2 binary factors derived from the data

# Conclusions
LASSO, our variable selection algorithm, did not identify the neighborhood type or name as a strong parameter. The availability of mechanical bicycles was the sole variable selected under this model.

# Lessons Learned
**Data cleaning and preparation should not be underestimated**  
Significant time and effort was used to identify, source, and join different datasets. This time commitment must be carefully managed to ensure there is sufficient bandwidth to complete the core data mining and analysis tasks.

**Deep analysis may be limited by computational resources**  
While the project team hoped to include further analysis in variable tuning, the number of hyperparameters tested had to be scaled back due to the time it took to compute the models. Each additional hyperparameter (_h_) tested increases the computational effort required to generate models exponentially, which is further multiplied by the number of observations (_n_) and monte carlo runs (_m_, if applicable to the model used). This produces a computational performance of $O(mh^n)$, which can be extremely computationally expensive.  

**Modeling is an art and a science**  
Each algorithm and methodology discussed in this course is a tool which can be used in many different ways. There is no single best way of addressing an analytical question, each practitioner may take a different approach and each approach may return vastly different results.
