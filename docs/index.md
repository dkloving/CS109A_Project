---
title: Murder Rate Predictive Analysis
---
<img style="float: right;" src="img/police-line.jpg">



> **Created by Team 14:** *David Loving* \| *Ilan Dor* \| *Volodymyr Popil*


### Problem Statement and Motivation
Our goal was to figure out which features, drawn from the data available to us, were most predictive of murder rates. The motivation behind our goal rests in the simple fact that murder is and has always been a most tragic and detrimental part of society and people's lives. Therefore, if it is possible to find generic predictors (e.g., income, education level) of murder rates, doing so could help society learn where to focus efforts to reduce murders (e.g., establish a universal basic income program, provide free education).


### Introduction and Description of Data
Murder is a very tragic aspect of society but it is also a relatively (although not absolutely) rare occurrence. That is, while many people get murdered each year, most people die from causes other than murder. Solving this problem is important because murder is one of the worst crimes that plague humanity. Solving this problem is challenging due to the relative infrequency of murder makes it challenging to predict. Furthermore, while we will show that certain predictors tend to be more correlated with murder than others, murder is often a highly personal crime whose circumstances vary widely by instance.

To do this analysis, we needed two main datasets: one consisting of violent crimes (including murder rate) in each MSA (metropolitan statistical area) and another consisting of Census data about the same MSAs. The murder rates, by MSA and year, were scraped from the `ucr.fbi.gov` website (accounting for differences by year in website URL format and HTML table tags), Census data was downloaded from the `factfinder.census.gov` website and CSV files were imported into a Python script. Note that the FBI does not provide a standalone rate for murder, only; the rate they provide includes both murders as well as instances of non-negligent manslaughter. It is this rate that we are referring to whenever we discuss or model the 'murder' rate.

There were numerous inconsistencies in data between years. For example, the number of features varies from year to year, as does the metadata, so we decided to fetch only 2010 (chosen arbitrarily) to perform our preliminary EDA. The subset of features was selected (excluding only some extremely redundant features) and renamed for better readability. 

After looking at a histogram which showed us a roughly normal-looking distribution of murder rates across the various MSAs with a mean of around 5 per 100,000 inhabitants, we moved our focus towards scatter plots of 190 features all taken against murder rate. From a careful visual analysis of these as well some common sense thought about forming a reasonable and varied set of predictors, we narrowed that large collection of features down to about 25. Repeating a similar analysis and scrutiny, we arrived at a selection of eight features (in addition to MSA and year) to be used in our modeling:

- now_married_except_separated
- less_than_high_school_diploma
- unmarried_portion_of_women_15_to_50_years_who_had_a_birth_in_past_12_months
- households_with_food_stamp_snap_benefits
- percentage_married-couple_family
- percentage_female_householder_no_husband_present_family
- poverty_all_people
- house_median_value_(dollars)


For these eight features, we merged (on MSA name) the two datasets described above to create a dataset on the matching rows, only. The FBI and Census have different sets of MSAs, so we used the smaller set (Census) and most matched perfectly to the FBI data, while leaving some of the FBI data points unused. This approach seems appropriate as it is not possible to match certain FBI listed MSA's to Census data if those are not available.

We noticed that some MSAs had similar but different names across years. In every case where we believed the MSA to represent either mostly or exactly the same geographical area, we chose a single name for MSA to use across all years of data provided for it. For the sake of transparency, we have included in our merged dataset both the original MSA name ('MSA_orig') as well as the revised/corrected one ('MSA_corr'), so that you can see where and how MSA names were revised. Additionally, for technical convenience, we added a column named 'MSA_abbr' to contain a much shorter version of each MSA name in a contiguous and highly-consistent format. This was particularly helpful for one-hot encoding the MSAs. For example, here is the set of these names that applied for the Denver, CO MSA:

MSA_orig|MSA_corr|MSA_abbr|year
---|---|---|---
Denver-Aurora-Lakewood, CO|Denver-Aurora, CO|DENVER_CO|2016



### Literature Review / Related Work

<font color='red'>`David please add 1-2 examples`</font>


>This could include noting any key papers, texts, or websites that you have used to develop your modeling approach, as well as what others have done on this problem in the past. You must properly credit sources.
>
We took our moving average approach from the Wikipedia page for that topic: 

https://en.wikipedia.org/wiki/Moving_average

It mentioned that "in science and engineering the mean is normally taken from an equal number of data on either side of a central value. This ensures that variations in the mean are aligned with the variations in the data rather than being shifted in time." Therefore, this is the approach that we used in our temporal modeling.

### Modeling Approach and Project Trajectory

#### Modeling Outlier Effects

We began the modeling phase by first splitting our merged dataset into train and test sets. We conducted a random 70/30 split for train and test, respectively.

During our EDA, we noticed a few observations with particularly high murder rates. Therefore, we created additional versions of our train and test sets sans outliers.

For our baseline modeling, we used a dictionary approach which allowed us to run a series of models in a somewhat side-by-side progression. We ran linear, ridge, huber, knn, adaboost and svr (support vector regression) models in this initial stage of modeling. Furthermore, we ran each of these models on both the full and sans-outliers train datasets.

<font color='red'>`David please describe violin plot results from Modeling Outlier Effects`</font>

#### Modeling Feature Subsets

Next, we decided to examine the differences between including/excluding MSA, year and/or features in our modeling. More specifically, we looked at the following subsets:
- MSA + Year
- MSA + Year + Features
- Features + Year

Given our results from modeling the effects of outliers, we excluded them from all models going forward, including here.


#### Modeling Temporal Effects
TODO

#### Inference
TODO

### Results, Conclusions, and Future Work
>Show and interpret your results. Summarize your results, the strengths and short-coming of your results, and speculated on how you might dress these short-comings if given more time



*Todo*



> delete [:2][::-1] in Outliers violin_plots([exp_3, exp_4], coeff_names, experiment_name=['Outliers','No Outliers'], cmap=colors[:2][::-1])



<br><br><br>
![png](img/report_requirements.png)
