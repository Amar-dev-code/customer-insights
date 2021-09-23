---
title: "Connections to other services from Customer Insights."
description: "Share data to other services."
ms.date: 04/09/2021
ms.reviewer: nikeller
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: conceptual
author: m-hartmann
ms.author: mhart
manager: shellyha
---

# Connections (preview) overview

Connections are the key to enable data sharing to and from Customer Insights. Each connection establishes data sharing with a specific service. Connections are the foundation to [configure third-party enrichments](enrichment-hub.md) and [configure exports](export-destinations.md). The same connection can be used multiple times. For example, one connection to Dynamics 365 Marketing works for multiple exports and one Leadspace connection can be used for several enrichments.

Go to **Admin** > **Connections** to create and view connections.

The **Connections** tab shows you all active connections. The list shows a row for each connection. 

Get a quick overview, description, and find out what you can do with each extensibility option on the **Discover** tab.

### Exports

Only administrators can configure new connections but they can grant access to contributors to use existing connections. Administrators control where data can go, contributors define the payload and frequency fitting their needs. For more information, see [Allow contributors to use a connection for exports](#allow-contributors-to-use-a-connection-for-exports).

### Enrichments

Only administrators can configure new connections but the created connections are always available to both administrators and contributors. Administrators manage credentials and give consent to data transfers. The connections can then be used for enrichments by both administrators and contributors.

## Add a new connection

To add connections, you need to have [administrator permissions](permissions.md). If you connect to other Microsoft services, we assume both services are in the same organization.

1. Go to **Admin** > **Connections (preview)**.

1. Go to the **Connections** tab.

1. Select **Add connection** to create a new connection. Choose from the dropdown menu what type of connection you want to create.

1. In the **Set up connection** pane, provide the required details. 
   1. The **Display name** and the type of the connection describe a connection. We recommend choosing a name that explains the purpose and target of this connection.
   1. The exact fields depend on what service you are connecting to. You can learn about details of a specific connection type in the article about the target service.

1. To create the connection, select **Save**.

You can also select **Set up** on a tile on the **Discover** tab.

### Allow contributors to use a connection for exports

When setting up or editing an export connection, you choose which users are allowed to use this specific connection to define [exports](export-destinations.md). By default a connection is available to users with an administrator role. You can change this setting under **Choose who can use this connection** and allow users with contributor role to use this connection.

- Contributors won't be able to view or edit the connection. They will only see the display name and its type when creating an export.
- By sharing a connection, you allow contributors to use a connection. Contributors will see shared connections when they set up exports. They can manage every export that uses this specific connection.
- You can change this setting while keeping the exports that have already been defined by contributors.

## Edit a connection

1. Go to **Admin** > **Connections (preview)**.

1. Go to the **Connections** tab.

1. Select the vertical ellipsis for the connection you want to edit.

1. Select **Edit**.

1. Change the values you want to update and select **Save**.

## Remove a connection

If the connection you are removing is used by enrichments or exports, you first need to detach or remove them. The remove dialog will guide you to the relevant enrichments or exports. 

Detached enrichments and exports become inactive. You reactivate them by adding another connection to them on the [Enrichments](enrichment-hub.md) or [Exports](export-destinations.md) page.

1. Go to **Admin** > **Connections (preview)**.

1. Go to the **Connections** tab.

1. Select the vertical ellipsis for the connection you want to remove.

1. Select **Remove** from the dropdown menu. A confirmation dialog appears.

   1. If there are enrichments or exports using this connection, select the button to see what's using the connection.
      - **Exports:** You can choose to either remove or disconnect the exports to be able to remove the connection. To disconnect an export, administrators can use the **Disconnect** action. This action is available for individual and multiple selected exports. By disconnecting you keep the export config, but it won't be run until another connection is added to it.
      - **Enrichments:** You can choose to either remove or deactivate the enrichments to be able to remove the connection. 
   1. Once the connection has no more dependencies, go back to **Admin** > **Connections** and try removing the connection again.

1. To confirm the deletion, select **Remove**.

## Setup Connections with Secrets from your own Key Vault

Some connections do need secrets like API Keys, Passwords, etc. Connections support secret configuration with your own Key Vault. Learn more about supported connections and how to setup on [Bring Your Own Key Vault](byo-key-vault.md).
