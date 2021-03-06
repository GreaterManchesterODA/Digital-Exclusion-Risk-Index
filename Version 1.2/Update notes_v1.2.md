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

Ward boundaries were downloaded from the [ONS Open Geography portal](https://geoportal.statistics.gov.uk/datasets/wards-december-2020-uk-bfc-v2/explore?location=55.340000%2C-3.316939%2C6.09). These were matched to Local Authority districts in order to map them against the LSOAs within Tableau. The process for joining in Tableau was as follows:
1. Add the Ward boundary shapefile to the Tableau workbook.
2. Create a full outer join between the LSOA boundary shapefile and the Ward boundary shapefile with a join clause of '1 = 0'. This makes a union of the two files but where no columns are the same.
3. Create a dual axis map where one marks card has LSOA geometry and one has ward geometry. Ensure that the Ward marks card is layered underneath the LSOA marks card in order to avoid losing the functionality of hovering over the map to see LSOA scores.
4. Created a calculated field of 'IFNULL([LA name from LSOA], [LA name from Wards])' and use this as a universal filter.

## Changing the weightings methodology
