# Predicting with Power Outage Dataset
## by Hae In Lee

### What are we predicting? We can essentially predict anything we want to know about this dataset ! 
## Before we dive into predicting anything, let's try to familiarize ourselves with the dataset using the following question:
- Which cause category is most responsible for power outages in different states?

---

# Introduction
## What is this dataset about? 
This dataset comes from Purdue University's LASCI Research Data on Power Outages in the US, by state, from January 2000 to July 2016. It provides information on the geographical locations of these events, regional climate data, land-use patterns, electricity consumption trends, and the economic characteristics of the states impacted by these outages. 

## Why is this dataset even worth looking at? And how does it help answer our question?
 The dataset is important for identifying trends in power outages and could help improve strategies for preventing and mitigating future disruptions.

This question helps understand the causes of power outages can help states and utility companies make effective choices when power outages occur. They can focus on improving infrastructure in areas most affected by specific causes like strengthening power grids in regions prone to weather-related outages. They can create a comprehensive emergency response planning, since different situations may require different strategies. They can also plan resource allocation by helping states identify which outages are likely to have the most significant impact on the population.

## General overview of the dataset
In total, there are 1534 rows and 55 columns (variables). 
For our analysis purposes, we will only be looking at a couple of the variables

---

### This chart shows the columns for analysis

| Columns from Power Outage Dataset     | Description    |
| ------------------------------------- | -------------- |
| **YEAR**                              | Indicates the year when the outage event occurred |
| **U.S._STATE**                        | Represents all the states in the continental U.S. |
| **CAUSE.CATEGORY**                    | Categories of all the events causing the major power outages |
| **OUTAGE.DURATION**                   | Duration of outage events (in minutes) |
| **CUSTOMERS.AFFECTED**                | Number of customers affected by the power outage event |
| **TOTAL.CUSTOMERS**                   | Annual number of total customers served in the U.S. state |
| **POPULATION**                        | Population in the U.S. state in a year |


---

# Dataset Cleaning 
To use the data from the columns, we first need to clean them up.

First, I dropped all the columns I will not be using for the analysis. 
I kept only seven columns, YEAR, U.S._STATE, OUTAGE.DURATION, CAUSE.CATEGORY, CUSTOMERS.AFFECTED, TOTAL.CUSTOMERS, POPULATION


|   YEAR | U.S._STATE   |   OUTAGE.DURATION | CAUSE.CATEGORY     |   CUSTOMERS.AFFECTED |   TOTAL.CUSTOMERS |   POPULATION |
|-------:|:-------------|------------------:|:-------------------|---------------------:|------------------:|-------------:|
|   2011 | Minnesota    |              3060 | severe weather     |                70000 |       2.5957e+06  |  5.34812e+06 |
|   2014 | Minnesota    |                 1 | intentional attack |                  nan |       2.64074e+06 |  5.45712e+06 |
|   2010 | Minnesota    |              3000 | severe weather     |                70000 |       2.5869e+06  |  5.3109e+06  |
|   2012 | Minnesota    |              2550 | severe weather     |                68200 |       2.60681e+06 |  5.38044e+06 |
|   2015 | Minnesota    |              1740 | severe weather     |               250000 |       2.67353e+06 |  5.48959e+06 |


---

## Univariant Analysis
- Refers to the analysis of one variable
- Focuses on  describing and summarizing the data. 
- Helps understand the distribution, central tendency, variability, and shape of the data

<iframe
  src="assets/causecatBarchart.html"
  width="900"
  height="700"
  frameborder="0"
></iframe>
This plot provides insights into the distribution of power outages by cause, which is an important step toward understanding how different factors might influence the number of customers affected. By examining this relationship alongside the duration of outages, it can help predict the impact of outages on customers.

<iframe
  src="assets/mapOfCustomersAffectedbyState.html"
  width="1700"
  height="700"
  frameborder="0"
></iframe>
This map allows users to visually assess which U.S. states experience the highest number of customers affected by power outages. While this map does not directly show the cause or duration of the outage, it provides a useful overview that can guide further investigation into those factors, especially in states with high outage counts.


## Bivariant Analysis
- Refers to the analysis of the relationship between two variables. 
- Determines if one variable can predict or explain the behavior of another variable.

<iframe
  src="assets/customersAffectedByYearCauseCategory-Barchart.html"
  width="1800"
  height="1000"
  frameborder="0"
></iframe>
This bivariate visualization is key to understanding how cause categories (like weather) and year correlate with the number of customers affected. The chart provides valuable context for predicting the impact of future outages and suggests that weather will likely continue to be a major factor in large-scale outages. The fluctuation in customer impact from human error and equipment failure might also help refine predictions, but the dominance of weather suggests that weather data could be a key predictor of customer impact.

## Interesting Aggregates
### Remember our initial question : Which cause category is most responsible for power outages in different states?
To help us answer this after seeing the visualizations of our data, I thought it would be helpful to group 'CAUSE.CATEGORY' and 'U.S._STATES' columns, sum the 'CUSTOMERS.AFFECTED,' to see how many customers were affected by outages in each state, broken down by the cause of the outage.

| CAUSE.CATEGORY    | U.S._STATE   |   CUSTOMERS.AFFECTED |
|:------------------|:-------------|---------------------:|
| equipment failure | AK           |      14273           |
| equipment failure | AR           |          0           |
| equipment failure | AZ           |     167000           |
| equipment failure | CA           |          1.39026e+06 |
| equipment failure | DE           |      18400           |


Then, I pivoted the table to better analyze the relationship between the cause categories (e.g., Weather, Human Error, Equipment Failure) and the U.S. states, showing how each cause affects the number of customers in each state.


|   equipment failure |   fuel supply emergency |   intentional attack |   islanding |   public | U.S._STATE   |   equipment failure |   fuel supply emergency |   intentional attack |   islanding |   public appeal |   severe weather |   system operability disruption |
|:-------------|--------------------:|------------------------:|---------------------:|------------:|----------------:|-----------------:|--------------------------------:|
| AK           |     14273           |                     nan |                  nan |         nan |             nan |    nan           |                   nan           |
| AL           |       nan           |                     nan |                    0 |         nan |             nan | 471644           |                   nan           |
| AR           |         0           |                     nan |                 9200 |           0 |           54094 | 556466           |                   nan           |
| AZ           |    167000           |                     nan |                 2713 |         nan |             nan | 180911           |                229000           |
| CA           |         1.39026e+06 |                       0 |               127920 |      131019 |               0 |      2.05794e+07 |                     3.34489e+06 |