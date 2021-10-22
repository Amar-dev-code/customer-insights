---
title: "Company data enhancement"
description: "Enrich and normalize company data with Microsoft's models."
ms.date: 10/22/2021
ms.reviewer: mhart
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: how-to
author: kishorem-ms
ms.author: kishorem
manager: shellyha
---

# Enrichment of company profiles with enhanced company data

Use Microsoft’s models and compiled company data to correct, supplement, and standardize your company profiles into the Common Data Model format for better accuracy and insights.

## How we enhance company data

Our model goes through a two-step process to enhance a company profile. First, it normalizes the company name. For example, *Microsft Corp*. will be corrected and standardized to *Microsoft Corporation*. Then, we try to find a match in our compiled company data. If a match is found, we enrich the company profile with information from our compiled company data, including the company name.


### Example

Company information might be in a nonstandard format and contain spelling errors. The model can fix these issues and create consistent information.

```Input
Microsft
```

```Output
- AccountName: Microsoft Corporation
- MainPhoneNumber: 8006427676
- Website: https://www.microsoft.com/
- Street1: One Microsoft Way
- City: Redmond
- StateOrProvince: Washington
- County: King
- ZipOrPostalCode: 98052
- CountryOrRegion: United States
```

## Limitations

The model doesn't: 

1.	Confirm the identity of the company. We don't verify if the input company profile is an existing organization or that it uses the output company name as its standard name.
2.	Comprehensively cover companies globally. Microsoft’s compiled company data has global coverage, but offers most coverage in Australia, Canada, United Kingdom, and the United States.
3.	Guarantee accuracy or freshness of data. As business information often changes, we can't guarantee that the enhanced company data provided is always accurate or up-to-date.

## Configure the enrichment

1. Go to **Data** > **Enrichment**.

1. Select **Enrich my data** on the **Enhanced company data** tile.

<TODO: Screenshot>

1. Select the **Customer data set** and choose the entity containing the addresses you want to enrich. You can select the *Customer* entity to enrich addresses in all your customer profiles or select a segment entity to enrich addresses only in customer profiles contained in that segment.

1. Select which type of fields from your company profiles should be used for matching with Microsoft’s compiled company data. This selection will affect the mapping fields you have access to in the next step.

1.	Map the company fields from your unified customer entity. The more key identifiers and fields you map, the more likelihood of a higher match rate.

<TODO: Screenshot>

1. Select **Next** to complete the field mapping.

1. Provide a name for the enrichment and the output entity.

1. Select **Save enrichment** after reviewing your choices.

## Enrichment results

To start the enrichment process, select **Run** from the command bar. You can also let the system run the enrichment automatically as part of a [scheduled refresh](system.md#schedule-tab). The processing time depends on the size of your customer data.

After the enrichment process completes, you can review the newly enriched customer profiles data under **My enrichments**. Additionally, you'll find the time of the last update and the number of enriched profiles.

You can access a detailed view of each enriched profile by selecting **View enriched data**.

## Next steps

[!INCLUDE [next-steps-enrichment](../includes/next-steps-enrichment.md)]

[!INCLUDE[footer-include](../includes/footer-banner.md)]
