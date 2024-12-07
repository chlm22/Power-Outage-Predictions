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

# Dataset Cleaning & Analysis
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
  width="1000"
  height="700"
  frameborder="0"
></iframe>
This bar chart visualizes the distribution of power outage causes by category, showing the number of outages for each cause. 
- The x-axis represents the cause categories of power outages
- the y-axis represents the count of outages within each category, providing a direct comparison of how often each cause contributes to power outages


<iframe
  src="assets/mapOfCustomersAffectedbyState.html"
  width="1500"
  height="700"
  frameborder="0"
></iframe>
This map shows how power outages, in terms of customers affected, are distributed across the U.S. states. It identifies regions where the most significant disruptions occur (e.g., high-impact states are shaded darker).


## Bivariant Analysis
- Refers to the analysis of the relationship between two variables. 
- Determines if one variable can predict or explain the behavior of another variable.

<iframe
  src="assets/customersAffectedByYearCauseCategory-Barchart.html"
  width="1300"
  height="800"
  frameborder="0"
></iframe>
This bar chart shows how changes in the cause of outages (across years) influence the total number of customers affected. Each bar represents a year, with the different cause categories (e.g., Weather, Human Error, Equipment Failure) stacked next to each other to show the proportion of customers affected by each cause.
- The x-axis represents Years
- The y-axis represents the total number of customers affected by outages

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

| U.S._STATE   |   equipment failure |   fuel supply emergency |   intentional attack |   islanding |   public appeal |   severe weather |   system operability disruption |
|:-------------|--------------------:|------------------------:|---------------------:|------------:|----------------:|-----------------:|--------------------------------:|
| AK           |     14273           |                     nan |                  nan |         nan |             nan |    nan           |                   nan           |
| AL           |       nan           |                     nan |                    0 |         nan |             nan | 471644           |                   nan           |
| AR           |         0           |                     nan |                 9200 |           0 |           54094 | 556466           |                   nan           |
| AZ           |    167000           |                     nan |                 2713 |         nan |             nan | 180911           |                229000           |
| CA           |         1.39026e+06 |                       0 |               127920 |      131019 |               0 |      2.05794e+07 |                     3.34489e+06 |


## Imputation & Missing Values
 I did not conduct any imputation on the missing values since the 'NaN' values represent missing data in the dataset, which could be due to various reasons like no reported outages for specific causes, irrelevance of certain causes for particular states, or gaps in the data collection process. However, having said that, either filling them with zeros or mean or median values could be valid depending on different analysis needs and goals.

 ---

 # Prediction Problem 
 -- Finally 
 ## Now that we are acquainted with our dataset thanks to our initial question, 
 ## "Which cause category is most responsible for power outages in different states?" 

 ## Our real prediction question: 
 ## **"Can we predict the number of customers affected based on the cause and duration of the outage?"**
This question is a **regression** prediction problem.


# Baseline Model
Because my prediction problem is a regression problem, I will start with using a linear regression base model with MAE, RMSE, and R^2 metrics. 

**Target Variable: 'CUSTOMERS.AFFECTED'**
### Two Features : **CAUSE.CATEGORY** - Nominal feature and **OUTAGE.DURATION** - Quantitative feature 


- There are total of 1534 rows to work with
- There are 443 NaN values for 'CUSTOMERS.AFFECTED'
- There are 58 NaN values for 'OUTAGE,DURATION'
- There are 0 NaN values for 'CAUSE.CATEGORY'

- I will be dropping a total for 501 rows from this dataset since we do not know what
the right answers to these NaN values of the columns will be. Also, we are trying to predict the 'CUSTOMERS.AFFECTED'; therefore, there is no point in imputing the NaN values. Trying to impute the 443 rows of 'CUSTOMERS.AFFECTED' will just lead us to inaccurate and misleading predictions. 

- Also, the 58 NaN values of 'OUTAGE.DURATION' will also be dropped and NOT imputed because a lot of those data simply do not have any information across all columns to draw imputations from, meaning, that those rows were purposely not filled out by the dataset creators. 

After running the linear regression model with pipeline preprocessing steps and fitting the LinearRegression() model, the results I got were:

**Mean Absolute Error (MAE): 111903.32126078878**
**Root Mean Squared Error (RMSE): 230339.58903807346**
**R-squared (R²): 0.10278075225620387**



# Final Model