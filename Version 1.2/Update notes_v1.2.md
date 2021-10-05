# Updates to Version 1.2

[Version 1.2](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_2/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y) of the Digital Exclusion Risk Index included three main changes:
1. Adding data for Welsh LSOAs
2. Adding ward boundary overlays to the map
3. Changing the calculation and methodology behind the weightings

## Adding Welsh data

The data that was added for Wales is indicated in the [data sources v1.2](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.2/Data%20sources_v1.2.csv) document. As with the existing English data used in the tool, the Welsh data includes:
* Proportion of population aged 65+ (ONS Mid-year population estimates)
* Proportion of population aged 75+ (ONS Mid-year population estimates)
* Proportion of over 65 residents on guaranteed Pension Credit (DWP benefit claimants)
* Proportion of 16+ population with no qualifications (ONS Census 2011)
* Alternative unemployment rate (DWP Claimant count)
* Index of Multiple Deprivation score (Welsh Government)
* Proportion of homes unable to receive 30MBit/s broadband (Ofcom Connected Nations)
* Proportion of connections receiving less than 10MBit/s (Ofcom Connected Nations)
* Average download speed (Ofcom Connected Nations)

## Adding ward boundaries

Feedback from versions 1.0 and 1.1 indicated that users would benefit from seeing ward boundaries as well as LSOA boundaries, as wards tend to have more meaningful names than LSOAs and would provide additional context. In order to bring wards into the DERI tool, ward boundaries were downloaded from the [ONS Open Geography portal](https://geoportal.statistics.gov.uk/datasets/wards-december-2020-uk-bfc-v2/explore?location=55.340000%2C-3.316939%2C6.09). These were matched to Local Authority districts in order to map them against the LSOAs within Tableau. The process for joining in Tableau was as follows:
1. Added the Ward boundary shapefile to the Tableau workbook.
2. Created a full outer join between the LSOA boundary shapefile and the Ward boundary shapefile with a join clause of '1 = 0'. This makes a union of the two files but where no columns are the same.
3. Created a dual axis map where one marks card has LSOA geometry and one has ward geometry.
4. Layered the Ward marks card underneath the LSOA marks card. This ensures that the user is able to see LSOA scores when hovering over the map.
5. Created a calculated field of 'IFNULL([LA name from LSOA], [LA name from Wards])' and used this as a universal filter.


## Changing the weightings methodology

Feedback from versions 1.0 and 1.1 indicated that the weightings were too precise and this made them difficult to use. As a result, we simplified the weightings to be on a scale of 0-10 rather than 0-100. The new default values for each parameter are shown in the table below:
|Parameter name|Type|Applied to|Default value|
|---|---|---|---|
|Weighting: % with no quals|Indicator weighting|Percentage of residents aged 16+ with no qualifications|4|
|Weighting: 65+|Indicator weighting|Percentage of population aged 65 and over|5|
|Weighting: 75+|Indicator weighting|Percentage of population aged 75 and over|5|
|Weighting: avg download speed|Indicator weighting|Average download speed (MBit/s)|3|
|Weighting: connections less than 10MBit/s|Indicator weighting|Percentage of connections receiving less than 10MBit/s|3|
|Weighting: guaranteed pension credit|Indicator weighting|Guaranteed pension credit (rate per 1,000 aged 65+)|2|
|Weighting: homes unable to receive 30MBit/s|Indicator weighting|Percentage of homes unable to receive at least 30MBit/s|3|
|Weighting: IMD score|Indicator weighting|Index of Multiple Deprivation 2019 score|2|
|Weighting: unemployment rate|Indicator weighting|Unemployment rate|2|
|Weighting: age component|Component weighting|Age component|3|
|Weighting: broadband component|Component weighting|Broadband component|3|
|Weighting: deprivation component|Component weighting|Deprivation component|3|

We also removed the weightings warning that displayed when the sum of the weightings exceeded 100, and changed the calculation behind the scores to be based on the parameter weighting as a proportion of the sum of parameter weightings within that component. The updated calculations for the component and DERI scores are shown in the table below:
|Component name|Component calculation|
|---|---|
|Age component|`([Score: percentage of population aged 65+]*(([Weighting: 65+]/([Weighting: 65+]+[Weighting: 75+])))+([Score: percentage of population aged 75+]*(([Weighting: 75+]/([Weighting: 65+]+[Weighting: 75+])))`|
|Broadband component|`([Score: percentage of connections receiving less than 10MBit/s]*([Weighting: connections less than 10MBit/s]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))+([Score: percentage of homes unable to receive at least 30MBit/s]*([Weighting: homes unable to receive 30MBit/s]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))+([Score: average download speed]*([Weighting: avg download speed]/([Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s]+[Weighting: avg download speed])))`|
|Deprivation component|`([Score: unemployment rate]*([Weighting: unemployment rate]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([Score: percentage of residents aged 16+ with no qualifications]*([Weighting: % no quals]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([Score: guaranteed pension credit]*([Weighting: guaranteed pension credit]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))+([Score: Index of Multiple Deprivation score]*([Weighting: IMD score]/([Weighting: unemployment rate]+[Weighting: % no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score])))`|
|DERI score|`([Age component]*([Weighting: age component]/([Weighting: age component]+[Weighting: broadband component]+[Weighting: deprivation component])))+([Broadband component]*([Weighting: broadband component]/([Weighting: age component]+[Weighting: broadband component]+[Weighting: deprivation component])))+([Deprivation component]*([Weighting: deprivation component]/([Weighting: age component]+[Weighting: broadband component]+[Weighting: deprivation component])))`|
