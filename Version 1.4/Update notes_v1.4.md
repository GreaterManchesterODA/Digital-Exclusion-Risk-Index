# Updates to Version 1.4

[Version 1.4](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_4/DERIhomepage?:iid=2&:isGuestRedirectFromVizportal=y&:embed=y) included three main changes to the methodology and tool:
* Transforming the 'age' component to a broader 'demography' component
* Calculating two new sets of DERI scores based on national and Great Britain level mins and maxes
* Adding functionality to the dashboards to allow users to select the preferred DERI score (local/national/GB)

## Demography component
Versions 1.0 to 1.3 of the DERI used an age component to form the DERI score. However, [research by the Good Things Foundation](https://www.goodthingsfoundation.org/insights/digital-exclusion-and-health-inequalities/) indicates that there are other demographic factors in addition to age that put people at higher risk of being digitally excluded, such as being disabled or on a low income. As a result, we have expanded our `Age component` to a broader `Demography component` that brings together the following four indicators:
* Percentage of population aged 65-74
* Percentage of population aged 75+
* Percentage of residents whose daily activities are limited
* Percentage of population in social grade DE

### Tableau updates for demography component
Changing this component required two new sets of calculations: one set to create a score for the percentage of residents whose daily activities are limited and one for the percentage of population in social grade DE. Parameters were also created for the weightings of each of these new scores. The creation of these calculations and parameters followed the same process as outlined in the original [version 1.0 methodology](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.0/DERI%20Score%20Methodology_v1.0.md#individual-indicator-scores), with updates to the parameter weightings as outlined in the [version 1.2 methodology](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.2/Update%20notes_v1.2.md).

#### New calculated fields for indicator minimum and maximums
The first step in creating new indicator scores is to fix the minimum and maximum LSOA scores within each local authority district. This is done by creating calculated fields, as outlined in the table below:

|Indicator|Type|Calculated field name|Calculation|
|---|---|---|---|
|Percentage of population with disability|Maximum per district|Max of percentage of population with disability|`{ FIXED [Local authority name]: MAX([Percentage of residents whose day-to-day activities are limited])}`|
|Percentage of population with disability|Minimum per district|Min of percentage of population with disability|`{ FIXED [Local authority name]: MIN([Percentage of residents whose day-to-day activities are limited])}`|
|Percentage of residents in social grade DE|Maximum per district|Max of Percentage of residents in social grade DE|`{ FIXED [Local authority name]: MAX([Percentage of residents in social grade DE])}`|
|Percentage of residents in social grade DE|Minimum per district|Min of Percentage of residents in social grade DE|`{ FIXED [Local authority name]: MIN([Percentage of residents in social grade DE])}`|

#### New calculated fields for indicator scores
Using the minimum and maximum value calculated fields mentioned above, individual scores between 0 and 10 can be created for the two new indicators. For both of these indicators, a higher value is assumed to relate to a higher risk of digital exclusion. Therefore, the highest value would receive a score of 10, and the lowest value a score of 0. A value halfway between the highest and lowest values would gain a score of 5. The calculated fields for creating these scores are shown in the table below:

|Score name|Score calculation|
|---|---|
|Score: percentage of population with disability|`10*([Percentage of residents whose day-to-day activities are limited]-[Min of percentage of population with disability])/([Mx of percentage of population with disability]-[Min of percentage of population with disability])`|
|Score: percentage of population in social grade DE|`10*([Percentage of population in social grade DE]-[Min of percentage of population in social grade DE])/([Max of percentage of population in social grade DE]-[Min of percentage of population in social grade DE])`|

#### New parameters
To create each component score, weightings are applied to each indicator score. The new parameters needed in order to create the demography component are outlined in the table below:

|Parameter name|Type|Applied to|Default value|
|---|---|---|---|
|Weighting: disability|Indicator weighting|Percentage of residents whose day-to-day activities are limited|2|
|Weighting: social grade DE|Indicator weighting|Percentage of population in social grade DE|2|

#### Updated calculation for demography component
Once these calculations and parameters were created, the `Age component` was renamed to `Demography component` and the calculated field for the component was updated to be based on the scores and parameters for all four indicators. The calculation for the updated demography component is shown below:

`([Score: percentage of population aged 65+]*(([Weighting: 65+]/([Weighting: 65+]+[Weighting: 75+])))+([Score: percentage of population aged 75+]*(([Weighting: 75+]/([Weighting: 65+]+[Weighting: 75+])))+([Score: percentage of population with disability]*([Weighting: disability]/([Weighting: 65-74]+[Weighting: 75+]+[Weighting: disability]+[Weighting: social grade DE])))+([Score: percentage of population in social grade DE]*([Weighting: social grade DE]/([Weighting: 65-74]+[Weighting: 75+]+[Weighting: disability]+[Weighting: social grade DE])))`

## National and Great Britain DERI scores 
Prior versions of the DERI tool based the calculation for the indicator, component and DERI scores on the minimum and maximum values in each local authority district. While this is useful for seeing the relative risk of digital exclusion within a local area, this approach limits the usefulness of comparisons between different local authority areas. To enable meaningful comparisons between different local authorities required a second and third set of calculations to be created. The first set recalculated the scores based upon the maximum and minimum indicator values within each nation (England, Scotland and Wales). The second set recalculated the scores based upon the maximum and minimum values across the full dataset, which includes all of Great Britain.

### Tableau updates for national and Great Britain DERI scores
As with the original methodology outlined in [version 1.0](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.0/Tableau%20development_v1.0.md), the national and Great Britain DERI score must be built up from a series of individual indicator scores. These indicator scores are built using calculations to work out the minimum and maximum LSOA values for those scores. In the original methodology, these minimum and maximum LSOA values were fixed at Local Authority level.

#### Maximum and minimum calculations for indicator scores
In order to create the minimum and maximum of each nation's LSOA values, the calculation needs to be fixed at the nation level. In order to create the minimum and maximum of the Great Britain LSOA values, the calculation needs to be fixed at the highest and lowest value within the full dataset.

The standard calculation used for each 'maximum' field at the nation level was:

`{ FIXED [nation]: MAX([indicator])}`

Similarly, the calculation used for the 'minimum' field was:

`{ FIXED [nation]: MIN([indicator])}`

The standard calculation used for the 'maximum' at the Great Britain level was:

`{ FIXED: MAX([indicator])}`

Similarly, the calculation used for the 'minimum' field was:

`{ FIXED: MIN([indicator])}`

In total, 22 calculated fields were created for each new set - one minimum and one maximum calculated field for each indicator. The full list of calculated fields and calculations at nation level is presented in [Appendix A](#appendix-a) and the full list of calculations at Great Britain level is presented in [Appendix B](#appendix-b).

#### Indicator score calculations
As with the original methodology, using the minimum and maximum value calculated fields mentioned above, individual scores between 0 and 10 can be created for each indicator. In most instances, a higher indicator value is assumed to relate to a higher risk of digital exclusion. Therefore, the calculation identifies where on the scale between the minimum and maximum values in the district each LSOA lies. The highest value would receive a score of 10, and the lowest value a score of 0. A value halfway between the highest and lowest values would gain a score of 5.

The general calculation for this remains:

`10*([indicator value]-[Min of indicator])/([Max of indicator]-[Min of indicator])`

where `[indicator value]` is the value of the the indicator for each LSOA, and `[Max of indicator]` and `[Min of indicator]` represent the maximum and minimums of that indicator, as mentioned above, at either the nation or Great Britain level.

However, one indicator - the average download speed - was associated with higher risk of digital exclusion. As average broadband speeds are lower, there is a risk that many homes will have low speed connections that might be underutilised. In this instance, the calculation is reversed: when average broadband speeds are low, the score needs to be high, and vice versa:

`10*([Max of indicator]-[indicator value])/([Max of indicator]-[Min of indicator])`

A full list of indicator score calculations at nation level is provided in [Appendix C](#appendix-c) and a full list of indicator score calculations at Great Britain level is provided in [Appendix D](#appendix-D).

#### Component and DERI score calculations

The general calculation method for each component score follows the same process as the methodology for Local Authority scores, as outlined in [updates to version 1.2](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.2/Update%20notes_v1.2.md) of the tool:

`(Indicator score A * ((Indicator score A weighting)/(Indicator score A weighting + Indicator score B weighting + Indicator score C weighting ...)) + (Indicator score B * (Indicator score B weighting)/Indicator score A weighting + Indicator score B weighting + Indicator score C weighting ...) + ...`

This weighted sum is applied to all of the relevant indicators for each component to produce a component score.

A full list of calculations for the nation level scores is presented in [Appendix E](#appendix-e) and a full list of calculations for the GB level scores is presented in [Appendix F](#appendix-f).


## Improving dashboard functionality to select different DERI score calculations
To allow users the option to choose a set of scores at either local authority, nation or Great Britain level requires the creation of a new parameter and a new set of calculated fields to update the scores based on the parameter selection.

### Local / national / GB parameter
The parameter required is as follows:
|Parameter name|Data type|Options|Default value|
|---|---|---|---|
|Local / national / GB score|String|Local Authority, Nation, Great Britain|Local Authority|

### Calculated fields for local / national / GB selection
The calculated fields tell Tableau which set of scores to select based on the parameter selection. As the DERI score pulls together the scores for each component, four calculations are needed to accompany the parameter - one for each component (broadband, demography and deprivation) and one for the overall DERI score. The component calculations follow the format below, where 'X' is either broadband, demography or deprivation:

`CASE [Local / national / GB score]`

`WHEN "Local Authority" THEN [X component]`

`WHEN "Nation" THEN [X component (national)]`

`WHEN "Great Britain" THEN [X component (GB)]`

`END`

The calculation for the overall DERI score follows the same format:

`CASE [Local / national / GB score]`

`WHEN "Local Authority" THEN [DERI score]`

`WHEN "Nation" THEN [DERI score (national)]`

`WHEN "Great Britain" THEN [DERI score (GB)]`

`END`

### Adding the parameter to the dashboards
The final step to allow users to select whether the scores are calculated based on either local authority, nation level, or Great Britain level mins and maxes is to add the parameter to the Tableau workbook dashboards. There is space in the dashboard to add the parameter in a horizontal container next to the filter for the local authority selection, underneath the title of the dashboard.

The dashboards are linked so that if 'Nation' is selected in one dashboard, the scores will be updated to display the national scores throughout the other dashboards.

## Appendix A: Calculations for nation level minimum and maxium fields
|Indicator|Type|Calculated field name|Calculation|
|---|---|---|---|
|Nation level Percentage of homes unable to receive at least 30MBit/s|Maximum per nation|National max of Percentage of homes unable to receive at least 30MBit/s|`{ FIXED [Nation]: MAX([Percentage of homes unable to receive at least 30Mbit/s broadband])}`|
|Nation level Percentage of homes unable to receive at least 30MBit/s|Minimum per nation|National min of Percentage of homes unable to receive at least 30MBit/s|`{ FIXED [Nation]: MIN([Percentage of homes unable to receive at least 30Mbit/s broadband])}`|
|Nation level Average download speed (MBit/s)|Maximum per nation|National max of Average download speed|`{ FIXED [Nation]: MAX([Average download speed (Mbit/s)])}`|
|Nation level Average download speed (MBit/s)|Minimum per nation|National min of Average download speed|`{ FIXED [Nation]: MIN([Average download speed (Mbit/s)])}`|
|Nation level Percentage of connections receiving less than 10MBit/s|Maximum per nation|National max of Percentage of connections less than 10MBit/s|`{ FIXED [Nation]: MAX([Percentage of connections receiving less than 10MBit/s])}`|
|Nation level Percentage of connections receiving less than 10MBit/s|Minimum per nation|National min of Percentage of connections less than 10MBit/s|`{ FIXED [Nation]: MIN([Percentage of connections receiving less than 10MBit/s])}`|
|Nation level Percentage of population aged 65 and over|Maximum per nation|National max of Percentage of population aged 65+|`{ FIXED [Nation]: MAX([Percentage of population aged 65 and over])}`|
|Nation level Percentage of population aged 65 and over|Minimum per nation|National min of Percentage of population aged 65+|`{ FIXED [Nation]: MIN([Percentage of population aged 65 and over])}`|
|Nation level Percentage of population aged 75 and over|Maximum per nation|National max of Percentage of population aged 75+|`{ FIXED [Nation]: MAX([Percentage of population aged 75 and over])}`|
|Nation level Percentage of population aged 75 and over|Minimum per nation|National min of Percentage of population aged 75+|`{ FIXED [Nation]: MIN([Percentage of population aged 75 and over])}`|
|Nation level Percentage of residents aged 16+ with no qualifications|Maximum per nation|National max of Percentage of residents with no qualifications|`{ FIXED [Nation]: MAX([Percentage of residents aged 16+ with no qualifications])}`|
|Nation level Percentage of residents aged 16+ with no qualifications|Minimum per nation|National min of Percentage of residents with no qualifications|`{ FIXED [Nation]: MIN([Percentage of residents aged 16+ with no qualifications])}`|
|Nation level Guaranteed pension credit (rate per 1,000 aged 65+)|Maximum per nation|National max of Guaranteed Pension Credit|`{ FIXED [Nation]: MAX([Guaranteed pension credit (rate per 1,000 aged 65+)])}`|
|Nation level Guaranteed pension credit (rate per 1,000 aged 65+)|Minimum per nation|National min of Guaranteed Pension Credit|`{ FIXED [Nation]: MIN([Guaranteed pension credit (rate per 1,000 aged 65+)])}`|
|Nation level Index of Multiple Deprivation 2019 score|Maximum per nation|National max of Index of Multiple Deprivation Score|`{ FIXED [Nation]: MAX([Index of Multiple Deprivation 2019 score])}`|
|Nation level Index of Multiple Deprivation 2019 score|Minimum per nation|National min of Index of Multiple Deprivation Score|`{ FIXED [Nation]: MIN([Index of Multiple Deprivation 2019 score])}`|
|Nation level Unemployment rate|Maximum per nation|National max of Unemployment rate|`{ FIXED [Nation]: MAX([Unemployment rate])}`|
|Nation level Unemployment rate|Minimum per nation|National min of Unemployment rate|`{ FIXED [Nation]: MIN([Unemployment rate])}`|
|Nation level percentage of residents in social grade DE|Maximum per nation|National max of Percentage of residents in social grade DE|`{ FIXED [Nation]: MAX([Percentage of residents in social grade DE])}`|
|Nation level percentage of residents in social grade DE|Minimum per nation|National min of Percentage of residents in social grade DE|`{ FIXED [Nation]: MIN([Percentage of residents in social grade DE])}`|
|Nation level percentage of population with disability|Maximum per nation|National max of percentage of population with disability|`{ FIXED [Nation]: MAX([Percentage of residents whose day-to-day activities are limited])}`|
|Nation level percentage of population with disability|Minimum per nation|National min of percentage of population with disability|`{ FIXED [Nation]: MIN([Percentage of residents whose day-to-day activities are limited])}`|

## Appendix B: Calculations for Great Britan level minimum and maxium fields
|Indicator|Type|Calculated field name|Calculation|
|---|---|---|---|
|GB level Percentage of homes unable to receive at least 30MBit/s|Maximum per full dataset|GB max of Percentage of homes unable to receive at least 30MBit/s|`{ FIXED: MAX([Percentage of homes unable to receive at least 30Mbit/s broadband])}`|
|GB level Percentage of homes unable to receive at least 30MBit/s|Minimum per full dataset|GB min of Percentage of homes unable to receive at least 30MBit/s|`{ FIXED: MIN([Percentage of homes unable to receive at least 30Mbit/s broadband])}`|
|GB level Average download speed (MBit/s)|Maximum per full dataset|GB max of Average download speed|`{ FIXED: MAX([Average download speed (Mbit/s)])}`|
|GB level Average download speed (MBit/s)|Minimum per full dataset|GB min of Average download speed|`{ FIXED: MIN([Average download speed (Mbit/s)])}`|
|GB level Percentage of connections receiving less than 10MBit/s|Maximum per full dataset|GB max of Percentage of connections less than 10MBit/s|`{ FIXED: MAX([Percentage of connections receiving less than 10MBit/s])}`|
|GB level Percentage of connections receiving less than 10MBit/s|Minimum per full dataset|GB min of Percentage of connections less than 10MBit/s|`{ FIXED: MIN([Percentage of connections receiving less than 10MBit/s])}`|
|GB level Percentage of population aged 65 and over|Maximum per full dataset|GB max of Percentage of population aged 65+|`{ FIXED: MAX([Percentage of population aged 65 and over])}`|
|GB level Percentage of population aged 65 and over|Minimum per full dataset|GB min of Percentage of population aged 65+|`{ FIXED: MIN([Percentage of population aged 65 and over])}`|
|GB level Percentage of population aged 75 and over|Maximum per full dataset|GB max of Percentage of population aged 75+|`{ FIXED: MAX([Percentage of population aged 75 and over])}`|
|GB level Percentage of population aged 75 and over|Minimum per full dataset|GB min of Percentage of population aged 75+|`{ FIXED: MIN([Percentage of population aged 75 and over])}`|
|GB level Percentage of residents aged 16+ with no qualifications|Maximum per full dataset|GB max of Percentage of residents with no qualifications|`{ FIXED: MAX([Percentage of residents aged 16+ with no qualifications])}`|
|GB level Percentage of residents aged 16+ with no qualifications|Minimum per full dataset|GB min of Percentage of residents with no qualifications|`{ FIXED: MIN([Percentage of residents aged 16+ with no qualifications])}`|
|GB level Guaranteed pension credit (rate per 1,000 aged 65+)|Maximum per full dataset|GB max of Guaranteed Pension Credit|`{ FIXED: MAX([Guaranteed pension credit (rate per 1,000 aged 65+)])}`|
|GB level Guaranteed pension credit (rate per 1,000 aged 65+)|Minimum per full dataset|GB min of Guaranteed Pension Credit|`{ FIXED: MIN([Guaranteed pension credit (rate per 1,000 aged 65+)])}`|
|GB level Index of Multiple Deprivation 2019 score|Maximum per full dataset|GB max of Index of Multiple Deprivation Score|`{ FIXED: MAX([Index of Multiple Deprivation 2019 score])}`|
|GB level Index of Multiple Deprivation 2019 score|Minimum per full dataset|GB min of Index of Multiple Deprivation Score|`{ FIXED: MIN([Index of Multiple Deprivation 2019 score])}`|
|GB level Unemployment rate|Maximum per full dataset|GB max of Unemployment rate|`{ FIXED: MAX([Unemployment rate])}`|
|GB level Unemployment rate|Minimum per full dataset|GB min of Unemployment rate|`{ FIXED: MIN([Unemployment rate])}`|
|GB level percentage of residents in social grade DE|Maximum per full dataset|GB max of Percentage of residents in social grade DE|`{ FIXED: MAX([Percentage of residents in social grade DE])}`|
|GB level percentage of residents in social grade DE|Minimum per full dataset|GB min of Percentage of residents in social grade DE|`{ FIXED: MIN([Percentage of residents in social grade DE])}`|
|GB level percentage of population with disability|Maximum per full dataset|GB max of percentage of population with disability|`{ FIXED: MAX([Percentage of residents whose day-to-day activities are limited])}`|
|GB level percentage of population with disability|Minimum per full dataset|GB min of percentage of population with disability|`{ FIXED: MIN([Percentage of residents whose day-to-day activities are limited])}`|

## Appendix C: Nation level indicator scores
|Score name|Score calculation|
|---|---|
|National score: average download speed|`10*([National max of Average download speed]-[Average download speed (Mbit/s)])/([National max of Average download speed]-[National min of Average download speed])`|
|National score: guaranteed pension credit|`10*([Guaranteed pension credit (rate per 1,000 aged 65+)]-[National min of Guaranteed Pension Credit])/([National max of Guaranteed Pension Credit]-[National min of Guaranteed Pension Credit])`|
|National score: Index of Multiple Deprivation score|`10*([Index of Multiple Deprivation 2019 score]-[National min of Index of Multiple Deprivation Score])/([National max of Index of Multiple Deprivation Score]-[National min of Index of Multiple Deprivation Score])`|
|National score: percentage of connections receiving less than 10MBit/s|`10*([Percentage of connections receiving less than 10Mbit/s broadband]-[National min of Percentage of connections less than 10MBit/s])/([National max of Percentage of connections less than 10MBit/s]-[National min of Percentage of connections less than 10MBit/s])`|
|National score: percentage of homes unable to receive at least 30MBit/s|`10*([Percentage of homes unable to receive at least 30Mbit/s broadband]-[National min of Percentage of homes unable to receive at least 30MBit/s])/([National max of Percentage of homes unable to receive at least 30MBit/s]-[National min of Percentage of homes unable to receive at least 30MBit/s])`|
|National score: percentage of population aged 65+|`10*([Percentage of population aged 65 and over]-[National min of Percentage of population aged 65+])/([National max of Percentage of population aged 65+]-[National min of Percentage of population aged 65+])`|
|National score: percentage of population aged 75+|`10*([Percentage of population aged 75 and over]-[National min of Percentage of population aged 75+])/([National max of Percentage of population aged 75+]-[National min of Percentage of population aged 75+])`|
|National score: percentage of residents aged 16+ with no qualifications|`10*([Percentage of residents aged 16+ with no qualifications]-[National min of Percentage of residents with no qualifications])/([National max of Percentage of residents with no qualifications]-[National min of Percentage of residents with no qualifications])`|
|National score: unemployment rate|`10*([Unemployment rate]-[National min of Unemployment rate])/([National max of Unemployment rate]-[National min of Unemployment rate])`|
|National score: percentage of population with disability|`10*([Percentage of residents whose day-to-day activities are limited]-[National min of percentage of population with disability])/([National max of percentage of population with disability]-[National min of percentage of population with disability])`|
|National score: percentage of population in social grade DE|`10*([Percentage of population in social grade DE]-[National min of percentage of population in social grade DE])/([National max of percentage of population in social grade DE]-[National min of percentage of population in social grade DE])`|

## Appendix D: Great Britain level indicator scores
|Score name|Score calculation|
|---|---|
|GB score: average download speed|`10*([GB max of Average download speed]-[Average download speed (Mbit/s)])/([GB max of Average download speed]-[GB min of Average download speed])`|
|GB score: guaranteed pension credit|`10*([Guaranteed pension credit (rate per 1,000 aged 65+)]-[GB min of Guaranteed Pension Credit])/([GB max of Guaranteed Pension Credit]-[GB min of Guaranteed Pension Credit])`|
|GB score: Index of Multiple Deprivation score|`10*([Index of Multiple Deprivation 2019 score]-[GB min of Index of Multiple Deprivation Score])/([GB max of Index of Multiple Deprivation Score]-[GB min of Index of Multiple Deprivation Score])`|
|GB score: percentage of connections receiving less than 10MBit/s|`10*([Percentage of connections receiving less than 10Mbit/s broadband]-[GB min of Percentage of connections less than 10MBit/s])/([GB max of Percentage of connections less than 10MBit/s]-[GB min of Percentage of connections less than 10MBit/s])`|
|GB score: percentage of homes unable to receive at least 30MBit/s|`10*([Percentage of homes unable to receive at least 30Mbit/s broadband]-[GB min of Percentage of homes unable to receive at least 30MBit/s])/([GB max of Percentage of homes unable to receive at least 30MBit/s]-[GB min of Percentage of homes unable to receive at least 30MBit/s])`|
|GB score: percentage of population aged 65+|`10*([Percentage of population aged 65 and over]-[GB min of Percentage of population aged 65+])/([GB max of Percentage of population aged 65+]-[GB min of Percentage of population aged 65+])`|
|GB score: percentage of population aged 75+|`10*([Percentage of population aged 75 and over]-[GB min of Percentage of population aged 75+])/([GB max of Percentage of population aged 75+]-[GB min of Percentage of population aged 75+])`|
|GB score: percentage of residents aged 16+ with no qualifications|`10*([Percentage of residents aged 16+ with no qualifications]-[GB min of Percentage of residents with no qualifications])/([GB max of Percentage of residents with no qualifications]-[GB min of Percentage of residents with no qualifications])`|
|GB score: unemployment rate|`10*([Unemployment rate]-[GB min of Unemployment rate])/([GB max of Unemployment rate]-[GB min of Unemployment rate])`|
|GB score: percentage of population with disability|`10*([Percentage of residents whose day-to-day activities are limited]-[GB min of percentage of population with disability])/([GB max of percentage of population with disability]-[GB min of percentage of population with disability])`|
|GB score: percentage of population in social grade DE|`10*([Percentage of population in social grade DE]-[GB min of percentage of population in social grade DE])/([GB max of percentage of population in social grade DE]-[GB min of percentage of population in social grade DE])`|

## Appendix E: Nation level component and DERI score calculations
|Component name|Component calculation|
|---|---|
|Demography component (national)|`([National score: percentage of population aged 65+]*(([Weighting: 65+]/([Weighting: 65+]+[Weighting: 75+])))+([National score: percentage of population aged 75+]*(([Weighting: 75+]/([Weighting: 65+]+[Weighting: 75+])))+([National score: percentage of population with disability]*([Weighting: disability]/([Weighting: 65-74]+[Weighting: 75+]+[Weighting: disability]+[Weighting: social grade DE])))+([National score: percentage of population in social grade DE]*([Weighting: social grade DE]/([Weighting: 65-74]+[Weighting: 75+]+[Weighting: disability]+[Weighting: social grade DE])))`|
|Broadband component (national)|`([National score: percentage of connections receiving less than 10MBit/s]*([Weighting: connections less than 10MBit/s]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))+([National score: percentage of homes unable to receive at least 30MBit/s]*([Weighting: homes unable to receive 30MBit/s]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))+([National score: average download speed]*([Weighting: avg download speed]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))`|
|Deprivation component (national)|`([National score: unemployment rate]*([Weighting: unemployment rate]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([National score: percentage of residents aged 16+ with no qualifications]*([Weighting: % no quals]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([National score: guaranteed pension credit]*([Weighting: guaranteed pension credit]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([National score: Index of Multiple Deprivation score]*([Weighting: IMD score]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))`|
|DERI score (national)|`([Demography component (national)]*([Weighting: demography component (national)]/([Weighting: demography component (national)]+[Weighting: broadband component (national)]+[Weighting: deprivation component (national)])))+([Broadband component (national)]*([Weighting: broadband component (national)]/([Weighting: demography component (national)]+[Weighting: broadband component (national)]+[Weighting: deprivation component (national)])))+([Deprivation component (national)]*([Weighting: deprivation component (national)]/([Weighting: demography component (national)]+[Weighting: broadband component (national)]+[Weighting: deprivation component (national)])))`|


## Appendix F: Great Britain level component and DERI score calculations
|Component name|Component calculation|
|---|---|
|Demography component (GB)|`([GB score: percentage of population aged 65+]*(([Weighting: 65+]/([Weighting: 65+]+[Weighting: 75+])))+([GB score: percentage of population aged 75+]*(([Weighting: 75+]/([Weighting: 65+]+[Weighting: 75+])))+([GB score: percentage of population with disability]*([Weighting: disability]/([Weighting: 65-74]+[Weighting: 75+]+[Weighting: disability]+[Weighting: social grade DE])))+([GB score: percentage of population in social grade DE]*([Weighting: social grade DE]/([Weighting: 65-74]+[Weighting: 75+]+[Weighting: disability]+[Weighting: social grade DE])))`|
|Broadband component (GB)|`([GB score: percentage of connections receiving less than 10MBit/s]*([Weighting: connections less than 10MBit/s]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))+([GB score: percentage of homes unable to receive at least 30MBit/s]*([Weighting: homes unable to receive 30MBit/s]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))+([GB score: average download speed]*([Weighting: avg download speed]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))`|
|Deprivation component (GB)|`([GB score: unemployment rate]*([Weighting: unemployment rate]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([GB score: percentage of residents aged 16+ with no qualifications]*([Weighting: % no quals]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([GB score: guaranteed pension credit]*([Weighting: guaranteed pension credit]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([GB score: Index of Multiple Deprivation score]*([Weighting: IMD score]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))`|
|DERI score (GB)|`([Demography component (GB)]*([Weighting: demography component (GB)]/([Weighting: demography component (GB)]+[Weighting: broadband component (GB)]+[Weighting: deprivation component (GB)])))+([Broadband component (GB)]*([Weighting: broadband component (GB)]/([Weighting: demography component (GB)]+[Weighting: broadband component (GB)]+[Weighting: deprivation component (GB)])))+([Deprivation component (GB)]*([Weighting: deprivation component (GB)]/([Weighting: demography component (GB)]+[Weighting: broadband component (GB)]+[Weighting: deprivation component (GB)])))`|
