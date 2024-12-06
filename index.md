# Predicting with Power Outage Dataset
## by Hae In Lee

### What are we predicting? We can essentially predict anything we want to know about this dataset ! 

### For this project, I am curious 
## if we can predict the number of people affected by the power outage by seeing the cause of the outage and duration of the outage

---

# Introduction
## Let's first see what this dataset is about
This dataset comes from Purdue University's LASCI Research Data on Power Outages and focuses on Major Power Outage Risks in the U.S. This comprehensive dataset documents power outages across various states in the continental United States. It provides information on the geographical locations of these events, regional climate data, land-use patterns, electricity consumption trends, and the economic characteristics of the states impacted by these outages. 

This dataset shows the importance of examining power outages that can have economic, social, and enfironmental impacts. Also, observing this dataset can improve the way we respond and plan for natural disasters.

In total, there are 1534 rows and 55 columns (variables). 
However, to answew our question, we can just use a couple of the columns.

### This chart shows the columns for analysis

| Columns from Power Outage Dataset     | Description    |
| ------------------------------------- | -------------- |
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
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))

---

<iframe
  src="assets/file-name.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

###
