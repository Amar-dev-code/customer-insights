---
title: "Export data to SFTP hosts (preview) (contains video)"
description: "Learn how to configure the connection and export to an SFTP location."
ms.date: 06/09/2022
ms.reviewer: mhart

ms.subservice: audience-insights
ms.topic: how-to
author: pkieffer
ms.author: philk
manager: shellyha
---

# Export data to SFTP (preview)

Use your customer data in third-party applications by exporting them to a Secure File Transfer Protocol (SFTP) location.

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RWO94X]

## Prerequisites for connection

- Availability of an SFTP host and corresponding credentials.

## Known limitations

- SFTP destinations behind firewalls are currently not supported. 
- If you are using an SSH key for authentication, you need to [convert your private key to use for Open SSH](https://www.tbs-certificates.co.uk/FAQ/en/putty-ppk-vers-openssl-openssh.html)
- The runtime of an export depends on your system performance. We recommend two CPU cores and 1 Gb of memory as minimal configuration of your server.
- Exporting entities with up to 100 million customer profiles can take 90 minutes when using the recommended minimal configuration of two CPU cores and 1 Gb of memory.

## Set up connection to SFTP

1. Go to **Admin** > **Connections**.

1. Select **Add connection** and choose **SFTP** to configure the connection.

1. Give your connection a recognizable name in the **Display name** field. The name and the type of the connection describe this connection. We recommend choosing a name that explains the purpose and target of the connection.

1. Choose who can use this connection. If you take no action, the default will be Administrators. For more information, see [Allow contributors to use a connection for exports](connections.md#allow-contributors-to-use-a-connection-for-exports).

1. Choose whether you want to authenticate through SSH or Username/Password for your connection and provide the necessary details. Note: If you are using an SSH key for authentication, you need to [convert your private key to use for Open SSH](https://www.tbs-certificates.co.uk/FAQ/en/putty-ppk-vers-openssl-openssh.html)

1. Select **Verify** to test the connection.

1. Select **I agree** to confirm the **Data privacy and compliance**.

1. Select **Save** to complete the connection.

## Configure an export

You can configure this export if you have access to a connection of this type. For more information, see [Permissions needed to configure an export](export-destinations.md#set-up-a-new-export).

1. Go to **Data** > **Exports**.

1. To create a new export, select **Add destination**.

1. In the **Connection for export** field, choose a connection from the SFTP section. If you don't see this section name, there are no connections of this type available to you.

1. Provide a display name for your export.

1. Choose if you want to export your data **Gzipped** or **Unzipped** and the **field delimiter** for the exported files.

1. Select the entities, for example segments, you want to export.

   > [!NOTE]
   > Each selected entity will be split up into up to five output files when exported.

1. Select **Save**.

Saving an export doesn't run the export immediately.

The export runs with every [scheduled refresh](system.md#schedule-tab).
You can also [export data on demand](export-destinations.md#run-exports-on-demand).

> [!TIP]
> Export of entities that contain a large amount of data can lead to multiple CSV files in the same folder for each export. Splitting exports happens for performance reasons to minimize the time it takes for an export to complete.

## Data privacy and compliance

When you enable Dynamics 365 Customer Insights to transmit data via SFTP, you allow transfer of data outside of the compliance boundary for Dynamics 365 Customer Insights, including potentially sensitive data such as Personal Data. Microsoft will transfer such data at your instruction, but you are responsible for ensuring that the export destination meets any privacy or security obligations you may have. For more information, see [Microsoft Privacy Statement](https://go.microsoft.com/fwlink/?linkid=396732).
Your Dynamics 365 Customer Insights Administrator can remove this export destination at any time to discontinue use of this functionality.

[!INCLUDE [footer-include](includes/footer-banner.md)]
