# Updates to Version 1.2

Version 1.2 of the Digital Exclusion Risk Index included three main changes:
1. Adding data for Welsh LSOAs
2. Adding ward boundary overlays to the map
3. Changing the calculation and methodology behind the weightings

## Adding Welsh data

The data that was added for Wales is indicated in the data sources v1.2 document. As with the existing English data used in the tool, the data includes:
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

Ward boundaries were downloaded from the ONS Open Geography portal. These were matched to Local Authority districts in order to map them against the LSOAs within Tableau. The process for joining in Tableau was as follows:
1. Add the Ward boundary shapefile to the Tableau workbook.
2. Create a full outer join between the LSOA boundary shapefile and the Ward boundary shapefile with a join clause of '1 = 0' (this makes a union of the two files but where no columns are the same.
3. Create a dual axis map where one marks card has LSOA geometry and one has ward geometry (ensure that the Ward marks card is layered underneath the LSOA marks card in order to avoid losing the functionality of hovering over the map to see LSOA scores).
4. Created a calculated field of 'IFNULL([LA name from LSOA], [LA name from Wards])' and use this as a universal filter.

## Changing the weightings methodology
