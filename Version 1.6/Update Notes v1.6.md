# Update Notes for Version 1.6

This document has all the new notes for changes made between [version 1.5](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_5/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y) and [version 1.6](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_6/DERIhomepage?:showAppBanner=false&:display_count=n&:showVizHome=n&:origin=viz_share_link) of the Digital Exclusion Risk Index (DERI).

For full understanding of what goes into the DERI, it is important to read the [version 1.0 summary documents and details](GreaterManchesterODA/Digital-Exclusion-Risk-Index/tree/main/Version%201.0) as a foundation for the DERI dataset and tool. Each subsequent version of the tool includes updates to the relevant files in that folder.

The latest release of DERI is v1.6 which was released in November 2022.

This includes data updates from:

**1. Age Component**
  - Mid Year Population Estimates 
    - [Scotland, NRS SAPE 2020](https://www.nrscotland.gov.uk/statistics-and-data/statistics/statistics-by-theme/population/population-estimates/2011-based-special-area-population-estimates/small-area-population-estimates)
    - [England and Wales, ONS SAPE 2020](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/bulletins/annualsmallareapopulationestimates/mid2020)

**2. Broadband Component**
  - [Ofcom Data, May 2022, Connected Nations update on coverage availability by output area](https://www.ofcom.org.uk/research-and-data/multi-sector-research/infrastructure-research/connected-nations-update-autumn-2022)
  
**3. Deprivation Component**
  - [Alternative Claimant Count, May 2022, Stat-Xplore](https://stat-xplore.dwp.gov.uk/webapi/jsf/login.xhtml)
  - [Pension Credit Caseload, February 2022, Stat-Xplore](https://stat-xplore.dwp.gov.uk/webapi/jsf/login.xhtml)
  
**4. Dashboard refresh**
  - Refreshed some of the dashbord interface, to fix some reported issues in v1.5 such as the DERI scale on some dashboards


## Note on geographic data
At the time of development, data from the 2021 Census had not been fully released. While small area boundaries for 2021 were available - for example, the lower super output areas in England and Wales - not all data sources had updated their reporting to reflect these. As such, the decision was made to retain the 2011 Census lower super output area boundaries, and data zones in Scotland. We are exploring updating to 2021 boundaries in the next iteration of DERI.
