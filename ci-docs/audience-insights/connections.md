---
title: "Connections"
description: "Share data to other services."
ms.date: 01/03/2021
ms.reviewer: nikeller
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: conceptual
author: m-hartmann
ms.author: mhart
manager: shellyha
---

# Connections (preview) overview

Connections are the key to enabling data sharing to or from Customer Insights, including exports. Connections can only be configured by admins, who can also grant access to them for use in certain scenarios by specific roles. 

The **Connections** page shows you all connections you have setup. The list shows a row for each connection the columns expose relevant information for you to compare connections. Additionally, it shows all connections currently available. Get a quick overview, description, and find out what you can do with each extensibility option on the **Discover** pivot. 

Go to **Admin** > **Connections** to find possible connections under **Discover** and see the configured ones under **Connections**.

## Add a new connection

To add connections, you need to have [administrator permissions](permissions.md). If you connect to Microsoft services, we assume both services are in the same organization.

1. Go to **Admin** > **Connections (preview)**.

1. Switch to the **Connections** tab.

1. Select **Add connection** to create a new connection. Choose from the dropdown what kind of connection you want to set up.

1. In the **Set up connection** pane, select the ** ** of export destination in the drop-down.

1. Provide the required details which depend on what service you are connecting to. You can learn about details of specific connection type in the respective documentation page. 

1. To crate the connection select **Save**.

You can also select **Set up** on a tile on the **Discover** tab.

### Allow contributors to use a connection for exports
When setting up or editing a connection you choose which user roles are allowed to use this specific connection to define [exports](export-destinations.md). By default a connection is available to users with administrator role. The control **Choose who can use this connection** lets you change this to also allow users with role contributor to use this connection when they need to.

- Note this will not give them access to the Connections page or allow them to edit the connection itself. 
- By sharing a connection you empower contributors to use a connection. Contributors will see these Connections when they set up exports. Any export using this specific connection will be editable by contributors. 
- You can change this setting at anytime without loosing the exports defined by contributors.

## Edit a connection
1. Select the vertical ellipsis for the Connection you want to edit.

1. Select **Edit** from the dropdown menu.

1. Change the values that require update and select **Save**.

## Remove a connection

If the connection you are removing is used by exports, these will become inactive. You can activate them once you added another connection to them on the [Exports](export-destinations.md) page.

1. Select the vertical ellipsis for the Connection you want to edit.

1. Select **Remove** from the dropdown menu. A confirmation dialog will appear.

1. In the dialog window review the list of affected elements. To confirm the deletion select **Remove**.

