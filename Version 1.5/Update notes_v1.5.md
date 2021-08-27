# Updates to Version 1.5

[Version 1.5](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_5/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y) contained two main updates:
* Calculating a version of the Index of Multiple Deprivation score based on each of the English, Welsh and Scottish methodologies
* Adding functionality to the dashboards to allow users to select the English, Welsh or Scottish calculation

## Calculating English, Welsh and Scottish IMD scores
Each of the English, Welsh and Scottish IMD scores use slightly different metrics and methodologies so they are not directly comparable. This means that a score of x on the English IMD should not be construed as comparable to the same score on the Welsh or Scottish IMD scale. However, a few years ago a group of researchers set out to come up with a coherent deprivation score by mapping between the various domains. This work has been recently updated and is [published here](https://github.com/mysociety/composite_uk_imd), along with reflective discussion about how to use the scores and what their limitations are.

This repository includes a different composite IMD file for each nation, in which that nation has been used as the calculation base and all other scores are aligned with that nation's scores. The guidance for the comosite IMD is to use the data corresponding to the primary area of focus. Given that the DERI tool is available for users in all three nations, we felt it was necessary to provide users with the option to select the IMD score that corresponds to their area.

The repository has UK indices and GB indices. We have used the GB set of data as the DERI tool currently only looks at England, Wales and Scotland. The links below show where we sourced each dataset from within the composite IMD repository:
* [English IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_E.csv)
* [Welsh IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_W.csv)
* [Scottish IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_S.csv)

### Tableau calculations for the IMD scores
The process for calculating the separate IMD scores within the DERI tool followed the same steps as the original [indicator score methodology](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.0/DERI%20Score%20Methodology_v1.0.md#individual-indicator-scores).

In summary, the mins and maxes will first need to be calculated for each of the English, Welsh and Scottish IMD figures, fixed separately at Local Authority, nation, and Great Britain level. This will lead to 9 new calculated fields for the maxes and 9 new calculated fields for the mins. As an example, the `National max of IMD score - English base` would need the following calculated field:

`{FIXED [Nation] : MAX([Index of Multiple Deprivation 2019 score - England base])}`

Once all of these calculated fields have been created, they can be used to calculate 9 sets of scores to feed into the DERI tool - an English, Scottish and Welsh IMD score based on Local Authority, National, and Great Britain mins and maxes. As an example, the Great Britain level score using the Welsh IMD methodology would be calculated as follows:

`10*([Index of Multiple Deprivation 2019 score - Wales base]-[GB min of IMD score - Wales base])/([GB max of IMD score - Wales base]-[GB min of IMD score - Wales base])`

## Adding functionality to choose the IMD score base within the dashboards
In order to select different IMD scores within the dashboards, a new parameter and set of calculated fields must be created. These must then be added into the dashboard to allow the users to select the different options.

### Parameter
Create a parameter called `IMD: England / Scotland / Wales` with `Data type: String` and `Values of: England, Scotland, Wales`

### Interim calculated fields
To bring the England / Wales / Scotland options into the main component scores that feed into the dashboards, three interim calculated fields are needed: one for the IMD scores at Local Authority level, one at national level, and one at Great Britain level. As an example, the Great Britain interim calculated field would look like:

`CASE [IMD: England / Scotland / Wales]`

`WHEN "England" THEN [GB score: IMD score (England)]`

`WHEN "Scotland" THEN [GB score: IMD score (Scotland)]`

`WHEN "Wales" THEN [GB score: IMD score (Wales)]`

`END`

This calculated field can then form the basis of the IMD score within the main calculated field for the `Deprivation component (GB)`. This will allow the score to be controlled by both the `IMD: England /Scotland / Wales` parameter and the `Local / national / GB score` parameter (from [Version 1.4](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.4/Update%20notes_v1.4.md)) simultaneously. 

### Adding the parameter to the dashboards
The addition of the different calculation bases for the Index of Multiple Deprivation score impacts the deprivation component and feeds through to the overall DERI score. Therefore the `IMD: England / Scotland / Wales` parameter needs to be added to both the 'Deprivation Score dashboard' and the 'DERI Score dashboard'. 
