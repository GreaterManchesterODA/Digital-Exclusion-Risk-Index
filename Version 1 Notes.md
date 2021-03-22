# DERI Tool - Version 1 Notes

## Introduction


## Background


## Version 1
Version 1 of the tool is designed as a simple version of the tool, showing the very basic information: dashboards showing the final DERI score for each LSOA, and each of the digital exclusion components. It marks the first created version utilising a simple set of data, and was designed to produce something that could be tested with users.

It is also designed to show information for all of England, at the least. This expands the work from the original focus, which provided inofrmation for Salford only.

## Data inclusion
The data used is that indicated in the source document. That includes:
* Proportion of population aged 65+ (ONS Mid-year population estimates)
* Proportion of population aged 75+ (ONS Mid-year population estimates)
* Proportion of over 65 residents on guaranteed Pension Credit (DWP benefit claimants)
* Proportion of 16+ population with no qualifications (ONS Census 2011)
* Alternative unemployment rate (DWP Claimant count)
* Index of Multiple Deprivation score (MHCLG)
* Proportion of homes unable to receive 30MBit/s broadband (Ofcom Connected Nations)
* Proportion of connections receiving less than 10MBit/s (Ofcom Connected Nations)
* Average download speed (Ofcom Connected Nations)

However, the Digital Hard to Count score is not currently released by ONS. It has been shared individually with Census managers, but collating this information nationally would be difficult. Information provided by ONS suggests that this dataset will be released after the Census, and as such cannot be easily integrated into version 1.

> **DECISION:** Version 1 will not include an activity component, and therefore diverges from the [Methodology document](Methodology.md) and the [Data sources document](Data_sources.csv).

## Geographic choice
Almost all datasets originally used are provided on a lower super output area, or output area basis. For more information on these geographies, [see the ONS webpage on Census geographies](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeography#super-output-area-soa). While the original tool was developed on a ward basis, wards tend to be revised at least once a year. While not every ward name or geography will change each year, they do change more often than OA and LSOA geographies, which are set in Census years. The year-to-year change, over time, makes ward level boundaries useful at a local level (i.e. local authority level), but more difficult to use when looking at data over multiple time periods and across the nation. The view is that the DERI tool will aim to be updated and be made available for all areas of England at a minimum.

Furthermore, while OAs and LSOAs align neatly - i.e. an LSOA is composed of several OAs - wards do not always follow LSOA and OA boundaries. Therefore, using lookups to match LSOA or OA data to wards will not always provide a direct match, and has the potential for variance year-to-year.

> **DECISION:** Version 1 will focus on data at the LSOA level, and will convert OA data to LSOA level.

The Ofcom data for broadband is available at an OA level. To provide LSOA level data, we first ran a vlookup on the data in Excel to match each OA with an LSOA, using the ONS' OA to LSOA lookups.

To identify the proportions of connections under 10MBit/s, we:
* Pivoted the data to create sums of the number of connections and the number of connections under 10MBit/s for each LSOA.
* Divided the LSOA number of connections under 10MBit/s by the total number of connections in the LSOA (both calculated above).

For the proportion of homes unable to receive 30MBit/s, a similar approach was used.

For the average download speed per LSOA, we:
* Multiplied the average download speed for each OA by the number of connections in that OA.
* Pivoted the data, and summed the multiplied figures for each LSOA.
* Divided the total sum by the total number of connections for each LSOA to provide an average download speed. 

## Calculating each indicator score
As indicated in the methodology document, there are several approaches to potentially calculating the indicator score:
1. Using the entire population's minimum and maximum values, thereby creating a fixed, absolute score for each indicator, for each LSOA. By this approach, LSOA A and LSOA B, both in different districts, would attain the same average download speed score if they had the same average download speed.
2. Using the maximum and minimum of a fixed subset, such as that of a local authority, to calculate an absolute score for each indicator, for each LSOA. By this approach, LSOA A and LSOA B _could_ attain different scores for their average download speed, even if the average download speed was the same.
3. Using the maximum and minimum values of a varying set, chosen by the user. In this case, the advantages of using Tableau or other dashboard tools means that the calculation for this can be automatically updated. In the case of LSOAs A and B, they would only attain the same average download speed score if they were both in the chosen set of the user AND if their average download speed was the same. Otherwise, their scores would vary.

> **DECISION:**  

### Indicator scores

### Weightings and parameters

### Component scores

### Final DERI score

## Additional calculated fields

## Maps

## Charts and tables

## Additional sheets

## Dashboard creation
