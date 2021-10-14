# Updates to Version 1.5

[Version 1.5](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_5/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y) contains two main updates to the DERI tool:
* Calculating a version of the Index of Multiple Deprivation score based on each of the English, Welsh and Scottish methodologies
* Adding functionality to the dashboards to allow users to select the English, Welsh or Scottish scores

## Calculating English, Welsh and Scottish IMD scores
Each of the English, Welsh and Scottish IMD scores use slightly different metrics and methodologies so they are not directly comparable. This means that a score of x on the English IMD should not be construed as comparable to the same score on the Welsh or Scottish IMD scale. However, a few years ago a group of researchers set out to come up with a coherent deprivation score by mapping between the various domains. This work has been recently updated and is [published here](https://github.com/mysociety/composite_uk_imd), along with reflective discussion about how to use the scores and what their limitations are.

This repository includes a different composite IMD file for each nation, in which that nation has been used as the calculation base and all other scores are aligned with that nation's scores. The guidance for the composite IMD is to use the data corresponding to the primary area of focus. Given that the DERI tool is available for users in all three nations, we felt it was necessary to provide users with the option to select the IMD score that corresponds to their area.

The repository has UK indices and GB indices. We have used the GB set of data as the DERI tool currently only looks at England, Wales and Scotland. The links below show where we sourced each dataset from the composite IMD repository:
* [English IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_E.csv)
* [Welsh IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_W.csv)
* [Scottish IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_S.csv)

### Tableau calculations for the IMD scores

#### Calculations for new indicator minimum and maximums
The process for calculating the separate IMD scores within the DERI tool followed the same steps as the original [indicator score methodology](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.0/DERI%20Score%20Methodology_v1.0.md#individual-indicator-scores). The first step in creating new indicator scores is to fix the minimum and maximum LSOA scores within each local authority district, nation and Great Britain. 

The mins and maxes needed to be calculated for each of the English, Welsh and Scottish IMD figures, fixed separately at Local Authority, nation, and Great Britain level. This requires 9 new calculated fields for the maxes, in the format of the calculations below, where X is either England, Scotland or Wales.

`{FIXED [Local Authority name] : MAX([IMD score - X base])}`

`{FIXED [Nation] : MAX([IMD score - X base])}`

`{FIXED : MAX([IMD score - X base])}`

Similarly, this requires 9 new calculated fiels for the mins, in the format of the calculations below, where X is either England, Scotland or Wales.

`{FIXED [Local Authority name] : MIN([IMD score - X base])}`#

`{FIXED [Nation] : MIN([IMD score - X base])}`

`{FIXED : MIN([IMD score - X base])}`

The 18 individual calculations required for this step are outlined in full in Appendix A.

#### Calculations for new indicator scores

Once all of the minimum and maximum calculated fields are created, they can be used to calculate 9 unique IMD scores to feed into the DERI tool. The calculations to create an English, Scottish and Welsh IMD score based on local authority, national, and Great Britain mins and maxes follow the format below.

`10*([Index of Multiple Deprivation 2019 score - X base]-[Y min of IMD score - X base])/([Y max of IMD score - X base]-[Y min of IMD score - X base])`

where `X` is either England, Wales or Scotland, and `Y` is either local authority, nation or Great Britain.

## Adding functionality to choose the IMD score base within the dashboards
In order to select different IMD scores within the dashboards, a new parameter and set of calculated fields must be created. These can then be added into the dashboard to allow users to select different IMD score options.

### New parameter
A parameter is required to provide users with the option to choose a score. This parameter is called `IMD: England / Scotland / Wales` with `Data type: String` and `Values of: England, Scotland, Wales`

### Interim calculated fields
To bring this parameter into the calculations behind the main component scores that feed into the dashboards, three interim calculated fields are needed: one for the IMD scores at Local Authority level, one at national level, and one at Great Britain level. These calculated fields follow the format below:

`CASE [IMD: England / Scotland / Wales]`

`WHEN "England" THEN [X score: IMD score (England)]`

`WHEN "Scotland" THEN [X score: IMD score (Scotland)]`

`WHEN "Wales" THEN [X score: IMD score (Wales)]`

`END`

where `X` is either local authority, nation, or Great Britain.

This calculated field then forms the basis of the IMD score within the main calculated field for the `Deprivation component (GB)`. This allows the score to be controlled by both the `IMD: England /Scotland / Wales` parameter and the `Local / national / GB score` parameter (from [Version 1.4](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.4/Update%20notes_v1.4.md)) simultaneously. 

### Adding the parameter to the dashboards
The addition of the different calculation bases for the Index of Multiple Deprivation score impacts the deprivation component and feeds through to the overall DERI score. Therefore the `IMD: England / Scotland / Wales` parameter needed to be added to both the 'Deprivation Score dashboard' and the 'DERI Score dashboard'. 

## Appendix A: Calculations for minimum and maximum fields
|Indicator|Type|Calculated field name|Calculation|
|---|---|---|---|
|District level IMD score - England base|Maximum per district|Max of IMD score - England base|`{ FIXED [Local authority name]: MAX([Index of Multiple Deprivation 2019 score - England base])}`|
|District level IMD score - England base|Minimum per district|Min of IMD score - England base|`{ FIXED [Local authority name]: MIN([Index of Multiple Deprivation 2019 score - England base])}`|
|District level IMD score - Scotland base|Maximum per district|Max of IMD score - Scotland base|`{ FIXED [Local authority name]: MAX([Index of Multiple Deprivation 2019 score - Scotland base])}`|
|District level IMD score - Scotland base|Minimum per district|Min of IMD score - Scotland base|`{ FIXED [Local authority name]: MIN([Index of Multiple Deprivation 2019 score - Scotland base])}`|
|District level IMD score - Wales base|Maximum per district|Max of IMD score - England base|`{ FIXED [Local authority name]: MAX([Index of Multiple Deprivation 2019 score - Wales base])}`|
|District level IMD score - Wales base|Minimum per district|Min of IMD score - England base|`{ FIXED [Local authority name]: MIN([Index of Multiple Deprivation 2019 score - Wales base])}`|
|Nation level IMD score - England base|Maximum per nation|National max of IMD score - England base|`{ FIXED [Nation]: MAX([Index of Multiple Deprivation 2019 score - England base])}`|
|Nationl level IMD score - England base|Minimum per nation|National min of IMD score - England base|`{ FIXED [Nation]: MIN([Index of Multiple Deprivation 2019 score - England base])}`|
|Nation level IMD score - Scotland base|Maximum per nation|National max of IMD score - Scotland base|`{ FIXED [Nation]: MAX([Index of Multiple Deprivation 2019 score - Scotland base])}`|
|Nation level IMD score - Scotland base|Minimum per nation|National min of IMD score - Scotland base|`{ FIXED [Nation]: MIN([Index of Multiple Deprivation 2019 score - Scotland base])}`|
|Nation level IMD score - Wales base|Maximum per nation|National max of IMD score - England base|`{ FIXED [Nation]: MAX([Index of Multiple Deprivation 2019 score - Wales base])}`|
|Nation level IMD score - Wales base|Minimum per nation|National min of IMD score - England base|`{ FIXED [Nation]: MIN([Index of Multiple Deprivation 2019 score - Wales base])}`|
|GB level IMD score - England base|Maximum per full dataset|GB max of IMD score - England base|`{ FIXED: MAX([Index of Multiple Deprivation 2019 score - England base])}`|
|GB level IMD score - England base|Minimum per full dataset|GB min of IMD score - England base|`{ FIXED: MIN([Index of Multiple Deprivation 2019 score - England base])}`|
|GB level IMD score - Scotland base|Maximum per full dataset|GB max of IMD score - Scotland base|`{ FIXED: MAX([Index of Multiple Deprivation 2019 score - Scotland base])}`|
|GB level IMD score - Scotland base|Minimum per full dataset|GB min of IMD score - Scotland base|`{ FIXED: MIN([Index of Multiple Deprivation 2019 score - Scotland base])}`|
|GB level IMD score - Wales base|Maximum per full dataset|GB max of IMD score - England base|`{ FIXED: MAX([Index of Multiple Deprivation 2019 score - Wales base])}`|
|GB level IMD score - Wales base|Minimum per full dataset|GB min of IMD score - England base|`{ FIXED: MIN([Index of Multiple Deprivation 2019 score - Wales base])}`|
