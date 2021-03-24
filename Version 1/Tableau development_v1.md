# Tableau development - Version 1

## Contents
* [Introduction](#introduction)
* [Tableau versions](#tableau-versions)
* [Data](#data)
* [Indicator scores](#indicator-scores)
 * [Maximum and minimum calculations](#maximum-and-minimum-calculations)
 * [Calculating indicator scores](#calculating-indicator-scores)
* [Component scores](#component-scores)
 * [Weightings and parameters](#weightings-and-parameters)
 * [Calculating component scores](#calculating-component-scores)
* [Final DERI score](#final-deri-score)
* [Additional calculated fields](#additional-calculated-fields)
* [Sheets](#sheets)
 * [Maps](#maps)
  * [Example: DERI Score map creation](#example-deri-score-map-creation)
 * [Charts](#charts)
  * [Example: DERI Score chart creation](#example-deri-score-chart-creation)
 * [Additional sheets](#additional-sheets)
  * [Example: LSOA Text](#example-lsoa-text)
  * [Example: DERI Score Text](#example-deri-score-text)
* [Dashboard creation](#dashboard-creation)
  * [Example: DERI Score Dashboard](#example-deri-score-dashboard)
 * [Dashboard actions and filter](#dashboard-actions-and-filter)
* [Appendix A: Fields in the inner joined Tableau data sources](#appendix-a-fields-in-the-inner-joined-tableau-data-sources)
* [Appendix B: Calculations for maximum and minimum fields](#appendix-b-calculations-for-maximum-and-minimum-fields)
* [Appendix C: Individual indicator scores](#appendix-c-individual-indicator-scores)
* [Appendix D: Weighting parameters](#appendix-d-weighting-parameters)
* [Appendix E: Component score calculations](#appendix-e-component-score-calculations)
* [Appendix F: Weighting warning calculated fields](#appendix-f-weighting-warning-calculated-fields)
* [Appendix G: Dashboard actions](#appendix-g-dashboard-actions)

---

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

### Calculating indicator scores
Using the minimum and maximum value calculated fields mentioned above, individual scores between 0 and 10 can be created for each indicator. In most instances, a higher indicator value is assumed to relate to a higher risk of digital exclusion. Therefore, the calculation identifies where on the scale between the minimum and maximum values in the district each LSOA lies. The highest value would receive a score of 10, and the lowest value a score of 0. A value halfway between the highest and lowest values would gain a score of 5.

The general calculation for this was:
`10*([indicator value]-[Min of indicator])/([Max of indicator]-[Min of indicator])`
where `[indicator value]` is the value of the the indicator for each LSOA, and `[Max of indicator]` and `[Min of indicator]` represent the maximum and minimums of that indicator, as mentioned above.

However, one indicator - the average download speed - was associated with higher risk of digital exclusion. As average broadband speeds are lower, there is a risk that many homes will have low speed connections that might be underutilised. In this instance, the calculation is reversed: when average broadband speeds are low, the score needs to be high, and vice versa:
`10*([Max of indicator]-[indicator value])/([Max of indicator]-[Min of indicator])`

There are no log functions used in the calculation. This is something we may explore in future. A log function would help to identify if it may be harder to reach a higher value. For example, it may be more difficult to reduce down an unemployment rate from 1% to 0% than it would be to reduce it from 10% to 9%.

A full list of indicator score calculations is provided in Appendix C.

## Component scores
The next stage of the process is to create component scores. These component scores are based on the sum of weighted indicator scores. Only three component scores were created for this version of the tool:
* Age component: composed of the over 65 and over 75 indicator scores.
* Broadband component: composed of the homes unable to receive at least 30MBit/s, connections below 10MBit/s, and average download speed scores.
* Deprivation component: composed of the Index of Multiple Deprivation, Pension Credit, no qualifications, and unemployment rate scores.

The weightings are originally derived from the Salford work, but to fit with this model, some changes have been made.

### Weightings and parameters
One concern with expanding the Salford version of the tool to other areas is the choice of weightings used. Different areas might have different priorities, and as such may want to weight both the individual scores and the component scores. As such, it was decided that the weightings in the first version of the tool would not be fixed. Instead, they would be created using a parameter that can be applied and altered by the user.

To create each component score, weightings are applied to each indicator score. Furthermore, to create the final DERI score, weightings are applied to the component scores. Twelve parameters were created for the tool - one for each indicator score, and one for each component score. Each parameter had the following features:
* **Data type:** Integer
* **Display format:** Automatic
* **Allowable values:** Range
* **Minimum:** 0
* **Maximum:** 100

The decision was made to create these as an integer between 0 and 100, with the weightings within one component calculation, or the calculation for the overall DERI score, to sum to 100. One issue here is that, in using integers, we have applied integers where the original Salford tool may have implemented a decimal (e.g. 33.3). In this case, we have altered the weightings so that they always sum to 100.

A full list of parameters and weightings is available in Appendix D. This includes the weightings applied to both indicator scores and component scores.

### Calculating component scores
The general calculation method for each component score is:
`(Indicator score A * (Indicator score A weighting)/100) + (Indicator score B * (Indicator score B weighting)/100) + ...`

This weighted sum is applied to all of the relevant indicators for each component to produce a component score.

A full list of component score calculations is presented in Appendix E.

## Final DERI score
The final DERI score is composed of the three component scores, weighted and summed. The weightings, presented as parameters in Tableau, are shown in Appendix D, and the component scores in Appendix E. This approach contrasts with the original Salford tool, as one component area - activity - is not included. As such, the weighting for all components is equal in this version of the tool (with the exception that the weighting is an integer, and so the values are 33, 33 and 34).

The calculation for the final DERI score is:
`([Age component]*([Weighting: age component]/100)) + ([Broadband component]*([Weighting: broadband component]/100)) + ([Deprivation component]*([Weighting: deprivation component]/100))`

## Additional calculated fields
There are four more calculated fields created in Tableau. These four are listed in Appendix F. They are text outputs that take different weightings as an input. When the relevant weightings do not sum to 100, the text output of the calculated field is a warning that summed weightings should equal 100.

## Sheets
The final Tableau tool is composed of several dashboards. Each of these dashboards is itself composed of several sheets. This section sets out the different sheets created, and the content of these sheets. Choices of colour are not covered here, but it is sensible to include accessible colours as a way of showing change / variance in scores.

### Maps
Four maps were created for the Tableau tool:
* Overall DERI score map
* Age component map
* Broadband component
* Deprivation component

Each map uses a similar range of data. An example using the DERI score is presented below to explain how each map was created.

#### Example: DERI Score map creation
1. Add the `Geometry` field of the LSOAs to the 'Detail' element, with the geometry measure as 'collect'. `Longitude (generated)` and `Latitude (generated)` are automatically populated in the columns and rows respectively.
2. Add the `Local authority name` field to the filter shelf.
3. Choose to 'Show the filter', and change the filter type to 'Multiple values (dropdown)'.
4. Add the `LSOA code` and `LSOA name` fields to the 'Detail' element.
5. Add the `DERI score` field to the 'Color' element, which will automatically provide a sum as the measure.
6. At this point, the map should be a map of LSOAs coloured by the `DERI score` field.
7. Edit the colours and title in the 'Sum(DERI score)' legend that appears. Click the 'Advanced' button and set the minimum value to 0 and maximum value to 10.
8. Choose to 'Show Parameter Control' for each of the relevant weighting parameters. In this case, they are `Weighting: age component`, `Weighting: broadband component`, and `Weighting: deprivation component`.

Following the above, and substituting in the relevant data for other maps will create sufficient maps to be used in the final dashboard. They will be filtered by the chosen areas in the filter.

### Charts
A chart was also created for each of the component scores and the overall DERI score. Each chart shows where each LSOA in the chosen local authority sits on a scale of 0 to 10. Each chart is similar, but an example of how to create this is again presented below for the DERI score.

#### Example: DERI Score chart creation
1. Add the `DERI score` field to the 'Columns' area.
2. Add the `DERI score` field to the 'Filters' shelf. In the popup box that appears, choose 'Sum' then 'Next. In the next popup make this a range of values with a minimum of 0 and a maximum of 10.
3. Add the `Local authority name` field to the 'Filters' shelf. Choose 'All' and click OK.
4. Add the `LSOA name` and `LSOA code` fields to the 'Details' element.
5. Add the `DERI score` field to the 'Colours' element. Style the colours similar to the map, to ensure consistency, with a max of 10 and a min of 0.
6. In the 'Marks' shelf, under the dropdown menu, choose 'Gantt Bar' option.

The above will provide a chart of individual marks for each LSOA at their score level. To recreate the other charts, you will need to update the `DERI score` field with the relevant component calculated fields.

### Additional sheets
Five further text-based sheets were also created for addition to the dashboards. These were:
* **LSOA Text:** a sheet showing the `LSOA code` and `LSOA name` fields relating to the LSOA being viewed / selected on the map / chart.
* **DERI Score Text:** shows the value of the `DERI score` field, colour-coded, of the LSOA being viewed / selected on the map / chart.
* **Age Score Text:** shows the value of the `Age component` field, colour-coded, of the LSOA being viewed / selected on the map / chart.
* **Broadband Score Text:** shows the value of the `Broadband component` field, colour-coded, of the LSOA being viewed / selected on the map / chart.
* **Deprivation Score Text:** shows the value of the `Deprivation component` field, colour-coded, of the LSOA being viewed / selected on the map / chart.

The two examples below show how to make the 'LSOA Text' sheet and the 'DERI Score Text' sheet. The latter can be copied, with minor adjustments, to create the remaining three sheets.

#### Example: LSOA Text
1. Add `LSOA code` and `LSOA name` to the Text element.
2. Reformat the text so that it would be small enough to read, with the format `LSOA code` : `LSOA name`.

#### Example: DERI Score Text
1. Add the `DERI Score` field to the 'Text' element.
2. Reformat and resize the score.
3. Add the `DERI Score` field to the 'Colors' element.
4. Change the colours to match those in the map and graph, with a minimum of 0 and a maximum of 10.

## Dashboard creation
There are 6 dashboards that make up the tool:
1. Home page / introduction
2. How to use the DERI tool
3. DERI Score dashboard
4. Age Score Dashboard
5. Broadband Score Dashboard
6. Deprivation Score Dashboard

Dashboard 3 - 6 are effectively similar. They are styled in the same way, but use different graphs and maps.

#### Example: DERI Score Dashboard
The dashboard contains the following sheets: LSOA Text; DERI Score Text; Map of DERI Score; DERI Score graph; and DERI weighting warning. Additionally, there are five text boxes, two image boxes, a floating legend, a tiled filter and the relevant weightings for the dashboard.

The dashboard is arranged in both floating and tiled formats. The tiled format is arranged in the following way:
* Vertical
  * Horizontal
    * Text box: title of the dashboard
  * Horizontal: simple line separator
  * Filter: this is the map filter to choose a local authority
  * Horizontal
    * Vertical
      * LSOA Text
      * DERI Score Text
    * Horizontal
      * Text box: 'Low risk' - this is placed at the start of the graph
      * DERI Score graph
      * Text box: 'High risk' - this is placed at the end of the graph
  * Map of DERI Score
  * Horizontal
    * Text box: 'Based on original work by:'
    * Image: Salford City Council logo
    * Text box: 'Produced by'
    * Image: GM ODA logo

The score colour range is placed as a floating container in the top left of the map. This highlights the colours of the relevant areas.

Additionally, the weighting parameters and the 'DERI weighting warning' sheet are held in a floating vertical container.

A button has been added at the bottom, to provide a link back to the home dashboard.

This dashboard can be recreated for the component scores, substituting in the graphs, maps, weightings and warnings for that score.

### Dashboard actions and filter
A range of dashboard actions were created for each dashboard. The first action run is that the local authority filter from the first map applies to all worksheets using the same data source.

There are six dashboard actions in each dashboard. Two filters, which alter the 'LSOA Text' and relevant 'Score Text' sheets; and four highlighters to highlight the map and the chart when LSOAs are selected or hovered over. Appendix G sets out all the dashboard actions created.

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

## Appendix C: Individual indicator scores
|Score name|Score calculation|
|---|---|
|Score: average download speed|`10*([Max of Average download speed]-[Average download speed (Mbit/s)])/([Max of Average download speed]-[Min of Average download speed])`|
|Score: guaranteed pension credit|`10*([Guaranteed pension credit (rate per 1,000 aged 65+)]-[Min of Guaranteed Pension Credit])/([Max of Guaranteed Pension Credit]-[Min of Guaranteed Pension Credit])`|
|Score: Index of Multiple Deprivation score|`10*([Index of Multiple Deprivation 2019 score]-[Min of Index of Multiple Deprivation Score])/([Max of Index of Multiple Deprivation Score]-[Min of Index of Multiple Deprivation Score])`|
|Score: percentage of connections receiving less than 10MBit/s|`10*([Percentage of connections receiving less than 10Mbit/s broadband]-[Min of Percentage of connections less than 10MBit/s])/([Max of Percentage of connections less than 10MBit/s]-[Min of Percentage of connections less than 10MBit/s])`|
|Score: percentage of homes unable to receive at least 30MBit/s|`10*([Percentage of homes unable to receive at least 30Mbit/s broadband]-[Min of Percentage of homes unable to receive at least 30MBit/s])/([Max of Percentage of homes unable to receive at least 30MBit/s]-[Min of Percentage of homes unable to receive at least 30MBit/s])`|
|Score: percentage of population aged 65+|`10*([Percentage of population aged 65 and over]-[Min of Percentage of population aged 65+])/([Max of Percentage of population aged 65+]-[Min of Percentage of population aged 65+])`|
|Score: percentage of population aged 75+|`10*([Percentage of population aged 75 and over]-[Min of Percentage of population aged 75+])/([Max of Percentage of population aged 75+]-[Min of Percentage of population aged 75+])`|
|Score: percentage of residents aged 16+ with no qualifications|`10*([Percentage of residents aged 16+ with no qualifications]-[Min of Percentage of residents with no qualifications])/([Max of Percentage of residents with no qualifications]-[Min of Percentage of residents with no qualifications])`|
|Score: unemployment rate|`10*([Unemployment rate]-[Min of Unemployment rate])/([Max of Unemployment rate]-[Min of Unemployment rate])`|

## Appendix D: Weighting parameters
|Parameter name|Type|Applied to|Default value|
|---|---|---|---|
|Weighting: % with no quals|Indicator weighting|Percentage of residents aged 16+ with no qualifications|40|
|Weighting: 65+|Indicator weighting|Percentage of population aged 65 and over|50|
|Weighting: 75+|Indicator weighting|Percentage of population aged 75 and over|50|
|Weighting: avg download speed|Indicator weighting|Average download speed (MBit/s)|33|
|Weighting: connections less than 10MBit/s|Indicator weighting|Percentage of connections receiving less than 10MBit/s|33|
|Weighting: guaranteed pension credit|Indicator weighting|Guaranteed pension credit (rate per 1,000 aged 65+)|20|
|Weighting: homes unable to receive 30MBit/s|Indicator weighting|Percentage of homes unable to receive at least 30MBit/s|34|
|Weighting: IMD score|Indicator weighting|Index of Multiple Deprivation 2019 score|20|
|Weighting: unemployment rate|Indicator weighting|Unemployment rate|20|
|Weighting: age component|Component weighting|Age component|33|
|Weighting: broadband component|Component weighting|Broadband component|33|
|Weighting: deprivation component|Component weighting|Deprivation component|34|

## Appendix E: Component score calculations
|Component name|Component calculation|
|---|---|
|Age component|`([Score: percentage of population aged 65+]*([Weighting: 65+]/100))+([Score: percentage of population aged 75+]*([Weighting: 75+]/100))`|
|Broadband component|`([Score: percentage of connections receiving less than 10MBit/s]*([Weighting: connections less than 10MBit/s]/100)) +([Score: percentage of homes unable to receive at least 30MBit/s]*([Weighting: homes unable to receive 30MBit/s]/100)) +([Score: average download speed]*([Weighting: avg download speed]/100))`|
|Deprivation component|`([Score: unemployment rate]*([Weighting: unemployment rate]/100)) + ([Score: percentage of residents aged 16+ with no qualifications]*([Weighting: % with no quals]/100)) + ([Score: guaranteed pension credit]*([Weighting: guaranteed pension credit]/100)) + ([Score: Index of Multiple Deprivation score]*([Weighting: IMD score]/100))`|

## Appendix F: Weighting warning calculated fields
|Warning name|Warning calculation|
|---|---|
|Warning: DERI weighting|`IF ([Weighting: age component]+[Weighting: broadband component]+[Weighting: deprivation component])!=100 THEN 'Warning: Weightings need to sum to 100.' END`|
|Warning: Age component weighting|`IF ([Weighting: 65+]+[Weighting: 75+])!=100 THEN 'Warning: Weightings need to sum to 100.' END`|
|Warning: Broadband component weighting|`IF ([Weighting: avg download speed]+[Weighting: connections less than 10MBit/s]+[Weighting: homes unable to receive 30MBit/s])!=100 THEN 'Warning: Weightings need to sum to 100.' END`|
|Warning: Deprivation component weighting|`IF ([Weighting: % with no quals]+[Weighting: guaranteed pension credit]+[Weighting: IMD score]+[Weighting: unemployment rate])!=100 THEN 'Warning: Weightings need to sum to 100.' END`|

## Appendix G: Dashboard actions
|Action title|Type|Run on|Source sheet(s)|Target sheet(s)|Clearing the selection will...|
|---|---|---|---|---|---|
|Filter DERI score based on hover over map|Filter|Hover|DERI Score graph; Map of DERI score|DERI Score Text; LSOA Text|Leave the filter|
|Filter DERI score based on selected area|Filter|Select|DERI Score graph; Map of DERI score|DERI Score Text; LSOA Text|Leave the filter|
|Highlight DERI map based on graph hover|Highlight|Hover|DERI Score graph|Map of DERI score||
|Highlight DERI score graph on map hover|Highlight|Hover|Map of DERI score|DERI Score graph||
|Highlight DERI map based on graph selection|Highlight|Select|DERI Score graph|Map of DERI score||
|Highlight DERI score graph on map selection|Highlight|Select|Map of DERI score|DERI Score graph||
|Filter Age score based on hover over map|Filter|Hover|Age Score graph; Map of Age score|Age Score Text; LSOA Text|Leave the filter|
|Filter Age score based on selected area|Filter|Select|Age Score graph; Map of Age score|Age Score Text; LSOA Text|Leave the filter|
|Highlight Age map based on graph hover|Highlight|Hover|Age Score graph|Map of Age score||
|Highlight Age score graph on map hover|Highlight|Hover|Map of Age score|Age Score graph||
|Highlight Age map based on graph selection|Highlight|Select|Age Score graph|Map of Age score||
|Highlight Age score graph on map selection|Highlight|Select|Map of Age score|Age Score graph||
|Filter Broadband score based on hover over map|Filter|Hover|Broadband Score graph; Map of Broadband score|Broadband Score Text; LSOA Text|Leave the filter|
|Filter Broadband score based on selected area|Filter|Select|Broadband Score graph; Map of Broadband score|Broadband Score Text; LSOA Text|Leave the filter|
|Highlight Broadband map based on graph hover|Highlight|Hover|Broadband Score graph|Map of Broadband score||
|Highlight Broadband score graph on map hover|Highlight|Hover|Map of Broadband score|Broadband Score graph||
|Highlight Broadband map based on graph selection|Highlight|Select|Broadband Score graph|Map of Broadband score||
|Highlight Broadband score graph on map selection|Highlight|Select|Map of Broadband score|Broadband Score graph||
|Filter Deprivation score based on hover over map|Filter|Hover|Deprivation Score graph; Map of Deprivation score|Deprivation Score Text; LSOA Text|Leave the filter|
|Filter Deprivation score based on selected area|Filter|Select|Deprivation Score graph; Map of Deprivation score|Deprivation Score Text; LSOA Text|Leave the filter|
|Highlight Deprivation map based on graph hover|Highlight|Hover|Deprivation Score graph|Map of Deprivation score||
|Highlight Deprivation score graph on map hover|Highlight|Hover|Map of Deprivation score|Deprivation Score graph||
|Highlight Deprivation map based on graph selection|Highlight|Select|Deprivation Score graph|Map of Deprivation score||
|Highlight Deprivation score graph on map selection|Highlight|Select|Map of Deprivation score|Deprivation Score graph||
