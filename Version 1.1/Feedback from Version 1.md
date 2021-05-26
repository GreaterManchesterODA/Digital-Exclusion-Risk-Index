# Feedback from Version 1

## Introduction
Following the release of version 1 of the Digital Exclusion Risk Index, we shared the project with a range of local and national partners, seeking feedback on several areas of work:
 - Usability of the tool
 - Visualisation and geography
 - Methodology and guidance
 - Data

This note is a summary of the feedback received. Feedback was received directly in meetings, informally in conversations with users, and via email.

## Areas of focus
### Usability of the tool
Feedback in this area was generally positive, especially the creation of a tool to allow users to choose the weights used. Users appeared to like the relatively simplistic design, with one focus per dashboard page. Some users commented on how they might be able to use the tool, and whether or not the data might be made available.

One issue that was highlighted was the way the maps worked with the other aspects of each dashboard. Currently, the map highlights areas when you hover over or select them, but did not automatically show all sites again when the selection or hovering ended. Users asked for this to be changed and simplified.

One suggestion provided was to simplify the weighting tool. In Version 1, the weighting tool was a slider with a number between 0 and 100. It was noted that choosing a specific value (for example, 33 or 34 to represent a weighting of one third) might be difficult to do. Furthermore, this required a warning to appear when weightings did not sum to 100. Instead, the suggestion to simplify this was to change the way weightings were presented and calculated. The suggestion was to limit the values of weightings to between 0 and 10, and to change the calculation method so that the weighting for each indicator was the weighting vaue chosen as a proportion of the sum total of all weightings.

To take an example, assume there are three indicators, A, B and C, with weightings 4, 5, and 6 respectively. The weighting applied to A would be 4/15 (that is, 4 divided by the sum of weightings 4, 5 and 6) = 26.7%. The weighting for B would be 5/15 = 33.3%. And the weighting for C would be 6/15 = 40%.

**Actions:**
* Update weighting parameters to be integers between 0 and 10.
* Update component and overall DERI score calculations to apply relative weightings calculations as above.
* Update the dashboard actions to ensure that hovering and selecting sites does not have a negative impact on experience.

### Visualisation and geography
Users noted that the original version of the tool included a soft grey background map that did not include many features that indicated location. It was suggested that the background map in particular could be improved by adding roads, landmarks or place names to help.

Linked to this, the geography of choice became important. The lower super output area (LSOA) geography was chosen for the work as this was the level at which many of the datasets were available. Converting the data to ward or other electoral boundaries would require a degree of translation that might not be entirely accurate. This was balanced against the fact that some data at the LSOA level might be suppressed due to low counts.

However, many users noted that, especially at the local authority level, work was often based around wards rather than LSOAs. LSOA names and codes are not indicative of *where* an area is located. For example, given the name and code 'E01033667 - Manchester 054E', users would not be able to determine the location; however, the ward 'Piccadilly' has an instant location brought to mind for the user. Therefore, either a tool that explained the ward of the LSOA data (despite overlaps between wards of some LSOAs), overlaid wards, or translated the data to a ward level was considered a useful update.

After some discussion, it was felt that a series of approaches could be taken. Firstly, to consider overlaying ward boundaries and adding in the ward names on the tooltips for the dashboards. This would then provide an overview of wards, whilst showing the potential variance *within* wards that a purely ward-level analysis would not provide. Then to test this approach, and see whether other options might be better - for example, an on/off button for ward overlays, and separately an option to switch between LSOA and ward level analysis.

The original model focused on one local authority. Discussions with different parts of the country, and through the Cooperative Councils Innovation Network, has highlighted a sensible need to ensure that areas other than just England are reasonably included. This would involve adding in further Welsh data  - specifically, the Wales IMD data - and expanding the work to include Scotland, as well as potentially Northern Ireland.

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

Generally, users suggested an index approach worked for them - it simplified the issue of digital exclusion, whilst allowing specific datasets to be delved into. Users also noted that the use of clear guidance and releasing the notes on GitHub gave people a flavour and expectation of how the tool was developed and the decisions made.

However, many of the comments focused on the information that should be contained within the index. It is clear from the evidence, and from feedback, that users appreciated deprivation and age were two key risk factors for digital exclusion. Within the deprivation component of the DERI calculation, skills levels and unemployment were also considered key factors. Nevertheless, a number of new datasets were suggested for inclusion within the methodology. The primary area for inclusion was around digital activity as a component. In the original Salford work, this was captured through 'hard to count' scores that were pre-Census estimates from ONS; online contacts as a proportion of all contacts with the council; and the proportion of residents paying their council tax online. None of these datasets are available openly, nationally, and so the activity component was not included within version 1 of the tool.

Some suggestions for potential digital activity components included: library PC user addresses, though this was noted to be sensitive, and not available openly, nationally; Census data, when released, of the areas that were assigned paper copies in advance, and areas that requested paper copies during the Census period; and the CDRC's Internet User Classification.

Other domains were also suggested. One user suggested that 'impacts of digital exclusion' could also be included within the methodology. Suggested indicators for this component included the use of specific indices within the English Indices of Deprivation, such as access to services; and the use of Transport for Greater Manchester's 'Greater Manchester Accessibility Layer', or GMAL. 

It is important for the team to follow up on these potential methodological components. Not all of the datasets are openly available, or available across the relevant geographies.

Fourth domain - IMD access to services, GM transport accessibility
Validity of using IMD as a composite indicator already
Activity needs to be included - e.g. Census data on needing paper copies, who took paper copies
Guidance for how to use and how not to use the tool

**Actions:**
* Explore what other datasets might be sensible to include within the methodology, including those highlighted above.
* Continue to provide updates on developments on GitHub, as well as providing links to the tool.
* 

### Data
Wales IMD
Scotland inclusion

