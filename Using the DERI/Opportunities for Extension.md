# Opportunites for Extension
## Introduction
The Digital Exclusion Risk Index is a tool in your toolkit. This does not mean that it shows everything that you need to know about digital exclusion, or that it provides a comprehensive overview.

As such, you may choose to consider using the dataset and tool as a base; extending or altering the tool; extending, adding to, or altering the dataset; developing something new with the data; or developing something new that complements the DERI more generally.

This document provides some potential opportunities for extension that you might want to explore. Some of these may be taken forward by the Greater Manchester Combined Authority in future, but they are presented as options for you to explore.

If you would like to explore options for extension, please do so. The GMCA would be interested in what you do, but we claim no right over it - the dataset and notes about development are all released under an Open Government Licence. Rather, we would like to work with you on projects where this is beneficial to both parties.

If you would like to work with the GMCA on new tool developments, or would like to ask any questions about the tool, please contact us at oda@greatermanchester-ca.gov.uk.

## Dataset opportunities
There are several opportunities associated with the dataset itself. GMCA will commit to regularly updating and releasing new datasets, adding in new data where necessary. However, you may choose to do a number of things with the dataset to transform it for your needs. The below represents some potential examples.

### Updating the data
There is nothing to stop you taking a copy of the dataset from GitHub and changing the data within. We actively encourage this, especially where the dataset does not meet your needs.

One option for change would be to update the data within to newer datasets. Many of the source datasets are older than a year, and some datasets are static - for example, the Census information. While GMCA will update this data in time as new information comes out, you may wish to do this sooner.

### Switching the data
Another option might be to change individual datasets. The composite Indices of Deprivation, produced by mySociety might not be suitable for your needs, and a more specific national dataset might be more sensible to use for your purposes. Furthermore, you may wish to switch out the Indices of Deprivation for one of the domain scores or other component score within the indices.

### Cutting the data
A further change you may wish to take might be to take a cut of the dataset for a specific area, and recalculate DERI scores based on those areas. The DERI tool allows you to do this at a local authority level, but you may have a particular focus on different areas, such as neighbourhoods, wards, primary urban areas, CCG or ICS areas, or any number of potential geographical boundaries. To do this, we would suggest accessing the latest data, taking a cut of relevant LSOAs or areas, and following the DERI methodology to calculate maximum and minimum values for those relevant areas.

### Adding new data
There is nothing to stop you adding more data to the dataset, and following the same methodology with the new expanded dataset. This expansion could take the form of new indicators, or adding in new geographies. In terms of adding new indicators, see [the section below on extending the analysis to incorporate new data](#new-indicators-or-components).

One obvious missing geographic area within the current tool and dataset is Northern Ireland. We welcome and actively encourage work to expand the DERI to include Northern Ireland. Furthermore, with appropriate datasets, a similar type tool could also, theoretically, be developed for Europe or other areas of the world where potentially similar datasets are used.

### Altering calculations and weightings
While calculations are set, and weightings are put to a default level, these can be changed. Examples might include changing the weightings of different indicators or components (which can be done in the DERI tool itself) to see how this impacts the analysis; or changing the scoring methodology, such as using a different score level (e.g. 0-100).

One potential change to the calculations might be to take account of the difficulty in reducing or increasing some indicators. For example, reducing the unemployment rate from 10% to 9.8% might be significantly easier than reducing it from 0.2% to 0%. There are plenty of options to take account of this. The Human Development Index might be a sensible consideration in terms of approach - calculating indicator or component scores using a logarithm, for example, could take account of this difficulty. 

### Changing geographies
Different organisations care about different geographic splits. Early on in the development of the DERI, it was clear that local authorities especially were interested in the ward-level view of digital exclusion. This is why the tool incorporates an overlay of ward boundaries.

Much of the data for the DERI is at an LSOA or OA level, making it easy to build up into higher geographies based on their boundaries. However, several datasets are also available at other geographic levels. Therefore, while potentially difficult, the DERI could be calculated for other geographies. 

## Tool opportunities
The main tool opportunities focus on improving the accessibility and usability of the tool, to improve understanding of the data.

The current tool is developed using Tableau, a software that can be used for free for a limited period. However, while the DERI tool is provided to use for free online - utilising Tableau Server - other dashboarding tools and software exist. The tool could just as easily be developed using tools such as Leaflet, D3, R, PowerBI or others, and we would welcome a translation of the tool using other software or processes.

One area the GMCA would like to explore is creating more reactive calculations. That is, the calculations for the dataset are based on the maximum and minimum values of indicators at the local, national or GB-wide level. But Tableau allows users to select specific LSOAs, or districts. We are currently exploring whether the tool might allow calculations of the DERI score based on the maximum and minimum indicator values of the areas chosen by the user, not pre-defined by our calculations. For example, say a user chose Brentford and Cambridge. Currently, the local calculation method would use the maximum and minimum indicator values for Brentford to calculate the DERI score for each Brentford LSOA; and the maximum and minimum indicator values for Cambridge to calculate the DERI score for each Cambridge LSOA. Under this new method, the calculation would use the maximum and minimum indicator values of all LSOAs in Brentford _OR_ Cambridge to calculate the DERI score for each LSOA in those two areas. If Glasgow was added to the user selection, the calculation would update, and the DERI score for each LSOA in each district would change. Theoretically, this approach should be possible in Tableau or another tool. 

## Extensions to the analysis
There are  range of potential extensions that could be made to the analysis. The below extensions to the DERI dataset and tool would serve to improve or expand the scope of the work.

### New indicators or components
Through the development of the DERI, several new or additional datasets were identified as potential additions to the dataset. Indeed, the disabled people's data and social grade information was added to the original Salford calculation methodology, based on work from the University of Liverpool. While some of these datasets could be incorporated into the existing structure of the DERI, others require the creation of a separate component as they do not easily fit within the existing three components.

The original Salford methodology included a fourth 'activity' component. This was dropped initially for several reasons: firstly, the data used in the original methodology was not openly available, and was unlikely to be consistent nationally. The data used by Salford included the proportion of people who contacted the council online; and the proportion of residents in an area paying their council tax online.

The second reason was that the indicators used appeared to be related more to digital services than digital activity. Some local authorities, for example, will have moved significant numbers of services online, and pushed this as a first method of engagement for residents. Others will not have done this. Measuring use of these services might be more a measure of the push to these services being digital, rather than a choice to be actively digital.

Lastly, the team felt that those indicators focused more on _digital inclusion_ than _digital exclusion_. As a result, one area of potential expansion around this is [discussed below](#digital-inclusion-index).

Nevertheless, the inclusion of a digital activity component is considered by many who have developed an index. As such, several local and national datasets have been suggested for addition to the DERI. The primary dataset suggested appears to be the Internet User Classification. An exploration of this dataset suggests that the different groups would align with a risk score approach, though the exact ordering of the groups might be up for debate. Alternatively, using the proportion of residents who are likely to be in specific groups could also be an indicator that could be used in a new activity component. We would also welcome exploration of this work.

### Personality profiles
Many areas extended their analysis by incorporating personality profiles. These were usually resident typologies, often constructed in commercial, non-open datasets such as Acorn, Paycheck, and MOSAIC. The use of these typologies or profiles alongside the risk indices is helpful in providing a wider picture of the data, and the types of residents also associated with high levels of digital exclusion risk.

However, the commercial nature of these datasets meant that we would be unable to utilise them in an openly licenced DERI. Nevertheless, we would like to explore the potential for how this could be accomplished on a systematic basis. Other open typologies, such as the Output Area Classifications, might be amenable to inclusion in the DERI, or as an extension to the analysis.

### Risk matrix development
One way to conceptualise the DERI is to think of it as part of a wider risk matrix. A risk matrix is usually composed of two elements for every risk - likelihood, and impact. Risks with high likelihood and high impact are usually addressed first. In the context of digital exclusion, it may be sensible to consider the DERI as the 'likelihood' part of the risk matrix. That is, the higher the score, the more likely people in an area are digitally excluded.

On the impact side of things, it may be useful to consider particular groups who are likely to be impacted by digital exclusion - e.g. younger people, older people, disabled people. Using a similar scoring methodology, a score could be developed to show 'impact' - i.e. where priority groups are likely to live. When digital exclusion risk is high (likelihood), and there are high proportions of an affected group in an area (impact), then the overall risk level of an area is high, and these areas must be prioritised.

GMCA has attempted this approach in earlier stages, and would be willing to work with partners to explore this further.

## Complementary analysis
Lastly, there may be other areas of complementary analysis to the DERI. That is, new products or tools that would add to the DERI, or work alongside it, whilst being conceptually separate.

### Using risk indices
Generally, the use of risk indices in other areas of concern might be an opportunity. Across larger geographies, inequality may be something that a risk index type approach could be useful.

### Digital inclusion index
Specifically around digital exclusion, the issue of digital activity has previously been highlighted. One complementary analysis that could be explored is in creating a Digital _Inclusion_ Index. That is, attempting to identify where digital inclusion is more likely, due to high levels of activity. Datasets to incorporate might include a mapping of digital inclusion support, digital skills and qualifications take-up, and digital activity. This analysis could support a better understanding of digital _exclusion_ when mapped alongside one another. For example, areas that rank as having a high risk of digital exclusion might be tempered by a high degree of digital activity in the area and amongst residents. To a degree, this approach might rely on digital inclusion system mapping.

### System mapping
A further area of work the GMCA has explored is in mapping the digital inclusion support system in Greater Manchester. This includes identifying:
* **Projects** delivering digital inclusion support
* **Organisations** delivering these projects
* **Places and spaces** where these projects are delivered
* **Connections** between projects, organisations, and places or spaces

Organisations such as LOTI have pioneered this approach, and the wider implications of this work (such as creating 'service directories' across larger areas) is clear. Making information about these projects, organisations, places and spaces more open can support better engagement and delivery.

By identifying these in Greater Manchester, we can understand more about what is being delivered where, for who, and by who; understand where gaps in types of provision might occur; understand geographic gaps in provision of support; identify and support new opportunities; connect up organisations and projects; provide more information to individuals experiencing digital exclusion; and support a whole-system approach to tackling digital exclusion.

## Next steps
If you would like to discuss any of the above with us, please do, by contacting oda@greatermanchester-ca.gov.uk. We'd love to hear from you, and about the work you are doing. We also encourage people using the DERI to both feed back to us issues with the tool or dataset, contribute to this GitHub repository of information, and open their work for others to use.
