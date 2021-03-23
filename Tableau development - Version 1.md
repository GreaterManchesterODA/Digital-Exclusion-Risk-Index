# Tableau development - Version 1

## Introduction
This document sets out the processes used to create version 1 of the Digital Exclusion Risk Index on Tableau. In comparison to the version 1 notes, which details the considerations and issues in calculatng and building the tool, this document sets out how one might build exactly the same tool in Tableau.

It covers the data input to version 1 of the tool, the calculated fields, the sheets created and the final dashboard.

The aim of this development document is to update users so that they can also create a similar tool using their own data, or to recreate the DERI tool in full.

## Tableau versions
There are two versions of Tableau that have been used to create the tool. The first is v2018.3.4. This was used for the creation of much of the original tool. However, newer versions provide additional elements that are beneficial for different components of the tool. As a result, at a later stage a new v.2020.xx was used.

## Data
There are two data sources for the tool: a shapefile of LSOAs, and a dataset with relevant LSOA level data.

The first is the 2011 LSOA boundary shapefile from ONS, [available here](https://geoportal.statistics.gov.uk/datasets/lower-layer-super-output-areas-december-2011-boundaries-full-clipped-bfc-ew-v3?geometry=-16.993%2C50.522%2C12.648%2C55.161). The full, clipped boundary is chosen for the LSOAs, to clip the LSOAs to the land.

The second was created by GMCA, by sourcing all the relevant data and adding into a single Excel spreadsheet. The dataset includes only the indicator values, and relevant denominators, such as the total 16+ population. Whilst scores can be calculated in Excel and input to the dataset, it was felt that an approach that built the measurements in Tableau would be more beneficial, as they would update automatically if any changes needed to be made to the base dataset. Similarly, this also keeps the core dataset clean for other users, who may want to create their own calculations.

Furthermore, we added additional geographic information for each LSOA to the dataset. This was done using the lookup

These two data sources were loaded into Tableau, with an inner join based on the LSOA code.

## Indicator scores
Each indicator value was used to calculate a score between 0 and 10. The aim of this is to provide a range of normalised scores that can be weighted and combined to create a single Digital Exclusion Risk Index. The calculation for each of the indicators was marginally different. Each score was created in Tableau as a calculated field. As highlighted in the [version 1 notes](Version%201%20Notes.md), the decision was made to fix elements of the calculation. Each LSOA score was based on the maximum and minimum LSOA values of the district it sits within. This means that two LSOAs with the same indicator values in two separate districts may have different scores - they will be dependent on different maxima and minima.

### Maximum and minimum calculations
In order to create the minimum of each district's LSOA values, the calculation needs to be fixed at the local authority level. For each indicator score, it is possible to include this element within the calculation in Tableau. However, to cut down on the amount of typing and complexity of each calculation, it was decided to create calculated fields for the maximum and minimum values of each indicator for each LSOA in each district.

The standard calculation used for each 'maximum' field was:

`{ FIXED [Local authority name]: MAX([indicator])}`

where `[indicator]` is the the particular indicator field (identified in Appendix A below).

Similarly, the calculation used for the 'minimum' field was:

`{ FIXED [Local authority name]: MIN([indicator])}`

In total, 18 calculated fields were created - one minimum and one maximum calculated field for each indicator. The full list of calculated fields and calculations is presented in Appendix B.

## Calculating scores
Using the minimum and maximum value calculated fields mentioned above, individual scores between 0 and 10 can be created for each indicator.

### Weightings and parameters

### Component scores

### Final DERI score

## Additional calculated fields

## Maps

## Charts and tables

## Additional sheets

## Dashboard creation

## Appendix A: Fields in the inner joined Tableau data sources
The following table lists the joined data source fields. The two sources are the shapefile and the master spreadsheet created by GMCA.

|Field name|Information contained|Source|
|---|---|---|
|ObjectId|General ID for each polygon in the shapefile|Shapefile|
|Lsoa11Cd|The 2011 ONS code for each LSOA|Shapefile|
|Lsoa11Nm|The 2011 ONS name for each LSOA|Shapefile|
|BngE|Eastings of the centre point of the LSOA (British National Grid)|Shapefile|
|BngN|Northings of the centre point of the LSOA (British National Grid)|Shapefile|
|Long|Longitude of the centre point of the LSOA|Shapefile|
|Lat|Latitude of the centre point of the LSOA|Shapefile|
|Shape_Len|Length of the boundary of the LSOA in metres|Shapefile|
|Share_Are|Area contained by the LSOA in square metres|Shapefile|
|Geometry|Identifies the type of shape each LSOA is (e.g. polygon or multipolygon)|Shapefile|
|Local authority code|The 2020 ONS code for the district that each LSOA is in|Master spreadsheet|
|Local authority name|The 2020 ONS name for the district that each LSOA is in|Master spreadsheet|
|LSOA code|The 2011 ONS code for each LSOA|Master spreadsheet|
|LSOA name|The 2011 ONS name for each LSOA|Master spreadsheet|
|Region Code|The 2020 ONS code for the region that each LSOA is in|Master spreadsheet|
|Region Name|The 2020 ONS name for the region that each LSOA is in|Master spreadsheet|
|Combined Authority Code|The 2020 ONS code for the combined authority that each LSOA is in (not all LSOAs are within a Combined Authority area)|Master spreadsheet|
|Combined Authority Name|The 2020 ONS name for the combined authority that each LSOA is in (not all LSOAs are within a Combined Authority area)|Master spreadsheet|
|County code|The 2020 ONS code for the county that each LSOA is in|Master spreadsheet|
|County name|The 2020 ONS name for the county that each LSOA is in|Master spreadsheet|
|Total population|Total population from 2019 mid-year population estimates from ONS|Master spreadsheet|
|Aged 16+|Total population aged 16+ from 2019 mid-year population estimates from ONS|Master spreadsheet|
|Aged 65+|Total population aged 65+ from 2019 mid-year population estimates from ONS|Master spreadsheet|
|Aged 75+|Total population aged 75+ from 2019 mid-year population estimates from ONS|Master spreadsheet|
|Percentage of homes unable to receive at least 30MBit/s|Percentage of homes unable to receive at least 30MBit/s in each LSOA|Master spreadsheet|
|Average download speed (MBit/s)|Average download speed (MBit/s) for each LSOA|Master spreadsheet|
|Percentage of connections receiving less than 10MBit/s|Percentage of connections receiving less than 10MBit/s in each LSOA|Master spreadsheet|
|Percentage of population aged 65 and over|Percentage of population aged 65 and over from ONS 2019 mid-year population estimates for each LSOA|Master spreadsheet|
|Percentage of population aged 75 and over|Percentage of population aged 75 and over from ONS 2019 mid-year population estimates for each LSOA|Master spreadsheet|
|Percentage of residents aged 16+ with no qualifications|Percentage of residents aged 16+ with no qualifications from 2011 Census for each LSOA|Master spreadsheet|
|Guaranteed pension credit (rate per 1,000 aged 65+)|Number of claimants receiving guaranteed pension credit per LSOA for every 1,000 residents aged 65+ in each LSOA|Master spreadsheet|
|Index of Multiple Deprivation 2019 score|LSOA-level score from the 2019 English Indices of Deprivation|Master spreadsheet|
|Unemployment rate|Percentage of the adult population in each LSOA counted as 'unemployed'|Master spreadsheet|

## Appendix B: Calculations for maximum and minimum fields

|Indicator|Type|Calculated field name|Calculation|
|---|---|---|---|
|Percentage of homes unable to receive at least 30MBit/s|Maximum per district|Max of Percentage of homes unable to receive at least 30MBit/s|`{ FIXED [Local authority name]: MAX([Percentage of homes unable to receive at least 30Mbit/s broadband])}`|
|Percentage of homes unable to receive at least 30MBit/s|Minimum per district|Min of Percentage of homes unable to receive at least 30MBit/s|`{ FIXED [Local authority name]: MIN([Percentage of homes unable to receive at least 30Mbit/s broadband])}`|
|Average download speed (MBit/s)|Maximum per district|Max of Average download speed|`{ FIXED [Local authority name]: MAX([Average download speed (Mbit/s)])}`|
|Average download speed (MBit/s)|Minimum per district|Min of Average download speed|`{ FIXED [Local authority name]: MIN([Average download speed (Mbit/s)])}`|
|Percentage of connections receiving less than 10MBit/s|Maximum per district|Max of Percentage of connections less than 10MBit/s|`{ FIXED [Local authority name]: MAX([Percentage of connections receiving less than 10MBit/s])}`|
|Percentage of connections receiving less than 10MBit/s|Minimum per district|Min of Percentage of connections less than 10MBit/s|`{ FIXED [Local authority name]: MIN([Percentage of connections receiving less than 10MBit/s])}`|
|Percentage of population aged 65 and over|Maximum per district|Max of Percentage of population aged 65+|`{ FIXED [Local authority name]: MAX([Percentage of population aged 65 and over])}`|
|Percentage of population aged 65 and over|Minimum per district|Min of Percentage of population aged 65+|`{ FIXED [Local authority name]: MIN([Percentage of population aged 65 and over])}`|
|Percentage of population aged 75 and over|Maximum per district|Max of Percentage of population aged 75+|`{ FIXED [Local authority name]: MAX([Percentage of population aged 75 and over])}`|
|Percentage of population aged 75 and over|Minimum per district|Min of Percentage of population aged 75+|`{ FIXED [Local authority name]: MIN([Percentage of population aged 75 and over])}`|
|Percentage of residents aged 16+ with no qualifications|Maximum per district|Max of Percentage of residents with no qualifications|`{ FIXED [Local authority name]: MAX([Percentage of residents aged 16+ with no qualifications])}`|
|Percentage of residents aged 16+ with no qualifications|Minimum per district|Min of Percentage of residents with no qualifications|`{ FIXED [Local authority name]: MIN([Percentage of residents aged 16+ with no qualifications])}`|
|Guaranteed pension credit (rate per 1,000 aged 65+)|Maximum per district|Max of Guaranteed Pension Credit|`{ FIXED [Local authority name]: MAX([Guaranteed pension credit (rate per 1,000 aged 65+)])}`|
|Guaranteed pension credit (rate per 1,000 aged 65+)|Minimum per district|Max of Guaranteed Pension Credit|`{ FIXED [Local authority name]: MIN([Guaranteed pension credit (rate per 1,000 aged 65+)])}`|
|Index of Multiple Deprivation 2019 score|Maximum per district|Max of Index of Multiple Deprivation Score|`{ FIXED [Local authority name]: MAX([Index of Multiple Deprivation 2019 score])}`|
|Index of Multiple Deprivation 2019 score|Minimum per district|Min of Index of Multiple Deprivation Score|`{ FIXED [Local authority name]: MIN([Index of Multiple Deprivation 2019 score])}`|
|Unemployment rate|Maximum per district|Max of Unemployment rate|`{ FIXED [Local authority name]: MAX([Unemployment rate])}`|
|Unemployment rate|Minimum per district|Min of Unemployment rate|`{ FIXED [Local authority name]: MIN([Unemployment rate])}`|

