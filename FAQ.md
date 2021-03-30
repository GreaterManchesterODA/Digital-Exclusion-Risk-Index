# Frequently Asked Questions

This document related to [Version 1](/Version%201) of the DERI.

Common questions:
* [What is the Digital Exclusion Risk Index?](#what-is-the-digital-exclusion-risk-index)
* [What is the background to the DERI?](#what-is-the-background-to-the-deri)
* [Who is creating the DERI?](#who-is-creating-the-deri)
* [How can I access the DERI tool?](#how-can-i-access-the-deri-tool)
* [How is the DERI calculated?](#how-is-the-deri-calculated)
* [What are the data sources for the DERI?](#what-are-the-data-sources-for-the-deri)
* [What is the geographic basis of the DERI?](#what-is-the-geographic-basis-of-the-deri)
* [Can I access the background data?](#can-i-access-the-background-data)
* [Can I add data to the DERI?](#can-i-add-data-to-the-deri)
* [Can I view bespoke geographies in the tool?](#can-i-view-bespoke-geographies-in-the-tool)
* [What are the next steps for the DERI?](#what-are-the-next-steps-for-the-deri)

---

## What is the Digital Exclusion Risk Index?
The Digital Exclusion Risk Index (DERI) is a methodology and a tool to visualise and understand the risk of digital exclusion at a localised geographic level. It uses a number of indicators, which are normalised, weighted and summed, to create a DERI score - a number between 0 and 10 that identifies the risk of digital exclusion in an area. The score is calculated on a lower super output area geography, and presented in a Tableau dashboard to allow users to explore the score in more detail.

## What is the background to the DERI?
The DERI is based on original work by Salford City Council (SCC). SCC created a model to visualise the risk of digital exclusion in its locality, and this was shared with digital locality leads in Greater Manchester. Locality leads saw the value in creating an index to help target resources and improve understanding, while several local authorities around the country have started to, or have, created their own indices. Locality leads in Greater Manchester saw the value in expanding the approach by SCC, and the Greater Manchester Combined Authority (GMCA) agreed to develop a tool for Greater Manchester.

Separately, in conversation with a number of districts around the country, it was identified that a similar approach would also be beneficial. With digital inclusion being a priority for GMCA, it was agreed that the organisation would expand the approach further, with the aim of creating a national methodology and tool. With several areas considering or having developed their own indices, it was felt that a national tool might help reduce duplication of effort, and help to foster a shared view of the relevant indicators of digital exclusion nationally.

Throughout the latter half of March 2021, GMCA developed a first version of the tool in Tableau, and shared this with locality leads and key partners.

## Who is creating the DERI?
The work is based on original work by Salford City Council. The DERI is being developed by GMCA, specifically the Research and Digital teams.

## How can I access the DERI tool?
The DERI tool is currently closed to a limited number of users for testing, who have been contacted directly. However, all the related information to recreate version 1 of the tool is [available in this repository](/Version%201).

## How is the DERI calculated?
[A full methodology document](/Version%201/DERI%20Score%20Methodology_v1.md) has been created to show how the DERI is calculated. In addition to this methodology, certain elements are specific to Tableau. As such, a [Tableau development document has also been created](/Version%201/Tableau%20development_v1.md) to allow users to recreate the Tableau dashboards on their own. It is envisaged that later versions of the tool will be made more open.

## What are the data sources for the DERI?
There is a [data sources document](/Version%201/Data%20sources_v1.csv) that identifies the source of the data for the indicators that make up the DERI score. These should be read alongside the [methodology document](/Version%201/DERI%20Score%20Methodology_v1.md).

## What is the geographic basis of the DERI?
The DERI provides a score between 0 and 10, with 0 being low risk and 10 a high risk of digital exclusion. These are calculated on an LSOA basis, using maxmum and minimum values at the local authority level.

## Can I access the background data?
We have not released the background data on this repository. This is due to the data being an early stage prototype, and therefore the data being subject to significant change. However, all of the data sources are identified in the [data sources document](/Version%201/Data%20sources_v1.csv), and all are accessible datasets.

## Can I add data to the DERI?
No, not at present. The tool is not designed for users to add further data. However, we aim to make the data open so that users can download and use the data from the tool, as well as update with their own information.

## Can I view bespoke geographies in the tool?
Currently, the only geographies used in the tool are LSOAs (for which the scores are derived) and local authorities (which are used to filter the LSOAs).

## What are the next steps for the DERI?
Currently, we are in a testing phase of the tool and methodology. We want to test certain factors - the choice of geography, the usability of the tool, and the methodology - before making changes to the tool for wider use. We will update this repository with next steps when the results of the testing are complete.
