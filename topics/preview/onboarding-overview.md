---
title: Onboarding to the private preview
author: ruthaisabokhae
description: Learn what you need to do to take advantage of the private preview capabilities of Dynamics 365 Product Insights
ms.author: ruthai
ms.date: 08/11/2020
ms.service: product-insights
ms.topic: conceptual
robots: noindex,nofollow
---

# Onboard to the Product Insights private preview

[!INCLUDE [cc-beta-prerelease-disclaimer]( ../includes/cc-beta-prerelease-disclaimer.md)]

This onboarding article gives organizations participating in private preview visibility into product features, documentation, scenarios to validate, and known issues, and explains how to engage with Microsoft throughout the private preview. Nothing in this documentation is meant to, or should be construed to, modify the terms of your agreements with Microsoft, including your preview terms.

## Onboarding overview

*	Review and agree to the [NDA and preview agreement](../preview/preview-terms-of-service.md) with Microsoft.  
*	Review [capabilities outlined in this article](#private-preview-capabilities) for private preview.  
*	Review and understand the [expectations](#private-preview-expectations) and [known issues](known-issues.md) of the private preview.  
*	Validate the [core scenarios](#product-use-cases-to-test) and provide feedback to Microsoft.

## Private preview expectations

*	Private preview is for testing purposes only. Environments may be taken down at the end of the testing period to make way for future releases. See the [Preview terms of service](../preview/preview-terms-of-service.md) for more disclosures and limitations.  
*	Private preview is not for production use, but rather is strictly for prototyping and providing feedback. We are likely to delete data and rebuild environments at any point during the private preview, but will make reasonable efforts to ensure communication of any changes to avoid disruption in testing.   
*	We will work closely with you to seek feedback and incorporate product changes. We expect to establish a cadence for this interaction during the period of private preview and will communicate that subsequently.  
*	Private preview is expected to run approximately for two months (August - September 2020) and we appreciate your active participation. We plan to consider all relevant feedback  in developing future releases.  
*	Reach out to your assigned product manager first or use the email **[pirequest@microsoft.com](mailto:pirequest@microsoft.com)** to provide feedback and report issues. We will use reasonable efforts to triage reported issues, prioritize them, track them, and share a status with you regularly.  
	
## Prerequisites

*	Access to a production website with authentication for your customers to instrument the Product Insights SDK.
*	Access to a test environment for [Dynamics 365 Customer Insights](https://dynamics.microsoft.com/ai/customer-insights/) to test the integration of data.
*	Access to, or ability to create, an Azure Data Lake Storage (ADLS) Gen 2 account for export.

## User consent for use of cookies

*	Refer to the [Manage cookies and user consent](user-consent-storage.md) article.
*	After reviewing this article, you must evaluate if there is need for an update to your user consent notification. If you previously had no "non-essential" cookies, then this will likely require an update to your site policy.

## Private preview capabilities

### First run experience

The starting point for any user is signing in to Product Insights in which the organization is generated and your own environment and projects are created. This is where you'll be able to start ingesting your web analytics data.

### Web SDK

The JavaScript library for your website to measure user interaction with the provided sample code.

### Web analytics and reports

The out-of-the-box reports show the events coming through from the Web SDK with predefined visualizations and dashboards.

### Derived signals

The capability to create a derived event from the web analytics data, filter it and export it to your Azure Data Lake Storage. The exported data in ADLS can get imported into Customer Insights as a data source.

## Product use cases to test

## Setup and provisioning steps

*	Before you start, ensure you have read and agree to the [Preview terms of service](../preview/preview-terms-of-service.md) provided.
*	Sign in to the [Dynamics 365 Product Insights portal](https://pi.dynamics.com) using your Microsoft Azure Active Directory user accounts.
*	Follow the steps in the [quickstart](quickstart-product-insights.md) article to set up your environment and project.
*	Review the [known issues](known-issues.md).

### First run experience

* Follow the account creation process. Set up your environment, create your project, and add members.
* Instrument website with the SDK to see telemetry arriving into your project.
* View the real-time report showing active users by device, page view trend, top pages, top referrers, and users’ geographic locations.

### Export data from Product Insights

  *	Custom website instrumentation: ensure to send an *authid* for each user signing in to your site.
  *	Create a derived event for export activities data.
  *	Export the data into your ADLS Gen 2 storage.
  *	Optional: Ingest Product Insights data export as activities in Customer Insights and view it as part of a customer profile.
  
