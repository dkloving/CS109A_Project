---
title: Murder Rate Predictive Analysis - Team 14 
---
<img style="float: right;" src="img/police-line.jpg">

> **Created by:** *David Loving* \| *Ilan Dor* \| *Volodymyr Popil*


### Problem Statement and Motivation

Our goal was to figure out which features, drawn from the data available to us, were most predictive of murder rates. The motivation behind our goal rests in the simple fact that murder is and has always been a most tragic and detrimental part of society and people's lives. Therefore, if it is possible to find generic predictors (e.g., income, education level) of murder rates, doing so could help society learn where to focus efforts to reduce murders (e.g., establish a universal basic income program, provide free education).


### Introduction and Description of Data

Murder is a very tragic aspect of society but it is also a relatively (although not absolutely) rare occurrence. That is, while many people get murdered each year, most people die from causes other than murder. Solving this problem is important because murder is one of the worst crimes that plague humanity. Solving this problem is challenging due to the relative infrequency of murder makes it challenging to predict. Furthermore, while we will show that certain predictors tend to be more correlated with murder than others, murder is often a highly personal crime whose circumstances vary widely by instance.  


To do this analysis we needed two main dataset, one about crimes recorded to retrieve the murder rates in each MSA and another on the Census data about population in these MSA areas. The murder rates were scraped from `ucr.fbi.gov` website by MSA (accounting for different year website URL format and HTML table tags), and Census data was downloaded from `factfinder.census.gov` website and CSV files imported into Python. There were numerous inconsistencies in data between years. For example the number of features varied from year to year, as did the metadata, so we decided to fetch only 2010 (chosen arbitrarily) to perform EDA first. Subset of features was selected and renamed for better readability. Once EDA is completed and final eight features were chosen for further modeling, data for those features was pulled for each year and combined into one dataset. Two datasets (murder rates and Census data) were merged on the MSA name, and only matching rows were considered for analysis

Note: assumption is that involuntary manslaughter is equvalent to murder

### Literature Review / Related Work

We took our moving average approach from the Wikipedia page for that topic: 

https://en.wikipedia.org/wiki/Moving_average

It mentioned that "in science and engineering the mean is normally taken from an equal number of data on either side of a central value. This ensures that variations in the mean are aligned with the variations in the data rather than being shifted in time." Therefore, this is the approach that we used in our temporal modeling.

### Modeling Approach and Project Trajectory

*Todo*

### Results, Conclusions, and Future Work

*Todo*


<br><br><br>
![png](img/report_requirements.png)