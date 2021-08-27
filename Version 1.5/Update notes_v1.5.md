# Updates to Version 1.5

[Version 1.5](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_5/DERIhomepage?:iid=1&:isGuestRedirectFromVizportal=y&:embed=y) contained two main updates:
* Calcualting a version of the Index of Multiple Deprivation score based on each of the English, Welsh and Scottish methodologies
* Adding functionality to the dashboards to allow users to select the English, Welsh or Scottish calculation

## Calculating English, Welsh and Scottish IMD scores
Each of the English, Welsh and Scottish IMD scores use slightly different metrics and methodologies so they are not directly comparable. This means that a score of x on the English IMD should not be construed as comparable to the same score on the Welsh or Scottish IMD scale. However, a few years ago a group of researchers set out to come up with a coherent deprivation score by mapping between the various domains. This work has been recently updated and is [published here](https://github.com/mysociety/composite_uk_imd), along with reflective discussion about how to use the scores and what their limitations are.

This repository includes a different composite IMD file for each nation, in which that nation has been used as the calculation base and all other scores are aligned with that nation's scores. The guidance for the comosite IMD is to use the data corresponding to the primary area of focus. Given that the DERI tool is available for users in all three nations, we felt it was necessary to provide users with the option to select the IMD score that corresponds to their area.

The repository has UK indices and GB indices. We have used the GB set of data as the DERI tool currently only looks at England, Wales and Scotland. The links below show where we sourced each dataset from within the composite IMD repository:
* [English IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_E.csv)
* [Welsh IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_W.csv)
* [Scottish IMD scores](https://github.com/mysociety/composite_uk_imd/blob/master/gb_index/GB_IMD_S.csv)

The process for calculating the separate IMD scores within the DERI tool followed the same steps as the original [indicator score methodology](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.0/DERI%20Score%20Methodology_v1.0.md#individual-indicator-scores).

## Adding functionality to choose the IMD score base within the dashboards
