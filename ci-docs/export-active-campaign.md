---
title: "Export segments to ActiveCampaign"
description: "Learn how to configure the connection and export to ActiveCampaign."
ms.date: 10/08/2021
ms.reviewer: mhart

ms.subservice: audience-insights
ms.topic: conceptual
author: pkieffer
ms.author: philk
manager: shellyha
---

# Export segments to ActiveCampaign (preview)

Export segments of unified customer profiles to ActiveCampaign and use them for marketing activities.

## Prerequisites

- An [ActiveCampaign account](https://www.activecampaign.com/) and corresponding administrator credentials.
- [Configured segments](segments.md) in Customer Insights.
- Unified customer profiles in the exported segments contain a field with an email address.
- An ActiveCampaign [connection](connections.md) is [set up](#set-up-connection-to-activecampaign) by an administrator.

## Known limitations

- The maximum customer profiles per export to ActiveCampaign is 1 million, which can take up to 90 minutes to complete. The number of customer profiles that you can export to ActiveCampaign depends on your contract with ActiveCampaign.
- Exporting to ActiveCampaign is limited to segments.

## Set up connection to ActiveCampaign

You must be an [administrator](permissions.md) in Customer Insights.

1. Go to **Admin** > **Connections**.

1. Select **Add connection** and choose **ActiveCampaign** to configure the connection.

1. Give your connection a recognizable name in the **Display name** field. The name and the type of the connection describe this connection. We recommend choosing a name that explains the purpose and target of the connection.

1. Choose who can use this connection. By default, it's only administrators. For more information, see [Allow contributors to use a connection for exports](../connections.md#allow-contributors-to-use-a-connection-for-exports).

1. Enter your [ActiveCampaign API Key and REST Endpoint Hostname](https://help.activecampaign.com/hc/articles/207317590-Getting-started-with-the-API#how-to-obtain-your-activecampaign-api-url-and-key). The REST Endpoint Hostname is the hostname only, without https://.

1. Select **I agree** to confirm the [Data privacy and compliance](#data-privacy-and-compliance).

1. Select **Connect** to initialize the connection to ActiveCampaign.

1. Select **Add yourself as export user** and provide your Customer Insights credentials.

1. Select **Save** to complete the connection.

### Data privacy and compliance

When you enable Dynamics 365 Customer Insights to transmit data to ActiveCampaign, you allow transfer of data outside of the compliance boundary for Dynamics 365 Customer Insights, including potentially sensitive data such as Personal Data. Microsoft will transfer such data at your instruction, but you are responsible for ensuring that ActiveCampaign meets any privacy or security obligations you may have. For more information, see [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?linkid=396732).

Your Dynamics 365 Customer Insights administrator can remove this export destination at any time to discontinue use of this functionality.

## Configure an export

You can configure an export if you have access to a connection of this type. For more information, see [Permissions needed to configure an export](export-destinations.md#set-up-a-new-export).

1. Go to **Data** > **Exports**.

1. To create a new export, select **Add export**.

1. In the **Connection for export** field, choose a connection from the ActiveCampaign section. If you don't see this section name, there are no connections of this type available to you.

1. Enter your [**ActiveCampaign List ID**](https://help.activecampaign.com/hc/articles/360000030559-How-to-create-a-list-in-ActiveCampaign).

1. In the **Data matching** section, in the **Email** field, select the field that represents a customer's email address. It's required to export segments to ActiveCampaign. Optionally, you can export First name, Last name, and Phone to create more personalized emails. Select Add attribute to map these fields.

1. Select **Save**.

Saving an export doesn't run the export immediately.

The export runs with every [scheduled refresh](system.md#schedule-tab). 
You can also [export data on demand](export-destinations.md#run-exports-on-demand).
