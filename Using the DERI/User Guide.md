# User Guide

## Introduction

### What is the DERI 
The Digital Exclusion Risk Index (DERI) is a tool that creates a digital exclusion risk score for each LSOA in Great Britain. This score is a single number between 0 (low risk of digital exclusion) and 10 (high risk). This final DERI score is actually composed of three component scores:
*	Deprivation – includes IMD, skills, and welfare recipients
*	Demography – includes information on disabled people and older residents
*	Digital connectivity – primarily focuses on broadband access

In total, 11 indicators are used. Each of these is normalised based on the maximum and minimum values of that indicator within the dataset. So, for example, if one LSOA has the highest rate of 65+ residents, it receives a score of 10; the LSOA with the lowest rate gets a score of 0. These indicators are then weighted and summed to produce the three components above. The components themselves are then weighted and summed to produce the final DERI score.

The DERI contains three different sets of calculations to normalise the indicators. The first set of calculations uses the maximum and minimum values of each indicator within each individual local authority. The second set uses the maximum and minimum indicator values within each nation in Great Britain (England, Scotland and Wales). The third set uses the maximum and minimum values within the full dataset, covering Great Britain as a whole. Users can select which set of calculations they want to see within the tool, depending on their area of interest.

### What problem is the DERI trying to solve
There is no single, national dataset that identifies who is and isn’t digitally excluded. Policymakers and researchers therefore need to rely on proxy information, or on national surveys to give an indication of digital exclusion prevalence.

An additional difficulty is the multi-faceted nature of digital exclusion. That is, digital inclusion and exclusion are on a continuum of need and support. Therefore, to move from a national view of digital exclusion (through surveys like the Lloyds Digital Consumer Index, or Ofcom surveys of internet usage) to a more localised view, a different approach must be taken to support policymakers.

Multiple local authorities have approached this issue by focusing on digital exclusion risk. That is, rather than identifying whether an individual is or isn’t digitally excluded, the approaches focus on factors that are associated with digital exclusion, but do not identify digital exclusion directly. These include age, disability, deprivation, broadband connectivity, poverty, and skills levels. For example, people aged 55 and over are more likely to be digitally excluded; but being aged 55 or over does not mean that you are digitally excluded. Each area has taken a different approach, using different datasets, but with a broad focus on these issues. Each of these approaches has been designed on a local basis, and often with local information that may not be open data or may not be consistent with other areas. Examples include proportions of residents who contact the council online; or proportions of residents who pay council tax bills online.

The GMCA, working with partners in GM, recognise the value in this approach and the need to expand locally derived approaches across the city region. GMCA agreed to take a single approach and expand it. One of the first risk indices was created by Salford City Council, and shared across GM. Other councils, such as Manchester and Westminster, have each created their own versions. The Salford risk index was taken as a template, and used to create an initial version for all of Greater Manchester by the GMCA.

It was quickly identified that there would be value in expanding this work nationally – first to England, and then Wales and Scotland. Many of the base datasets used to create the index were open datasets, available nationally, and could be incorporated into a national tool.

In expanding the tool, we have focused and refined the tool and the datasets used, working with partners around GM and the country. These organisations include GM local authorities, Cheshire West and Chester Council, Glasgow City Council, Westminster Council, Local Government Association, Good Things Foundation and others.

The tool now covers all of England, Scotland and Wales and focuses on Lower Super Output Area level detail, with a ward overlay. These GitHub pages include an open methodology and dataset, shared for all to use.


## Using the tool

### Accessing the tool
The different versions of the tool can be accessed via the following links:
|Version|Link|
|---|---|
|Version 1.0|https://www.gmtableau.nhs.uk/#/site/GMCA/views/210325_DERI/DERIhomepage?:iid=1|
|Version 1.1|https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_1/DERIhomepage?%3AisGuestRedirectFromVizportal=y&%3Aembed=y|
|Version 1.2|https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_2/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y|
|Version 1.3|https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_3/DERIhomepage?%3Aiid=1&%3AisGuestRedirectFromVizportal=y&%3Aembed=y|
|Version 1.4|https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_4/DERIhomepage?:iid=2&:isGuestRedirectFromVizportal=y&:embed=y|
|Version 1.5|https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_5/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y|

### Navigating the tool
The tool contains the following dashboards:
* Summary home page
* Tool guide
* DERI score dashboard
* Demography component dashboard
* Digital connectivity component dashboard
* Deprivation component dashboard

The hyperlinks above navigate to the main DERI home page for each version of the tool. From the home page, there are links to each of the other 5 dashboards, all displayed as white text on a dark grey background. Within each of the other 5 dashboards there are links back to the main home page, again displayed as white text on a dark grey background.

Users are also able to navigate to each dashboard directly by clicking the relevant tab displayed in the bar along the top of the tool.

### Using the dashboards
Each component dashboard is set out in an identical format and has a number of key elements:
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

There is an additional drop down box in the deprivation dashboard for the IMD score methodology. This allows users to choose whether to base the calculation for the IMD score on the IMD methodology from Scotland, England or Wales.

The map and the graph are linked so that hovering or clicking anywhere on the map will highlight that same LSOA within the graph, and vice versa. When hovering or clicking on the map or graph, a tooltip box will appear to display the following information about the selected LSOA:
* LSOA code
* LSOA name
* Ward name
* Local authority name
* Nation
* Component score

#### DERI score dashboard
The DERI score dashboard follows the same visual structure as the individual component dashboard, but the score displayed is built from the three components. As with the deprivation dashboard, the DERI score dashboard contains the additional drop down box for the IMD score methodology, as the IMD indicator forms part of the overall DERI score through its inclusion within the deprivation component.

By default, the DERI score dashboard will open with all three components equally weighted. However, the button on the top right hand corner of the map allows users to change the relative importance of each indicator. Where changes are made to the score weighting, the scores and the associated visualisations on the map and graph will be updated automatically.

## How to use the DERI, and how not to use the DERI
The DERI is a risk index: it does not mean that every person in a high-risk area is digitally excluded; nor does it mean that no-one in a low-risk area is digitally excluded either. It gives an overview of where targeting resources could have the most benefit.

One way to consider the DERI is as part of an overall risk matrix around digital inclusion. Considering the DERI as an indicator of ‘likelihood’ – people are more likely to be digitally excluded in areas where the DERI score is high. However, adding in another dataset focused on where priority groups are more likely to live would provide the ‘impact’. As an example, anywhere with a high DERI score (likelihood) and a high proportion of disabled people (as a priority group, the ‘impact’) should be a key area of focus.

However, the tool and dataset should not be used as an indicator over time – changes in a DERI score could occur because of, for example, older people moving out of an area. Therefore, as the tool is developed and updated information is added, this should not be seen as a change over time due to digital inclusion activities alone, but rather an updated view on the likelihood of being digitally excluded within an area.

Furthermore, users should consider what additional local data might be used in context alongside the tool. This is not THE tool of digital exclusion, but rather A tool. Adding in local context and data – even if not openly available – can add more detail and ensure that local activity is focused on the areas most likely to be digitally excluded.

