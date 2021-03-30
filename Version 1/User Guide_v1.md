# User Guide - Version 1

## Contents
* [Introduction](#introduction)
* [Accessing the tool](#accessing-the-tool)
* [Home page](#home-page)
 * [Navigation](#navigation)
* [User guide page](#user-guide-page)
* [Individual dashboards](#individual-dashboards)
  * [Area filter](#area-filter)
  * [Marker graph](#marker-graph)
  * [Area score](#area-score)
  * [Map](#map)
* [How might you want to use the tool?](#how-might-you-want-to-use-the-tool)

---

## Introduction
This document complements the [methodology document](DERI%20Score%20Methodology_v1.md) for version 1 of the Tableau tool. It explains how users can utilise the tool, and what each element of the online tool does.

## Accessing the tool
The tool can be accessed through the main Tableau server link provided by email. For the first few versions of this tool, this link will not be shared openly. Rather, it will be shared with partners to help develop this before a better version is released for wider public use.

There are 6 parts of the tool:
* A home page, with a short description of the tool.
* A user guide
* A DERI score dashboard
* An age component dashboard
* A broadband component dashboard
* A deprivation component dashboard

## Home page
The first page is a 'home page' (DERI home page). It provides links to the tool guide and the four dashboards that makes up the tool. It provides a short description of the dashboards and the DERI score. The DERI score is a risk index, providing a number between 0 and 10. When the number is closer to ten, the risk of digital exclusion is higher; when the number is closer to 0, the risk is lower. For each of the components - also scored 0 to 10 - the score represents the risk of digital exclusion associated with that theme: age, deprivation, or broadband speeds and access.

### Navigation
Individual navigation buttons in the home page direct users to the individual dashboards or the user guide. However, users can also use the tabs at the very top of every page in the tool, above the page title.

Each dashboard and page, with the exception of the home page, includes a link button that takes users back to the home page. The aim of this is to reduce clutter and stop users from having multiple buttons directing them throughout the dashboard.

## User guide page
The user guide page provides a simple image of the DERI dashboard, highlighting all of the relevant components of the dashboard, which are replicated through each of the four dashboards.

## Individual dashboards
There are four dashboards in the online tool. The first, the DERI Score dashboard, focuses on the overall DERI score for each LSOA. The remaining dashboards focus on the individual components of the DERI score - age, broadband, and deprivation. Each of the dashboards is built in much the same way, although each draws on different data and present different information.

### Area filter
The first major component of each dashboard is the area filter, which sits beneath the dashboard title. This filter allows a user to choose one or more relevant local authorities, or to choose all local authorities. The local authority filter is at a district level, and so a view of county, city-regional, regional or other areas will require a choice of all individual districts within. The filter action applies to both the [map](#map) and the [marker graph](#marker-graph).

The filter is presented as a multi-choice dropdown. This allows users to choose more than one local authority. However, the calculation method for the DERI score, each of the components, and each of the indicators, is based on the maximum and minimum values of each local authority. Therefore, viewing the data at a larger area requires an understanding of the DERI methodology. Areas with similar individual indicator values may have very different DERI and component scores. Indeed, as the LSOA scores are based on the maximum and minimum values of LSOAs in each district, it may be that two LSOAs in separate districts have exactly the same indicator _values_ but significantly different indicator _scores_. For more information on this, see the [area score section below](#area-score). Therefore, choosing two or more districts will provide a view of each individual district's LSOA scores, rather than a score based on the maximum and minimum of all areas chosen.

This filter also applies to all dashboards. This means that if a district is chosen in one dashboard, moving to the next dashboard will also show the same local authority area.

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

### Other components
There are several other components to each dashboard that are added to the dashboard for usability or clarity.

#### Weightings
Each dashboard shows the relevant weightings for the score presented on the dashboard. The DERI score dashboard, for example, shows the weightings of the different components that make up the score; while the component dashboards show the weightings of the individual indicator scores within it.

The weightings are shown in a collapsible box, floating on the top right of the map. To hide the weightings, click the 'Hide score weightings' button at the top of the weightings, and to open them again, click the 'Edit score weighting button' that appears in its place.

Each weighting is a parameter that affects the score of each component, and therefore the overall DERI score. If you make a change to a weighting for an indicator score in a component dashboard, this will affect the DERI score in the DERI dashboard.

Weightings are set at default settings, and are available in the [methodology note](DERI%20Score%20Methodology_v1.md). The weightings are presented as sliders, which can be altered by the user to alter the different weightings of components and indicators. The sliders move an integer at a time, between 0(%) and 100(%). Once a change is made, the tool will automatically update the relevant scores throughout the dashboard, which may take a moment.

#### Warning
Weightings within each dashboard need to sum to 100, otherwise some component or indicator scores may be pushed beyond 10. If they do not sum - either they are too low or too high - then a warning will appear below the weightings to explain this. This warning is currently only visible in the expandable weightings container. 

#### Legend
A legend also appears in the bottom left of the map. This legend shows the colour coding used for the map, graph and LSOA score for each dashboard. This legend is set: 0 is a dark blue, and 10 is a dark red.

## How might you want to use the tool?
There are many different options for using the tool. Users may want to:
* See their locality scores: this can be done by accessing the relevant dashboard and choosing their locality in the area filter.
* Compare their area against another: this can be done by choosing the relevant areas in the area filter at the top of each dashboard.
* Understand digital exclusion relating to a particular component: individual component dashboards allow users to see relevant risk indices for age, deprivation and broadband access and speed.
* Re-weight the scores to understand a particular conmponent's impact on the DERI score: this can be done using the weightings section in each dashboard.
* Understand local or regional hotspots: by choosing one or more areas, users can see using the colour coding, graph, map and score, the areas that are at highest risk in each locality of experiencing digital exclusion.

It is important, however, to note what the DERI tool cannot be used for. To take an example, imagine a user wanted to understand the top ten areas at risk of digital exclusion in Greater Manchester. This tool would only show _within each district_ which areas were at risk of digital inclusion. Choosing all ten districts in Greater Manchester and identifying those with the top ten highest DERI scores would not show those at the highest risk of digital exclusion within Greater Manchester. If the risk of digital exclusion was based on maximum and minimum values within all of Greater Manchester, this would elicit different LSOAs at risk than the current approach, which is based on the maximum and minimum values _within each district_.
