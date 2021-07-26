# Notes on DERI tool and methodology - v1.0
## Contents
* [Introduction](#introduction)
* [Background](#background)
* [Version 1.0](#version-10)
* [Data inclusion](#data-inclusion)
* [Geographic choice](#geographic-choice)
  * [Converting OA to LSOA data](#converting-oa-to-lsoa-data)
* [Calculating each indicator score](#calculating-each-indicator-score)
* [Calculating component scores](#calculating-component-scores)
* [Calculating the DERI score](#calculating-the-deri-score)
* [Presenting the information](#presenting-the-information)

---

## Introduction
Version 1.0 of the Digital Exclusion Risk Index (DERI) tool is an online series of Tableau dashboards that aim to highlight the risk of digital exclusion at a lower super output area geography. These notes represent some of the considerations, calculations and decisions relating to the creation of version 1.0 of the tool. It is designed to complement both the [methodology document](DERI%20Score%20Methodology_v1.0.md) and the [Tableau develeopment document](Tableau%20development_v1.0.md) in this repository. It highlights important considerations for this version of the tool, and the divergences from the original tool developed by Salford on which this tool is based.

## Background
In 2020, Salford City Council created a Digital Exclusion Risk Index to visualise the areas in Salford at risk of digital exclusion. The tool was built in PowerBI, and showcased to a wider group of digital inclusion leads across Greater Manchester. Many other districts were building or considering building a similar tool with a similar approach. At the same time, digital inclusion leads at the Greater Manchester Combined Authority (GMCA) have engaged with leads across the UK, and identified similar work being explored or developed by other parties. It was therefore suggested that GMCA attempt to expand the Digital Exclusion Risk Index nationally.

Initial discussions with Salford identified a methodology and approach, as well as their consent to expand the tool nationally. GMCA took on the task of creating a new DERI tool in mid-March 2021, and the first version of the tool was released at the end of March 2021.

The aim of this work is to provide a single, coherent understanding of the risk of digital exclusion, and to iteratively develop this work with relevant feedback on issues such as usability, datasets, calculations and visualisations.

This note, and the accompanying [methodology](DERI%20Score%20Methodology_v1.md) and [Tableau development notes](Tableau%20development_v1.md), explain the process in developing a first version of the DERI tool. Feedback on the first version will be collated, and used to produce a note for an updated version of the tool.

## Version 1.0
Version 1.0 of the tool is designed as a simple, proof-of-concept version of the tool, visualising very basic information: dashboards showing the final DERI score for each LSOA, and each of the components of the final DERI score. It marks the first created version utilising a simple set of data, and was designed to produce something that could be tested with users. It is also designed to show information for all of England, at the least.

While the overall aim is to create a methodology and tool that is applicable to all of England and Wales, this first version acts as a starting point from which to develop the tool and methodology further. It is not a finalised project.

## Data inclusion
The data used is that indicated in the [data sources document](Data%20sources_v1.0.csv). That includes:
* Proportion of population aged 65+ (ONS Mid-year population estimates)
* Proportion of population aged 75+ (ONS Mid-year population estimates)
* Proportion of over 65 residents on guaranteed Pension Credit (DWP benefit claimants)
* Proportion of 16+ population with no qualifications (ONS Census 2011)
* Alternative unemployment rate (DWP Claimant count)
* Index of Multiple Deprivation score (MHCLG)
* Proportion of homes unable to receive 30MBit/s broadband (Ofcom Connected Nations)
* Proportion of connections receiving less than 10MBit/s (Ofcom Connected Nations)
* Average download speed (Ofcom Connected Nations)

Three indicators from the original Salford approach are not currently available. Two datasets were specific to Salford (proportion of contacts with the council made online, and proportion of council tax bills paid online), while one has not been released openly by ONS (a digital 'hard to count' score, identifying the areas with a propensity to respond to the Census online). The first two of these might be difficult to replicate nationally, as there is no consistent standard for these datasets. Information provided by ONS suggests that this dataset will be released after the Census, and as such cannot be easily integrated into version 1. However, it may be useful to explore other related activity datasets.

> **DECISION:** Version 1.0 will not include an activity component, and therefore diverges from the original Salford approach. Notes for this are available in our [methodology document](DERI%20Score%20Methodology_v1.md).

> **DECISION:** We will explore integrating the digital hard to count score, or a related dataset, in a future version of the methodology and tool.

> **DECISION:** We will discuss with local partners which additional measures might be included, and aim to understand any correlation between these measures. 

## Geographic choice
Almost all datasets used are provided on a lower super output area, or output area basis. For more information on these geographies, [see the ONS webpage on Census geographies](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeography#super-output-area-soa). While not every ward name or geography will change each year, they do change more often than OA and LSOA geographies, which are set in Census years. The year-to-year change, over time, makes ward level boundaries useful at a local level (i.e. local authority level), but more difficult to use when looking at data over multiple time periods and across the nation. The view is that the DERI tool will aim to be updated and be made available for all areas of England at a minimum.

Furthermore, while OAs and LSOAs align neatly - i.e. an LSOA is composed of several OAs - wards do not always follow LSOA and OA boundaries. Therefore, using lookups to match LSOA or OA data to wards will not always provide a direct match, and has the potential for variance year-to-year.

> **DECISION:** Version 1.0 will focus on data at the LSOA level, and will convert OA data to LSOA level.

Nevertheless, it is important to consider how potential users of the tool might perceive areas. LSOAs and OAs, for example, use simple names and codes (e.g. E010002345), which may not be beneficial for users wanting to understand areas. It is therefore prudent to consider the geography that best aligns with user's needs and perceptions.

> **DECISION:** We will explore which geographies are best to present the DERI scores. 

### Converting OA to LSOA data
The Ofcom data for broadband is available at an OA level. To provide LSOA level data, we first ran a vlookup on the data in Excel to match each OA with an LSOA, using [the ONS' OA to LSOA lookups](https://geoportal.statistics.gov.uk/datasets/output-area-to-lower-layer-super-output-area-to-middle-layer-super-output-area-to-local-authority-district-december-2011-lookup-in-england-and-wales).

To identify the proportions of connections under 10MBit/s, we:
* Pivoted the data to create sums of the number of connections and the number of connections under 10MBit/s for each LSOA.
* Divided the LSOA number of connections under 10MBit/s by the total number of connections in the LSOA (both calculated above).

For the proportion of homes unable to receive 30MBit/s, a similar approach was used.

For the average download speed per LSOA, we:
* Multiplied the average download speed for each OA by the number of connections in that OA.
* Pivoted the data, and summed the multiplied figures for each LSOA.
* Divided the total sum by the total number of connections for each LSOA to provide an average download speed. 

## Calculating each indicator score
Each indicator score is given as a number from 0 to 10, indicating the relative position of each indicator in each LSOA to the maximum and minimum values of the indicator. A more detailed explanation is given in the [methodology document](DERI%20Score%20Methodology_v1.md).

As indicated in the [methodology document](DERI%20Score%20Methodology_v1.md), there are several approaches to potentially calculating the indicator score:
1. Using the entire population's minimum and maximum values, thereby creating a fixed, absolute score for each indicator, for each LSOA. By this approach, LSOA A and LSOA B, both in different districts, would attain the same average download speed score if they had the same average download speed.
2. Using the maximum and minimum of a fixed subset, such as that of a local authority, to calculate an absolute score for each indicator, for each LSOA. By this approach, LSOA A and LSOA B _could_ attain different scores for their average download speed, even if the average download speed was the same.
3. Using the maximum and minimum values of a varying set, chosen by the user. In this case, the advantages of using Tableau or other dashboard tools means that the calculation for this can be automatically updated. In the case of LSOAs A and B, they would only attain the same average download speed score if they were both in the chosen set of the user AND if their average download speed was the same. Otherwise, their scores would vary.

> **DECISION:** For Version 1.0, the second option will be applied, as this provides a useful view at the local level, and a wider city-regional, county, or regional level.

> **DECISION:** We will explore with partners which of the different options might provide a better view of digital exclusion.

> **DECISION:** We will explore with partners whether a log calculation might be a better option for creating scores.

In some insatnces, data was unavailable. Often this is due to small counts (thereby protecting individuals or individual households from information disclosure). In these instances, a value of zero was assumed.

> **DECISION:** For datasets with null or suppressed values, the value of zero is assumed.

In other instances, data was simply unavailable from the chosen dataset. For example, the Indices of Deprivation used are the English Indices of Deprivation. While comparable, the Welsh Indices of Deprivation have not currently been used. In this case, an overall DERI score cannot be calculated, and as such these areas are filtered out from the dashboard views in the tool. However, the Welsh data is included in other component score dashboards where the data is available.

> **DECISION:** Where a component or overall DERI score cannot be calculated, the 'null' field is filtered out of the view.

> **DECISION:** We will explore with partners how this additional data might be included, and where data is not comparable, what datasets might be used to form a comparable basis.

## Calculating component scores
The component score calculations are set out in the methodology document. With the exception of the aforementioned lack of data for activity, each of the components follow a similar methodology to the original work by Salford.

> **DECISION:** The data sources and proposed weightings for each indicator (shown in the [methodology document](DERI%20Score%20Methodology_v1.0.md)) will be the same as those in the original Salford work as default.

> **DECISION:** There will not be an activity component in version 1.0 of the tool.

The development of a component score and DERI tool for the nation, however, means that different areas may have a different focus for their digital inclusion activities. For example, one area may be concerned more with digital exclusion based on age, whereas others may consider access to broadband as a key consideration. It is therefore important that the tool allows users to weight the different indicators and components as they would choose to do.

> **DECISION:** Version 1.0 of the tool will allow users to change the weighting of different components and indicators in the final score. However, the default values will be those in the [methodology document](DERI%20Score%20Methodology_v1.0.md).

## Calculating the DERI score
The DERI Score is calculated using a similar method to the component scores: a weighted sum of lower level scores. In the case of the overall DERI score, this is a weighted sum of the component scores; whereas the component scores were a weighted sum of indicator scores. The decision was made to weight each of the three component scores in this DERI tool equally (i.e. 33% each). Practically, however, the parameters used in the Tableau tool are integers, and as such the weightings are 33-33-34, to sum to 100.

> **DECISION:** The weightings of the components will be parameters, of values 33, 33 and 34 for age, broadband and deprivation.

## Presenting the information
We needed to consider how users might interact with the information. It was felt that a list / table of areas would not be beneficial, given the methodology uses LSOAs. LSOAs have simple codes and names that do not reflect commonly used names of areas, in the same way that wards might. Furthermore, a list of LSOAs might be considerably long if there are multiple areas chosen in the tool.

> **DECISION:** The tool will not include a table showing a list of LSOAs.

In terms of presenting the information, the aim of making a national DERI tool is to provide comparison and to see neighbouring / surrounding areas on a similar basis. As such, it was decided that the tool should allow users to choose multiple areas to view. However, this should be available at a sensible geography - a list of LSOAs would be extensive, and as mentioned above, not as valuable in identifying areas as wards might be.

> **DECISION:** Version 1.0 of the tool will allow users to choose the areas they want to focus on.

> **DECISION:** The tool will use local authority areas as a way to filter and visualise the data. This means that users will be able to choose 'Bolton', as an example, and all LSOAs in Bolton will appear on screen.

It was felt that a map format, given that this shows the risk in different areas, would be beneficial to visualise the data. Additionally, the tool should show the variability of the overall DERI score, and the component scores, within the chosen areas. Both of these methods of visualisation should be aligned, so that choosing or hovering over an LSOA in one visualisation highlights it in the other visualisation (e.g. hovering over an LSOA in the map highlights the LSOA on a graph).

> **DECISION:** The tool will use a map to highlight the main data.
> **DECISION:** The tool will use a graph to highlight the variability in data in the chosen area(s).

A further important consideration is to make the information, and the tool, as accessible as possible. This means three things:
1. The data, guides, decisions and methodology should be made open for others to use.
2. The tool itself should be accessible by all, and not in a closed system.
3. The tool and data should be accessible by all types of users, including those requiring support to access content on the internet.

We have attempted to ensure this is the case, by providing these documents openly, using Tableau server to present the dashboards, and considering accessibility requirements in the creation of the dashboard (e.g. colours appropriate for those with colour vision deficiency (colour blindness).

> **DECISION:** The data, notes, data sources and methodology of the tool should be made open.

> **DECISION:** The tool should use Tableau server to present the data, and the link be accessible to all.

> **DECISION:** The tool should try to be as accessible as possible to all users, focusing on key accessibility requirements.
