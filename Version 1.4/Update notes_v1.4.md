# Updates to Version 1.4

[Version 1.4](https://www.gmtableau.nhs.uk/t/GMCA/views/DigitalExclusionRiskIndexv1_4/DERIhomepage?:iid=2&:isGuestRedirectFromVizportal=y&:embed=y) included three main changes to the methodology and tool:
* Transforming the 'age' component to a broader 'demography' component
* Calculating two new sets of DERI scores based on national and Great Britain level mins and maxes
* Adding functionality to the dashboards to allow users to select the preferred DERI score (local/national/GB)

## Demography component
Versions 1.0 to 1.3 of the DERI used an age component to form the DERI score. However, [research by the Good Things Foundation](https://www.goodthingsfoundation.org/insights/digital-exclusion-and-health-inequalities/) indicates that there are other demographic factors in addition to age that put people at higher risk of being digitally excluded, such as being disabled or on a low income. As a result, we have expanded our `Age component` to a broader `Demography component` that brings together the following four indicators:
* Percentage of population aged 65-74
* Percentage of population aged 75+
* Percentage of residents whose daily activities are limited
* Percentage of population in social grade DE

### Tableau updates for demography component
Changing this component required two new sets of calculations: one set to create a score for the percentage of residents whose daily activities are limited and one for the percentage of population in social grade DE. Parameters were also created for the weightings of each of these new scores. The creation of these calculations and parameters followed the same process as outlined in the original [version 1.0 methodology](https://github.com/GreaterManchesterODA/Digital-Exclusion-Risk-Index/blob/main/Version%201.0/DERI%20Score%20Methodology_v1.0.md#individual-indicator-scores).

Once these calculations and parameters were created, the `Age component` was renamed to `Demography component` and the calculated field was updated to be based on the scores and parameters for all four indicators.

## National and Great Britain DERI scores 
Prior versions of the DERI tool based the calculation for the indicator, component and DERI scores on the minimum and maximum values in each local authority district. While this is useful for seeing the relative risk of digital exclusion within a local area, this approach limits the usefulness of comparisons between different local authority areas. To enable meaningful comparisons between different local authorities required a second and third set of calculations to be created. The first set recalculated the scores based upon the maximum and minimum indicator values within each nation (England, Scotland and Wales). The second set recalculated the scores based upon the maximum and minimum values across the full dataset, which includes all of Great Britain.

### National scores
Add text here ...

Appendix A details the full set of calculations involved behind the national scores.

### Great Britain scores
Add text here ...

Appendix B details the full set of calculations involved behind the GB scores.

## Improving dashboard functionality to select different DERI score calculations
Add text here ...

## Appendix A

## Appendix B
