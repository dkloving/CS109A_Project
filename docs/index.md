---
title: Murder Rate Predictive Analysis
---
<img style="float: right;" src="img/police-line.jpg">


> **Created by Team 14:** *David Loving* \| *Ilan Dor* \| *Volodymyr Popil*

### Problem Statement and Motivation
Our goal was to figure out which features, drawn from the data available to us, were most predictive of murder rates. The motivation behind our goal rests in the simple fact that murder is and has always been a most tragic and detrimental part of society and people's lives. Therefore, if it is possible to find generic predictors (e.g., income, education level) of murder rates, doing so could help society learn where to focus efforts to reduce murders (e.g., establish a universal basic income program, provide free education).


### Introduction and Description of Data
Murder is a very tragic aspect of society but it is also a relatively (although not absolutely) rare occurrence. That is, while many people get murdered each year, most people die from causes other than murder. Solving this problem is important because murder is one of the worst crimes that plague humanity. Solving this problem is challenging due to the relative infrequency of murder makes it challenging to predict. Furthermore, while we will show that certain predictors tend to be more correlated with murder than others, murder is often a highly personal crime whose circumstances vary widely by instance.

To do this analysis, we needed two main datasets: one consisting of violent crimes (including murder rate) in each MSA (metropolitan statistical area) and another consisting of Census data about the same MSAs. The murder rates, by MSA and year, were scraped from the `ucr.fbi.gov` website (accounting for differences by year in website URL format and HTML table tags), Census data was downloaded from the `factfinder.census.gov` website and CSV files were imported into a Python script. There were numerous inconsistencies in data between years. For example, the number of features varies from year to year, as does the metadata, so we decided to fetch only 2010 (chosen arbitrarily) to perform our preliminary EDA. The subset of features was selected (excluding only some extremely redundant features) and renamed for better readability. 

After looking at a histogram which showed us a roughly normal-looking distribution of murder rates across the various MSAs with a mean of around 5 per 100,000 inhabitants, we moved our focus towards scatter plots of 190 features all taken against murder rate. From a careful visual analysis of these as well some common sense thought about forming a reasonable and varied set of predictors, we narrowed that large collection of features down to about 25. Repeating a similar analysis and scrutiny, we arrived at a selection of eight features to be used in our modeling.

For these eight features, we merged (on MSA name) the two datasets described above to create a dataset on the matching rows, only. The FBI and Census have different sets of MSAs, so we used the smaller set (Census) and most matched perfectly to the FBI data, while leaving some of the FBI data points unused. This approach seems appropriate as it is not possible to match certain FBI listed MSA's to Census data if those are not available.

We noticed that some MSAs had similar but different names across years. In every case where we believed the MSA to represent either mostly or exactly the same geographical area, we chose a single name for MSA to use across all years of data provided for it. For the sake of transparency, we have included in our merged dataset both the original MSA name ('MSA_orig') as well as the revised one ('MSA_corr'), so that you can see where and how MSA names were revised. Additionally, for technical convenience, we added a column named 'MSA_abbr' to contain a much shorter version of each MSA name in a contiguous and highly-consistent format. This was particularly helpful for one-hot encoding the MSAs. For example, here is the set of these names that applied for the Denver, CO MSA:

MSA_orig|MSA_corr|MSA_abbr|year
---|---|---|---
Denver-Aurora-Lakewood, CO|Denver-Aurora, CO|DENVER_CO|2016

<br><br>

MSA_orig|MSA_corr|MSA_abbr|year
---|---|---|---
Denver-Aurora, CO|Denver-Aurora, CO|DENVER_CO|2006
Denver-Aurora, CO|Denver-Aurora, CO|DENVER_CO|2007
Denver-Aurora-Broomfield, CO|Denver-Aurora, CO|DENVER_CO|2009
Denver-Aurora-Broomfield, CO|Denver-Aurora, CO|DENVER_CO|2010
Denver-Aurora-Broomfield, CO|Denver-Aurora, CO|DENVER_CO|2011
Denver-Aurora-Lakewood, CO|Denver-Aurora, CO|DENVER_CO|2013
Denver-Aurora-Lakewood, CO|Denver-Aurora, CO|DENVER_CO|2014
Denver-Aurora-Lakewood, CO|Denver-Aurora, CO|DENVER_CO|2015
Denver-Aurora-Lakewood, CO|Denver-Aurora, CO|DENVER_CO|2016




> Note: assumption is that involuntary manslaughter is equvalent to murder and so considered as one combined datapoint

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
