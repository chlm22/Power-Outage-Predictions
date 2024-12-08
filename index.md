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
  height="800"
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
 Now that we are acquainted with our dataset thanks to our initial question, "Which cause category is most responsible for power outages in different states?" 

 ### Prediction question
"Can we predict the number of customers affected based on the cause and duration of the outage?"
- This question is a **regression** prediction problem.


# Baseline Model
Because my prediction problem is a regression problem, I started with using a linear regression base model with Mean Absolute Error, Root Mean Squared Error, and R-squared metrics. Linear Regression assumes a linear relationship between the features and the target and the metrics gives model’s predictive performance and its ability to explain the variance in the target variable.

### Target Variable: 'CUSTOMERS.AFFECTED'
### Two Features: 
1. **CAUSE.CATEGORY** (Nominal feature) 
2. **OUTAGE.DURATION** (Quantitative feature) 

**Note:**
- There are total of 1534 rows to work with however, I will be dropping the NaN values from the 3 columns I am working with, 'CUSTOMERS.AFFECTED', 'OUTAGE.DURATION', 'CAUSE.CATEGORY'
- I will be dropping the rows because do not know what the right answers to these NaN values of the columns will be. Also, we are trying to predict the 'CUSTOMERS.AFFECTED'; therefore, there is no point in imputing the NaN values. Trying to impute the NaN rows will just lead us to inaccurate and misleading predictions. 
- Also, the NaN values of 'OUTAGE.DURATION' will also be dropped and not imputed because a lot of those data simply do not have any information across all columns to draw imputations from, meaning, that those rows were purposely not filled out by the dataset creators. 
- I will be working with a total of 1052 rows of data 
- I have set my code to train on 80% of the rows (844 rows) and test on 20% of the rows (212rows)

### Baseline Model Metric Results: 
- **Mean Absolute Error (MAE): 129084.54289691892**
- **Root Mean Squared Error (RMSE): 302647.37444542814**
- **R-squared (R^2): 0.13119692403417982**

These performance results are **BAD**. 
Mean Absolute Error shows that the predictions are off by about 129,084 customers. This is a significant amount, suggesting that the model isn't providing accurate predictions.

Root Mean Squared Error  shows the model is making large errors in some cases.

R-squared shows that the model explains only about 13.1% of the variance in the target variable, which is quite low, suggesting that the model is not capturing much of the underlying patterns in the data and is not very predictive.

Some of the reaons why I think the results turned out so poorly is that maybe the variables have weak correlations and they may have non-linear relationships. 

---


# Final Model 
Since my results from my baseline model was so poor, I decided to make my own columns using the given data to make a stronger and effective impact. 

### Newly Added Features
1. The first feature I created was **'OUTAGE_SEVERITY'** = 'OUTAGE.DURATION' * 'CUSTOMERS.AFFECTED' 
- I thought this was an important feature to add since it covers and combines both the duration of the outage time and how many people it affected 
- These two factors are crucial to predicting the total impact of an outage

2. The second feature I created was **'POP_DENSITY'** = ('POPDEN_URBAN' + 'POPDEN_RURAL' + 'POPDEN_UC') / 3
- I thought this was an important feature to add since it helps model how the location and concentration of people affects the number of customers impacted


### Modeling Algorithm
- **Random Forest Regression!**
- According to my Baseline Model result, it showed that the target and feature variables seemed to have non-linear relationships
- Random forest is one of the algorithms that can capture non-linear relationships
- Random forest works with both numerical and categorical features
- Less likely to overfit or underfit when there are multiple trees -> less noise
- Works well with GridSearchCV -> optimize hyperparameters
- According to **GeeksforGeeks** "Hyperparameter tuning is the process of selecting the optimal values for a machine learning model’s hyperparameters."


### Hyperparameter, Best Parameter, GridSearchCV
**n_estimators = [50, 100, 200]:**
- Testing multiple values of n_estimators helps find the optimal number of trees 
- 50 trees - Faster training and less computationally expensive
- 100 trees - Default starting point and provides a good balance for most use cases (according to Google)
- 200 trees - More accurate but computationally expensive. More trees usually make the model more robust, as the model has more trees to get predictions from

**max_depth = [100, 10, 20]:** 
- three different maximum depths for the trees to see which tree depth strikes the right balance
- 100 means trees can grow 100 levels deep -> detailed patterns and interactions between features, risks overfitting 
- 10 means it captures general patterns up to maximum depth of 10, which is relatively shallow. Risks underfitting 
- 20 means a tree with a maximum depth of 20. This helps it not overfit like depth 100 but not underfit like depth 10

**max_features: sqrt** 
- Using the square root of the number of features lead to a good model performance
- Helps to reduce overfitting


# Final Model Metric Results: 
- **Mean Absolute Error (MAE): 63804.31157813248**
- **Root Mean Squared Error (RMSE): 174916.45915436902**
- **R-squared (R^2): 0.7097923321184068**

<iframe
  src="assets/comparison_side_by_side.html"
  width="1400"
  height="700"
  frameborder="0"
></iframe>
These graphs compare the metric results of Baseline and Final Models.

# Conclusion
Based on the final evaluation metrics, there was a huge improvement from the baseline model evaluation metrics. This means that the final model can reasonably predict the number of customers affected by an outage, but it is not perfect. The R^2 score suggests a good fit, but, as always, there is obviously room for improvement. The next steps would require exploring and finding different ways of reducting the large prediction errors, shown by the high value of Root Mean Squared Error. 

