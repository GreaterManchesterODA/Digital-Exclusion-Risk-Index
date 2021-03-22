# Methodology

## Contents
* [General process](#general-process)
* [Choice of indicators](#choice-of-indicators)
* [Choice of geography](#choice-of-geography)
* [Individual indicators scores](#individual-indicators-scores)
  * [Scoring based on minimum and maximum](#scoring-based-on-minimum-and-maximum)
  * [Local considerations](#local-considerations)
* [Components](#components)
  * [Age component and weightings](#age-component-and-weightings)
  * [Broadband component and weightings](#broadband-component-and-weightings)
  * [Deprivation component and weightings](#deprivation-component-and-weightings)
  * [Activity component](#activity-component)
* [DERI Score](#deri-score)
  * [Weightings](#weightings)

## General process
The DERI score is composed of a number of calculations that each build on top of one another. The base level for these calculations is a series of individual indicators at an LSOA level. The general process is:

1. Individual indicators are used to create an individual indicator score for each LSOA.
2. These indicator scores are then weighted to create several component scores.
3. These components are then weighted to create the final DERI score.

The most important area of this work is the original indicator score calculation.

## Choice of indicators
The original choice of indicators comes from work completed internally at Salford City Council. The indicators aim to convey the breadth of the issue of digital exclusion, covering aspects such as age, deprivation and affordability, access, and activity.

It is important to review these over time, and to ensure that chosen and new indicators are not so closely correlated that they do not 'double-count' an issue.

## Choice of geography
The original tool developed by Salford City Council focused on ward areas. All of the datasets used are available at an LSOA or OA level, but not all are available at ward level. It was suggested that the LSOA level of detail remained, and as such the DERI score is provided at an LSOA level. 

## Individual indicator scores
There are 10 individual indicators that make up the overall DERI score. These are individually weighted to form the next part in the calculation chain, the component scores. The table below highlights, for each indicator, what is considered a higher risk of digital exclusion

|Indicator|What is classed as 'higher risk'?|
|---|---|
|Proportion of population aged 65+|Higher proportion|
|Proportion of population aged 75+|Higher proportion|
|Proportion of over 65 residents on guaranteed Pension Credit|Higher proportion|
|Proportion of 16+ population with no qualifications|Higher proportion|
|Alternative unemployment rate|Higher rate|
|Index of Multiple Deprivation score|Higher score|
|Proportion of homes unable to receive 30MBit/s broadband|Higher proportion|
|Proportion of connections receiving less than 10MBit/s|Higher proportion|
|Average download speed|Lower average speed|
|Digital Hard to Count Score|Higher score|

The original work by Salford included two local measures: the proportion of council helpline contacts made online; and the proporton of Council Tax bills that are electronic. In order to expand this nationally, it was decided to drop these two measures. The main reason for this was that the data would not be available at a local level for all local authorities. Additionally, the data is likely to be impacted by the specific focus of the local authority - Salford has made great strdes in recent years in creating a digital first approach to council contacts and services, which may not be consistent across all local authorities. 

### Scoring based on minimum and maximum 
Based on the above, it is clear that most indicators suggest that a higher rate, score or proportion is equivalent to a higher level of risk of digital exclusion. However, all of these indicators have different denominators (e.g. number of homes, number of connections, number of people aged 16+). It is therefore important, in order to create an index, that these indicators are transformed into a consistent 'score'. For the DERI, the score for each indicator in each LSOA is given as a number between 0 and 10, where 10 indicates a higher level of digital exclusion risk.

The score for each indicator aimed to show how far between the minimum and maximum indicator values the individual indicator value was for each LSOA located. This gives a value between 0 (the LSOA has the smallest indicator value, therefore indicating low risk) to 10 (the LSOA has the highest indicator value, therefore indicating high risk).

The calculation used for each indicator (i) and each LSOA (j) was:

>10 x ((Value of indicator i for LSOA j) - (Minimum value of indicator i)) / ((Maximum value of i) - (Minimum value of i))

However, for one of the indicators (average download speed), a lower value indicated a higher risk. As a result, the calculation is different for this indicator. There are two possible formulations:

>10 x ((Maximum value if i) - (Value of indicator i for LSOA l)) / ((Maximum value of i) - (Minimum value of i))

OR

>10 - (10 x ((Value of indicator i for LSOA l) - (Minimum value of indicator i)) / ((Maximum value of i) - (Minimum value of i)))

Both calculations should provide the same outcome.

### Local considerations
The DERI score is based on some original work at Salford City Council. As this work was created for just one local authority, the maximum and minimum values of each indicator were based on the maximum and minimum levels of the local authority (for more information on the background, see the Background document). As a result of this, there are multiple approaches that can be taken.

The first is to consider this information on a single geographic basis. That is, use the maximum and minimum values nationally. However, not all datasets are provided across all areas of the UK, or even of Great Britain. Substitute indicators might also need to be used.

The second option is to consider a smaller geography, such as local authority level, for the maximum and minimum values. The benefit of this approach is it provides a localised view of where risk is highest, regardless of the wider levels of risk. That is, an LSOA could get a score of 10 on one indicator, because it is the highest indicator value within the local authority. Unless the indicator value in that LSOA was also the highest nationally, the LSOA would not get the same score as in the first approach.

The third option is to take the maximum and minimum values of the areas of focus. That is, if a local authority is being viewed, the maximum and minimum values of that local authority are used; if a region is being viewed, the maximum and minimum values of that region are used. This would mean a recalculation - and thereby reprioritisation of risk - dependent on the area in focus.

## Components
Each indicator is turned into a score between 0 and 10. This allows indicators to be grouped into wider 'components' of digital exclusion, and weighted to provide a component score between 0 and 10. The four components are: age, broadband, deprivation, and activity. The calculation is simply:

(Indicator score a x weighting a) + (indicator score b x weighting b) ...

### Age component and weightings
The age component is built from two indicator scores: the proportion of the population aged 65+, and the proportion of the population aged 75+. There is a clear correlation between these two datasets, but not a direct correlation. As a result, both datasets are used. Each is equally weighted (50% each) to form the age component.

### Broadband component and weightings
The broadband component is built from three indicator scores: the proportion of homes unable to receive a 30MBit/s connection; the proportion of connections receiving less than 10MBit/s broadband; and the average download speed. The components are equally weighted (33.3%).

### Deprivation component and weightings
The deprivation component is built from four indicator scores: the proportion of over 65 residents on guaranteed Pension Credit; the proportion of 16+ population with no qualifications; the alternative unemployment rate; and the Index of Multiple Deprivation score. The components are weighted 20%, 40%, 20% and 20% respectively.

### Activity component
The activity component is built from just one indicator: the ONS' Digital Hard to Count score.

## DERI Score
The overall DERI score takes each of the components and weights them to provide a score between 0 and 10, with 0 being low risk of digital exclusion, and 10 being a high risk. The score is again composed of the sum of weighted individual component scores. That is:

(Age component score x age component weighting) + (Deprivation component score x deprivation component weighting) + (Broadband component score x broadband component weighting) + (Activity component score x activity component weighting)

### Weightings
The weightings used for the DERI score are:
* Age component: 33%
* Broadband component: 17%
* Deprivation component: 33%
* Activity component: 17%
