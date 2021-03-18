# Methodology

## General process
The DERI score is composed of a number of calculations that each build on top of one another. The base level for these calculations is a series of individual indicators at an LSOA level. The general process is:

1. Individual indicators are used to create an individual indicator score for each LSOA.
2. These indicator scores are then weighted to create several component scores.
3. These components are then weighted to create the final DERI score.

The most important area of this work is the original indicator score calculation.

## Choice of indicators

## Choice of geography

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

### Scoring based on minimum and maximum 
Based on the above, it is clear that most indicators suggest that a higher rate, score or proportion is equivalent to a higher level of risk of digital exclusion. However, all of these indicators have different denominators (e.g. number of homes, number of connections, number of people aged 16+). It is therefore important, in order to create an index, that these indicators are transformed into a consistent 'score'. For the DERI, the score for each indicator in each LSOA is given as a number between 0 and 10, where 10 indicates a higher level of digital exclusion risk.

The score for each indicator aimed to show how far between the minimum and maximum indicator values the individual indicator value was for each LSOA located. This gives a value between 0 (the LSOA has the smallest indicator value, therefore indicating low risk) to 10 (the LSOA has the highest indicator value, therefore indicating high risk).

The calculation used for each LSOA (l) anbd each indicator (i) was:

>10 x ((Value of indicator i for LSOA l) - (Minimum value of indicator i)) / ((Maximum value of i) - (Minimum value of i))

However, for one of the indicators (average download speed), a lower value indicated a higher risk. As a result, the calculation is different for this indicator. There are two possible formulations:

>10 x ((Maximum value if i) - (Value of indicator i for LSOA l)) / ((Maximum value of i) - (Minimum value of i))

OR

>10 - (10 x ((Value of indicator i for LSOA l) - (Minimum value of indicator i)) / ((Maximum value of i) - (Minimum value of i)))

Both calculations should provide the same outcome.

### Local considerations
The DERI score is based on some original work at Salford City Council. As this work was created for just one local authority, the maximum and minimum values of each indicator were based on the maximum and minimum levels of the local authority (for more information on the background, see the Background document). As a result of this, there are multiple approaches that can be taken.

The first is to consider this information on a single geographic basis. That is, use the maximum and minimum values nationally. However, not all datasets are provided across all areas of the UK, or even of Great Britain. Substitute indicators might also need to be used.

The second option is to consider a smaller geography, such as local authority level, for the maximum and minimum values. The benefit of this approach is it provides a localised view of where risk is highest, regardless of the wider levels of risk.

The third option, and one being used by the Tableau online tool, is to take the maximum and minimum values of the areas of focus. That is, if a local authority is being viewed, the maximum and minimum values of that local authority are used; if a region is being viewed, the maximum and minimum values of that region are used.

## Components

### Age component

### Broadband component

### Deprivation component

### Activity component

## DERI Score
