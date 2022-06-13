---
title: "Export segments to Mailchimp (preview)"
description: "Learn how to configure the connection and export to Mailchimp."
ms.date: 10/08/2021
ms.reviewer: mhart

ms.subservice: audience-insights
ms.topic: how-to
author: pkieffer
ms.author: philk
manager: shellyha
---

# Export segments to Mailchimp (preview)

Export segments of unified customer profiles to Mailchimp to create newsletters and email campaigns.

## Prerequisites for connection

-	You have a [Mailchimp account](https://mailchimp.com/) and corresponding administrator credentials.
-	There are existing audiences in Mailchimp and the corresponding IDs. For more information, see [Mailchimp audiences](https://mailchimp.com/help/create-audience/).
-	You have [configured segments](segments.md)
-	Unified customer profiles in the exported segments contain a field representing an email address.

## Known limitations

- Up to 1 million customer profiles per export to Mailchimp.
- Exporting to Mailchimp is limited to segments.
- Exporting segments with 1 million customer profiles can take up to three hours. 
- The number of customer profiles that you can export to Mailchimp is dependent and limited on your contract with Mailchimp.

## Set up connection to Mailchimp

1. Go to **Admin** > **Connections**.

1. Select **Add connection** and choose **Mailchimp** to configure the connection.

1. Give your connection a recognizable name in the **Display name** field. The name and the type of the connection describe this connection. We recommend choosing a name that explains the purpose and target of the connection.

1. Choose who can use this connection. If you take no action, the default will be Administrators. For more information, see [Allow contributors to use a connection for exports](connections.md#allow-contributors-to-use-a-connection-for-exports).

1. Select **I agree** to confirm the **Data privacy and compliance**.

1. Select **Connect** to initialize the connection to Mailchimp.

1. Select **Authenticate with Mailchimp** and provide your Mailchimp credentials.

1. Select **Add yourself as export user** and provide your Customer Insights credentials.

1. Select **Save** to complete the connection. 

## Configure the connector

You can configure this export if you have access to a connection of this type. For more information, see [Permissions needed to configure an export](export-destinations.md#set-up-a-new-export).

1. Go to **Data**> **Exports**.

1. To create a new export, select **Add destination**.

1. In the **Connection for export** field, choose a connection from the Mailchimp section. If you don't see this section name, there are no connections of this type available to you.

1. Enter your **[Mailchimp audience ID](https://mailchimp.com/help/find-audience-id/)**

1. In the **Data matching** section, in the **Email** field, select the field that represents a customer's email address. 

1. Optionally, you can export **First name** and **Last name** to create more personalized emails. Select **Add attribute** to map these fields.

1. Select the segments you want to export. You can export up to 1 million customer profiles in total to Mailchimp.

1. Select **Save**.

Saving an export doesn't run the export immediately.

The export runs with every [scheduled refresh](system.md#schedule-tab). 
You can also [export data on demand](export-destinations.md#run-exports-on-demand). 

## Data privacy and compliance

When you enable Dynamics 365 Customer Insights to transmit data to Mailchimp, you allow transfer of data outside of the compliance boundary for Dynamics 365 Customer Insights, including potentially sensitive data such as Personal Data. Microsoft will transfer such data at your instruction, but you are responsible for ensuring that Mailchimp meets any privacy or security obligations you may have. For more information, see [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?linkid=396732).
Your Dynamics 365 Customer Insights Administrator can remove this export destination at any time to discontinue use of this functionality.

[!INCLUDE [footer-include](includes/footer-banner.md)]
