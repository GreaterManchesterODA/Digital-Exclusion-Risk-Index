# Updates to Version 1.3

Our main updates to [Version 1.3](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_3/DERIhomepage?%3Aiid=1&%3AisGuestRedirectFromVizportal=y&%3Aembed=y) have been:
* Adding in data for Scotland to ensure we have coverage of Great Britain
* Using Scottish Data Zones as comparators for LSOAs in England and Wales

## Adding Scottish data
As with the data for England and Wales, the Scottish data included is:
* Proportion of population aged 65+ (National Records of Scotland Mid-year population estimates)
* Proportion of population aged 75+ (National Records of Scotland Mid-year population estimates)
* Proportion of over 65 residents on guaranteed Pension Credit (DWP benefit claimants)
* Proportion of 16+ population with no qualifications (ONS Census 2011)
* Alternative unemployment rate (DWP Claimant count)
* Index of Multiple Deprivation score (mySociety Great Britain IMD index)
* Proportion of homes unable to receive 30MBit/s broadband (Ofcom Connected Nations)
* Proportion of connections receiving less than 10MBit/s (Ofcom Connected Nations)
* Average download speed (Ofcom Connected Nations)

The full data source details are available in the [data sources v1.3](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.3/Data%20sources_v1.3.csv) document

## Using Scottish Data Zones
As LSOA boundaries only apply to England and Wales, Scottish Data Zone boundaries were used as comparators for the purposes of the DERI tool. The Data Zone boundaries were downloaded in Shapefile format from [SpatialData.gov.scot](https://www.spatialdata.gov.scot/geonetwork/srv/api/records/7d3e8709-98fa-4d71-867c-d5c8293823f2#:~:text=The%20finalised%20set%20of%20boundaries%20consists%20of%206%2C976,previous%202001%20codes%20ranged%20from%20S01000001%20to%20S01006505%29.) and merged with the LSOA Shapefile for England and Wales using QGIS software. 
