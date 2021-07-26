# Feedback from Version 1.0

## Introduction
Following the release of [version 1.0 of the Digital Exclusion Risk Index](https://www.gmtableau.nhs.uk/t/GMCA/views/210325_DERI/DERIhomepage?%3Aiid=1&%3AisGuestRedirectFromVizportal=y&%3Aembed=y#1) and it's [methodology here on GitHub](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.0), we shared the project with a range of local and national partners, seeking feedback on several areas of work:
 - Usability of the tool
 - Visualisation and geography
 - Methodology and guidance
 - Data

This note is a summary of the feedback received. Feedback was received directly in meetings, informally in conversations with users, and via email.

## Areas of focus
### Usability of the tool
Feedback in this area was generally positive, especially the creation of a tool to allow users to choose the weights used. Users appeared to like the relatively simplistic design, with one focus per dashboard page. Some users commented on how they might be able to use the tool, and whether or not the data might be made available.

One issue that was highlighted was the way the maps worked with the other aspects of each dashboard. Currently, the map highlights areas when you hover over or select them, but did not automatically show all sites again when the selection or hovering ended. Users asked for this to be changed and simplified.

One suggestion provided was to simplify the weighting tool. In [Version 1](https://www.gmtableau.nhs.uk/t/GMCA/views/210325_DERI/DERIhomepage?%3Aiid=1&%3AisGuestRedirectFromVizportal=y&%3Aembed=y#2), the weighting tool was a slider with a number between 0 and 100. It was noted that choosing a specific value (for example, 33 or 34 to represent a weighting of one third) might be difficult to do. Furthermore, this required a warning to appear when weightings did not sum to 100. Instead, the suggestion to simplify this was to change the way weightings were presented and calculated. The suggestion was to limit the values of weightings to between 0 and 10, and to change the calculation method so that the weighting for each indicator was the weighting vaue chosen as a proportion of the sum total of all weightings.

To take an example, assume there are three indicators, A, B and C, with weightings 4, 5, and 6 respectively. The weighting applied to A would be 4/15 (that is, 4 divided by the sum of weightings 4, 5 and 6) = 26.7%. The weighting for B would be 5/15 = 33.3%. And the weighting for C would be 6/15 = 40%.

**Actions:**
* Update weighting parameters to be integers between 0 and 10.
* Update component and overall DERI score calculations to apply relative weightings calculations as above.
* Update the dashboard actions to ensure that hovering and selecting sites does not have a negative impact on experience.

### Visualisation and geography
Users noted that the original version of the tool included a soft grey background map that did not include many features that indicated location. It was suggested that the background map in particular could be improved by adding roads, landmarks or place names to help.

Linked to this, the geography of choice became important. The [lower super output area (LSOA) geography](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeography#super-output-area-soa) was chosen for the work as this was the level at which many of the datasets were available. Converting the data to ward or other electoral boundaries would require a degree of translation that might not be entirely accurate. This was balanced against the fact that some data at the LSOA level might be suppressed due to low counts<sup>[1](#footnote1)</sup>.

However, many users noted that, especially at the local authority level, work was often based around wards rather than LSOAs. LSOA names and codes are not indicative of *where* an area is located. For example, given the name and code 'E01033667 - Manchester 054E', users would not be able to determine the location; however, the ward 'Piccadilly' has an instant location brought to mind for the user. Therefore, either a tool that explained the ward of the LSOA data (despite overlaps between wards of some LSOAs), overlaid wards, or translated the data to a ward level was considered a useful update.

After some discussion, it was felt that a series of approaches could be taken. Firstly, to consider overlaying ward boundaries and adding in the ward names on the tooltips for the dashboards. This would then provide an overview of wards, whilst showing the potential variance *within* wards that a purely ward-level analysis would not provide. Then to test this approach, and see whether other options might be better - for example, an on/off button for ward overlays, and separately an option to switch between LSOA and ward level analysis.

**Actions:**
* Add a ward overlay to the data as a starting point.
* Consider adding an LSOA to ward lookup to the tool so that the ward name is displayed for each LSOA.
* Add a new background map that shows the roads and place names clearly for users.
* Update the style of the maps, to reduce opacity and allow users to see more of the underneath map.
* Review the ward overlays, and understand whether a ward-level tool would be appropriate.
* Consider using the tooltip to display more ward-level data, where possible.
* Explore the inclusion of further Welsh, Scottish and Northern Irish data into the tool.

### Methodology and guidance
The methodology feedback has been the most abundant. The team has shared the tool quite widely with local and national stakeholders, and the focus on the methodology has been important. Some of these issues cross over specifically with the datasets to be used, and the level of geography.

Generally, users suggested an index approach worked for them - it simplified the issue of digital exclusion, whilst allowing specific datasets to be delved into. Users also noted that the use of clear guidance and releasing the notes on GitHub gave people a flavour and expectation of how the tool was developed and the decisions made. Users also suggested guidance to highlight how to use the tool, and how not to use the tool. This latter point is crucial, as it is important to use the DERI score within the tool as *indicative* of digital exclusion risk.

However, many of the comments focused on the information that should be contained within the index. It is clear from the evidence, and from feedback, that users appreciated deprivation and age were two key risk factors for digital exclusion. Within the deprivation component of the DERI calculation, skills levels and unemployment were also considered key factors. Nevertheless, a number of new datasets were suggested for inclusion within the methodology. The primary area for inclusion was around digital activity as a component. In the original Salford work, this was captured through 'hard to count' scores that were pre-Census estimates from ONS; online contacts as a proportion of all contacts with the council; and the proportion of residents paying their council tax online. None of these datasets are available openly, nationally, and so the activity component was not included within version 1 of the tool.

Some suggestions for potential digital activity components included: library PC user addresses, though this was noted to be sensitive, and not available openly, nationally; Census 2021 data, when released, of the areas that were assigned paper copies in advance, and areas that requested paper copies during the Census period; and the CDRC's Internet User Classification.

Other domains were also suggested. One user suggested that 'impacts of digital exclusion' could also be included within the methodology. Suggested indicators for this component included the use of specific indices within the English Indices of Deprivation, such as access to services; and the use of Transport for Greater Manchester's 'Greater Manchester Accessibility Layer', or GMAL.

It is important for the team to follow up on these potential methodological components. Not all of the datasets are openly available, or available across the relevant geographies.

Lastly, an issue was also raised with the use of the Indices of Deprivation. This dataset is already a composite indicator dataset, and there were concerns that its inclusion might either double-count some existing indicators, or be closely aligned with other existing indicators. It is important that the model addresses correlations and the potential for double counting, an issue highlighted further in the data section below. 

**Actions:**
* Explore what other datasets might be sensible to include within the methodology, including those highlighted above.
* Continue to provide updates on developments on GitHub, as well as providing links to the tool.
* Explore the correlations between datasets to see if there is a risk of 'double-counting' a particular indicator.

### Data
The original model produced by Salford City Council focused on data for one local authority. Expansion to England and Wales means that a number of datasets are not used, such as the activity data identified above.

Discussions with different parts of the country, and through the Cooperative Councils Innovation Network, has highlighted a sensible need to ensure that areas other than just England are reasonably included. This would involve adding in further Welsh data  - specifically, the Wales IMD data - and expanding the work to include Scotland, as well as potentially exploring Northern Ireland. An issue with this expansion is in identifying an appropriate dataset to use. While the English and Welsh IMDs are roughly comparable, they are not identical. Therefore, the inclusion of all three deprivation indices would mean areas with similar characteristics in the different nations would experience different results.

One element of the feedback focused on which data should be used. There are strong arguments for adding new data to identify areas where people who are most likely to experience digital exclusion. Proposed additional data includes areas where disabled people are more likely to live, a group that is not currently included. This might need to be added to a wider 'demographic' component that incorporates age, rather than creating a new component to sit alongside the existing ones.

Furthermore, users have suggested the work of Prof. Simeon Yates et al as a source of the potential indicators for a sociodemographic component. Prof. Yates' work has highlighted that 'limited' users of the internet and digital services are more likely to:
* Be part of a lower socioeconomic classification (DE)
* Be older, especially aged 55 and above
* Live in a more rural location
* Have left education before university
It would be useful to consider these options as part of the work.

In relation to age data, users have suggested changing the data included in the calculation of the DERI score. In addition to the points raised above, the data currently includes 65+ and 75+ ages as data points. Users have suggested splitting this out (e.g. 65-74 and 75+), as there is an element of double counting in using over 75s in two parts of the age component. The two data points are closely, but not directly correlated, hence their inclusion. However, this split should be considered for the work. 

Lastly, a range of organisations have also created their own versions of a digital exclusion risk model. These include, but are not limited to, Westminster Council, Manchester City Council, and London Office of Technology and Innovation. The team should explore these models, and identify similarities and differences, where learning across programmes can be developed.

**Actions:**
* Explore an appropriate dataset to use across the different nations around deprivation
* Expand the data to include England, Wales and Scotland
* Consider the suggested socio-demographic indicators of disabled people, and a variance in the age data
* Consider splitting the current age data to include 65-74, and 75+ groups
* Engage with other organisations across the UK that are attempting to create a risk index, and explore how similar or different approaches may be


---
### Footnotes
<a name="footnote1">1</a>: For a more detailed discussion and overview of geographies used in the UK, see the [ONS UK Geographies webpages](https://www.ons.gov.uk/methodology/geography/ukgeographies).
