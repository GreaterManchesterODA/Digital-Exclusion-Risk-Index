# User Guide

***NOTE: This User Guide relates to the latest version of the Digital Exclusion Risk Index (v1.5). If you have any queries about using previous versions, please contact oda@greatermanchester-ca.gov.uk.***

## Introduction

### What is the DERI?
The Digital Exclusion Risk Index (DERI) is a dataset and accompanying tool that calculates and visualises a digital exclusion risk score for each LSOA<sup id="a1">[1](#f1)</sup> in Great Britain. The DERI score is a single number between 0 (low risk of digital exclusion) and 10 (high risk) and is composed of three component scores:
*	Deprivation – includes IMD, skills, and welfare recipients
*	Demography – includes information on disabled people and older residents
*	Digital connectivity – primarily focuses on broadband access

In total, 11 indicators are used. Each of these is normalised based on the maximum and minimum values of that indicator within the dataset. So, for example, if one LSOA has the highest rate of 65+ residents, it receives a score of 10; the LSOA with the lowest rate gets a score of 0. For each LSOA, each indicator is weighted and summed to produce the three components above. The components themselves are then weighted and summed to produce the final DERI score.

The DERI contains three different sets of calculations to normalise the indicators. The first set of calculations uses the maximum and minimum values of each indicator within each individual local authority. The second set uses the maximum and minimum indicator values within each nation in Great Britain (England, Scotland or Wales). The third set uses the maximum and minimum values within the full dataset, covering Great Britain as a whole. Users can select which set of calculations they want to see within the tool, depending on their area of interest, while the [dataset is also available on GitHub](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index).

### What problem is the DERI trying to solve?
There is no single, national dataset that identifies who is and isn’t digitally excluded. Policymakers and researchers therefore need to rely on proxy information, or on national surveys to give an indication of digital exclusion prevalence.

An additional difficulty is the multi-faceted nature of digital exclusion. That is, digital inclusion and exclusion are on a continuum of need and support. Therefore, to move from a national view of digital exclusion (through surveys like the [Lloyds Digital Consumer Index](https://www.lloydsbank.com/banking-with-us/whats-happening/consumer-digital-index.html), or [Ofcom surveys of internet usage](https://www.ofcom.org.uk/research-and-data/internet-and-on-demand-research/internet-use-and-attitudes)) to a more localised view, a different approach must be taken to support policymakers.

Multiple local authorities have approached this issue by focusing on digital exclusion risk. That is, rather than identifying whether an individual is or isn’t digitally excluded, the approaches focus on factors that are _associated with_ digital exclusion, but do not identify digital exclusion directly. These include age, disability, deprivation, broadband connectivity, poverty, and skills levels. For example, people aged 55 and over are more likely to be digitally excluded; but being aged 55 or over does not mean that you are digitally excluded. Each area has taken a different approach, using different datasets, but with a broad focus on these issues. Each of these approaches has been designed on a local basis, and often with local information that may not be open data or may not be consistent with other areas. Examples include proportions of residents who contact the council online; or proportions of residents who pay council tax bills online.

The [Greater Manchester Combined Authority](https://www.greatermanchester-ca.gov.uk/) (GMCA), working with partners in Greater Manchester, recognise the value in this approach and the need to expand locally derived approaches across the city region. GMCA agreed to take a single approach and expand it. One of the first risk indices was created by [Salford City Council](https://www.salford.gov.uk), and shared across Greater Manchester. Other councils, such as [Manchester City Council](https://www.manchester.gov.uk/) and [Westminster City Council](https://www.westminster.gov.uk/), have each created their own versions. The Salford risk index was taken as a template, and used to create an initial version for all of Greater Manchester by the GMCA.

It was quickly identified that there would be value in expanding this work nationally – first to England, and then Wales and Scotland. Many of the base datasets used to create the index were open datasets, available for England or across Great Britain, and could be incorporated into a national tool.

In expanding the tool, we have focused and refined the datasets and methodology used, working with partners around the country. These organisations include GM local authorities, [Cheshire West and Chester Council](https://www.cheshirewestandchester.gov.uk/home.aspx) and other [Co-operative Councils' Innovation Network](https://www.councils.coop/) members, [Glasgow City Council](https://glasgow.gov.uk/), [Westminster Council](https://www.westminster.gov.uk/), the [Local Government Association](https://www.local.gov.uk/), [Good Things Foundation](https://www.goodthingsfoundation.org/) and others.

The tool now covers all of England, Scotland and Wales, and focuses on Lower Super Output Area level detail, with a ward overlay. [These GitHub pages](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index) include an open methodology and dataset, shared for all to use.


## Using the tool

### Accessing the tool
The different versions of the tool can be accessed via the following links:
|Version|Tool link|Methodology, data and notes|
|---|---|---|
|Version 1.0|[Version 1.0 on Tableau](https://www.gmtableau.nhs.uk/#/site/GMCA/views/210325_DERI/DERIhomepage?:iid=1)|[Version 1.0 notes](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.0)|
|Version 1.1|[Version 1.1 on Tableau](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_1/DERIhomepage?%3AisGuestRedirectFromVizportal=y&%3Aembed=y)|[Version 1.1 notes](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.1)|
|Version 1.2|[Version 1.2 on Tableau](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_2/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y)|[Version 1.2 notes](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.2)|
|Version 1.3|[Version 1.3 on Tableau](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_3/DERIhomepage?%3Aiid=1&%3AisGuestRedirectFromVizportal=y&%3Aembed=y)|[Version 1.3 notes](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.3)|
|Version 1.4|[Version 1.4 on Tableau](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_4/DERIhomepage?:iid=2&:isGuestRedirectFromVizportal=y&:embed=y)|[Version 1.4 notes](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.4)|
|Version 1.5|[Version 1.5 on Tableau](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_5/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y)|[Version 1.5 notes](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.5)|

### Navigating around the tool
Each version of tool contains the following tabs, which are all Tableau dashboards and part of the same Tableau workbook:
* Summary home page
* Tool guide
* DERI score dashboard
* Demography component dashboard
* Digital connectivity component dashboard
* Deprivation component dashboard

The links in [the above section](#accessing-the-tool) navigate to the main home page for each version of the tool. From the home page, there are links to each of the other five pages - the tool guide, the DERI score dashboard, and the three component score dashboards. All of these links are displayed as white text on a dark grey background. Within each of the other five pages there are links back to the main home page, again displayed as white text on a dark grey background. This is to reduce page clutter, and support navigation.

Users are also able to navigate to each dashboard directly by clicking the relevant tab displayed in the bar along the top of the tool.

### Home page and user guide page
The first page of the DERI tool is a 'home page'. It provides links to the tool guide and the four dashboards that makes up the tool. It also provides a short description of the dashboards and the DERI score.

The user guide page follows the home page provides a simple image of the DERI dashboard, highlighting all of the relevant components of the dashboard, which are replicated through each of the four dashboards.

### The interactive dashboards
There are four interactive dashboards in the online tool. The first, the DERI Score dashboard, focuses on the overall DERI score for each LSOA.

The DERI score dashboard follows the same visual structure as the individual component dashboards, but the score displayed is built from the three component scores. As with the deprivation dashboard, the DERI score dashboard contains the additional drop down box for the IMD score methodology. This is because the IMD indicator forms part of the overall DERI score through its inclusion within the deprivation component.

The DERI score dashboard is linked directly to the component scores so that any changes to the weightings of individual indicators within the component dashboards will also update the DERI score.

By default, the DERI score dashboard will open with all three components equally weighted. However, the button on the top right hand corner of the map allows users to change the relative importance of each indicator. Where changes are made to the DERI score weighting, the scores and the associated visualisations (i.e. the map and graph) will be updated automatically.

The remaining dashboards focus on the individual components of the DERI score - demography, broadband access, and deprivation. Each of the dashboards is built in much the same way, although each draws on different data and present different information.

There are a number of key elements which remain the same on every dashboard:
* Title to show which dashboard is being displayed
* Drop down boxes to allow the users to select the following:
  * Local authority area(s)
  * Score calculation base (i.e. whether to base the scores on the minimum and maximum indicator values within either each local authority, each nation, or Great Britain)
* A graph to show the full range of values within the area(s) chosen from the local authority drop down box
* A map view to display the area(s) chosen from the local authority drop down box, which also contains the following features:
  * A legend to show the colour of scores from 0 to 10
  * Buttons in the top left hand corner to zoom in and out of the map or return to the default map view
  * A function in the top right hand corner that allows users to edit the score weighting by dragging a point along a slider bar for each indicator
* Coloured text to display the value of the score of the most recent LSOA selected (LSOAs are selected by hovering or clicking on the map or the graph)

There is an additional drop down box in both the deprivation score dashboard and the main DERI score dashboard. This allows users to choose whether to base the calculation for the Index of Multiple Deprivation score on the methodology from Scotland, England or Wales.

The map and the graph on each page are linked so that hovering or clicking anywhere on the map will highlight that same LSOA within the graph, and vice versa. When hovering or clicking on the map or graph, a tooltip box will appear to display the following information about the selected LSOA:
* LSOA code
* LSOA name
* Ward name
* Local authority name
* Nation
* Component score

### Area filter
The first major component of each dashboard is the area filter, which sits beneath the dashboard title. This filter allows a user to choose one or more relevant local authorities, or to choose all local authorities. The local authority filter is at a district level, and so a view of county, city-regional, regional or other areas will require a choice of all individual districts within. The filter action applies to both the [map](#map) and the [marker graph](#marker-graph).

The filter is presented as a multi-choice dropdown. This allows users to choose more than one local authority. However, the default [calculation method](#calculation-method-filter) for the DERI score, each of the components, and each of the indicators, is to use the maximum and minimum values of each local authority. Therefore, viewing the data at a larger area requires an understanding of the DERI methodology. Areas with similar individual indicator values may have very different DERI and component scores. Indeed, as the LSOA scores are based on the maximum and minimum values of LSOAs in each district, it may be that two LSOAs in separate districts have exactly the same indicator _values_ but significantly different indicator _scores_. For more information on this, see the [area score section below](#area-score). Therefore, choosing two or more districts will provide a view of each individual district's LSOA scores, rather than a score based on the maximum and minimum of all areas chosen.

This filter also applies to all dashboards. This means that if a district is chosen in one dashboard, moving to the next dashboard will also show the same local authority area.

### Calculation method filter
The calculation method filter allows you to choose which approach to take to calculating the DERI score, or relevant component score. There are three options:
**1. Local** - this method calculates the score for each indicator, for each LSOA, based on the maximum and minimum values of each indicator within each LSOA's district. This method provides a focus on the locality - what is the relative order of digital exclusion risk (low to high) for each LSOA within a district? It does not allowm for comparison across districts. That is, an LSOA with a risk score of 9 in one district is not comparable with an LSOA with a risk score of 9 in another district.
**2. National** - this method uses the maximum and minimum values of each indicator within each nation (England, Scotland, or Wales). This method provides a focus on the relevant nation, meaning that the relative risk position in each LSOA can be compared across district boundaries. That is, an LSOA in England with a risk score of 9 in one district will be equivalent to an LSOA in England with a risk score of 9 in another district. However, an LSOA with a risk score of 9 in England will not be comparable with an LSOA with a risk score of 9 in Scotland, or Wales.
**3. Great Britain** - this method uses the maximum and minimum values of each indicator across Great Britain. This means an LSOA in England with a risk score of 9 has the same risk of digital exclusion as an LSOA in Scotland, or an LSOA in Wales, with a risk score of 9.

### Marker graph
The marker graph appears under the area filter, to the right of the dashboard. The marker graph provides a view of the scores of each LSOA within the area of the district(s) chosen in the [filter](#area-filter). It ranges from 0 to 10, though these numbers are not shown on the graph directly. Rather, a value of 'low risk' to 'high risk' is shown at either end of the graph. The level of risk indicates the risk of digital exclusion in that area. The graph in each dashboard shows the LSOAs' relevant scores - age in the age dashboard, DERI score in the DERI dashboard etc. This means that an LSOA might have a high score in one dashboard, and a low score in another.

There is one mark (a short, vertical line) for each of the LSOAs. Each mark is colour coded from blue to red dependent on the relevant score - the DERI score in the DERI dashboard, and the individual component scores in the component dashboards. As above, it means that in one dashboard an LSOA might have one colour, but another colour in another dashboard.

The graph is filtered by the area dropdown above it. This means that if more than one district is chosen, more LSOA marks will be added to the graph relevant to the areas chosen.

Individual marks representing LSOAs can be selected. When they are, this acts as a highlight on the [map](#map) - the LSOA is highlighted and the other LSOAs are greyed out. Selection of an LSOA on the grpah also acts as a filter on the area on the [area score](#area-score) - the area score will update with the value of the relevant score for the dashboard. Furthermore, hovering over each of the LSOA marks on the grpah also highlights the areas on the map, and changes the value in the area score section.

Similarly, when an area of the map is selected, or hovered over, the graph relevant LSOA is highlighted in the graph.

### Area score
The area score is a small section below the area filter, to the left. It shows the LSOA name, LSOA code and relevant score (DERI or relevant component score). The score is colour coded between blue (score of 0) and red (score of 10).

The score, LSOA name and LSOA code are all changed by selecting or hovering over the LSOAs in the map or the graph.

### Map
The map is the central block on each dashboard. It visualises the LSOAs of the district chosen in the [filter](#area-filter), and colour codes each based on the score presented on the dashboard - e.g. the DERI score on the DERI dashboard, the age component score on the age component dashboard. The colour ranges from 0 (low risk) to 10 (high risk).

If an individual local authority is chosen in the area filter, the map will jump to that local authority area and show all lower super output areas within it. If more than one district is chosen, the map will expand to show all relevant LSOAs. The more districts that are chosen, the further out the map will zoom. Users can zoom in and out of the map to see more detail, using the + and - buttons in the top left of the map, by using a scroll function on a mouse, or by clicking the small right arrow in the map control panel and choosing the image of a rectangle with a magnifying glass. This last option allows you to specify an area to zoom to by creating a rectangle on the map.

Panning around the map can be done through holding down the left mouse button and dragging map to where you want to look. To return to a full view of the districts you have chosen, click the small image of a house ('Zoom home') in the top left of the map.

There are a number of tools on the map in addition to panning and zooming. Users can also search for areas in the top left of the map using the search function. This search function does not include all names of all areas, but roughly provides towns and cities in the UK as reference points.

The top left of the map also allows users to select multiple areas. The control panel for the map, in the top left of the map, has a small right arrow, which produces a sub-menu of features. There are five features:
* **Zoom area** - as noted above, this zooms to a chosen area on the map.
* **Pan** - this changes the cursor so that the user can move around the map by clicking and dragging.
* **Rectangle** - this allows a user to select a number of LSOAs using a rectangle. Clicking and dragging will select and highlight multiple LSOAs in the map.
* **Radial** - similar to the above, this selects and highlights LSOAs based on a circle emanating from a point; click and drag to enlarge the circle.
* **Lasso** - as with the above, this selects and highlights LSOAs, but does so on a basis of drawing the area to define the LSOAs.

Individually selecting LSOAs can also be done by clicking on an LSOA on the map, while selecting multiple LSOAs can be achieved by clicking on one LSOA and then holding down the Ctrl button on a keyboard and selecting the next LSOA. The action of selecting LSOAs highlights the LSOA(s) in the map AND in the marker graph above. However, due to the nature of the area score component, this is not updated. Rather, the area score element highlights only the last LSOA selected or hovered over.

The background map used is fairly simple, and does not provide major roads, location names or addresses. It does provide general physical geographic components (e.g. rivers, lakes) as a guide, however.

### Weightings
Each score - whether a component score, or the final DERI score - is composed of other individually weighted scores. The DERI score is composed of three weighted component scores, and the component scores are composed of multiple weighted indicator scores.

The DERI tool allows you to alter these weightings as you see fit. The weightings are shown in a collapsible box, floating on the top right of the map. To hide the weightings, click the 'Hide score weightings' button at the top of the weightings, and to open them again, click the 'Edit score weighting button' that appears in its place.

Each weighting is a parameter that affects the score of each component, and therefore the overall DERI score. If you make a change to a weighting for an indicator score in a component dashboard, this will affect the DERI score in the DERI dashboard.

Weightings are set at default settings, and are available in the [methodology note](DERI%20Score%20Methodology_v1.md) and subsequent updates. The weightings are presented as sliders, which can be altered by the user to alter the different weightings of components and indicators. The sliders move an integer at a time, between 0 (no weight) and 10 (high weight). Once a change is made, the tool will automatically update the relevant scores throughout the dashboard, which may take a moment.

The weightings are also relative to one another. That is, if three components have weightings of 1, 1, and 2, this is the same as weightings of 2, 2, and 4; or 3, 3, and 6. The overall score will not be affected if the relative value of the weightings remain the same. Similarly, if all weightings are 3, this will produce the same output as if all weightings were at 10. The only difference will occur if 0 values are used (e.g. weightings of 3, 3, and 3 are not the same as 0, 0, and 0). 

### Legend
A legend also appears in the bottom left of the map. This legend shows the colour coding used for the map, graph and LSOA score for each dashboard. This legend is set: 0 is a dark blue, and 10 is a dark red.

## How might you want to use the tool?
There are many different options for using the tool. Users may want to:
* See their locality's scores: this can be done by accessing the relevant dashboard and choosing their locality in the area filter.
* Compare their area against another: this can be done by choosing the relevant areas in the area filter at the top of each dashboard, and choosing the national or Great Britain calculation method.
* Understand digital exclusion relating to a particular component: individual component dashboards allow users to see relevant risk indices for age, deprivation and broadband access and speed. You can change the weighting of individual indicator scores, or the overall component scores.
* Re-weight the scores to understand a particular conmponent's impact on the DERI score: again, this can be done using the weightings section in each dashboard.
* Understand local or regional hotspots: by choosing one or more areas, users can see using the colour coding, graph, map and score, the areas that are at highest risk in each locality of experiencing digital exclusion.

For more discussion of the ways that you may or may not want to use the DERI tool and dataset, visit [the guide on how to, and how not to use the DERI tool](How%20to%20and%20how%20not%20to%20use%20the%20DERI.md).

---
<b id="f1">1</b> For England and Wales, the 2011 Census Lower Super Output Areas are used. For Scotland, the 2011 Data Zones are used. For the remainder of this document, the term 'LSOA' is used to represent LSOAs or Data Zones. [↩](#a1)
