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

These two data sources were loaded into Tableau, with an inner join based on the LSOA code.

The following table lists the data source fields:
Field name|Information contained|Source
ObjectId||
Lsoa11Cd||
Lsoa11Nm||
BngE||
BngN||
Long||
Lat||
Shape_Len||
Share_Are||
Geometry||
Local authority code||
Local authority name||
LSOA code||
LSOA name||
Region Code||
Region Name||
Combined Authority Code||
Combined Authority Name||
County code||
County name||
Total population||
Aged 16+||
Aged 65+||
Aged 75+||
Percentage of homes unable to receive at least 30MBit/s||
Average download speed (MBit/s)||
Percentage of connections receiving less than 10MBit/s||
Percentage of population aged 65 and over||
Percentage of population aged 75 and over||
Percentage of residents aged 16+ with no qualifications||
Guaranteed pension credit (rate per 1,000 aged 65+)||
Index of Multiple Deprivation 2019 score||
Unemployment rate||

### Indicator scores

Indicator|Calculated field name|Calculation score
Percentage of homes unable to receive at least 30MBit/s||
Average download speed (MBit/s)||
Percentage of connections receiving less than 10MBit/s||
Percentage of population aged 65 and over||
Percentage of population aged 75 and over||
Percentage of residents aged 16+ with no qualifications||
Guaranteed pension credit (rate per 1,000 aged 65+)||
Index of Multiple Deprivation 2019 score||
Unemployment rate||

### Weightings and parameters

### Component scores

### Final DERI score

## Additional calculated fields

## Maps

## Charts and tables

## Additional sheets

## Dashboard creation
