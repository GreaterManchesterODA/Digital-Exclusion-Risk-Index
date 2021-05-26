# Feedback

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

**Actions:**

