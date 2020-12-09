---
title: Manage workspaces and environments
description: How to create, rename, and delete a workspaces and environments.
author: pickwick129
ms.reviewer: ruthai
ms.author: v-salash
ms.date: 11/17/2020
ms.service: customer-insights
ms.subservice: engagement-insights 
ms.topic: how-to
ms.manager: shellyha
---

# Manage environments and workspaces

[!INCLUDE [cc-beta-prerelease-disclaimer](includes/cc-beta-prerelease-disclaimer.md)]

## Overview

Environments and workspaces are used to store and manage your reports, events, and other data assets. An environment can contain one or more workspaces. Workspaces are used to manage your analytics and store your data like reports and events. 

### Environments

An environment is a space where you manage your workspaces and connections. How you use environments depends on your organization and your use case. 

For example: 
- Choose to have a single environment.
- Create separate environments for test and production.
- Create separate environments that correspond to specific teams or departments in your organization, containing the relevant events for each audience.
- Create separate environments for different global branches of your company.
- Create connections to Customer Insights audience insights capability.

### Workspaces 

A workspace is a space to store and manage events and reports. When you create a workspace, you select the kind of data you'll be sending the workspace. Currently, only web data is supported. Workspaces come with pre-defined reports. You can create custom reports using web metrics and dimensions.

## Manage a workspace

You can maintain multiple workspaces concurrently in an environment. As a workspace admin, you can rename existing workspaces, or delete them. 

To edit or delete a workspace, you have to select the workspace from the workspace switcher. 

:::image type="content" source="media/select-workspace.png" alt-text="Workspace switcher highlighted in engagement insights user interface":::

### Rename a workspace

1. Go to **Admin** > **Settings** > **General**.

1. In the **Workspace name** field, enter the new name.

1. Select **Save**.

### Delete a workspace

Deleting a workspace will permanently remove all of its content, data, settings, and permissions. It can't be undone.

1. Go to **Admin** > **Settings** > **General**.

1. Select **Delete Workspace**. 

1. In the **Delete workspace** dialog, enter **CONFIRM DELETE**. 

1. Select **Delete** to permanently delete the workspace.

### Manage workspace members

1. Go to **Admin** > **Settings** > **Members**.

1. Select **Add members** to update members and [assign roles](user-roles.md). Currently, only **Workspace admin** is available.

1. Select the check box if you want **Allow access to profile data**. This selection enables the member to see reports based on user profiles if you set up the [connection to audience insights](configure-connections.md).

1. Select **Add members** to add them to your workspace.

## Manage an environment

The admin center lets you manage engagement insights environments. It currently includes options to configure general settings, other environment admins, workspaces, and [connections to audience insights](configure-connections.md).

To access the environment admin center, you need to have an environment admin role.

Switch between the different areas in the admin center by selecting the corresponding tabs.

:::image type="content" source="media/environment-admin-center-tabs.png" alt-text="Environment admin center with callout on tabs":::

### Choose the environment to configure

1. Go to **Admin** > **Settings** > **General**.

1. Select **Go to admin center**.

   :::image type="content" source="media/open-admin-center.png" alt-text="Highlight on link to go to the admin center":::

1. To change an environment, select **Environments** in the navigation pane.

1. In the list, select the environment you want to configure.

### Rename an environment

1. Go to **Admin** > **Settings** > **General**.

1. Select **Go to admin center**.

1. Select **General**.

1. Update the **Environment name** and select **Save** to apply your changes.

### Manage environment members

1. Go to **Admin** > **Settings** > **General**.

1. Select **Go to admin center**.

1. Select **Members**.

1. Select **Add members** to update members and [assign roles](user-roles.md). Currently, only **Environment admin** is available.

1. Select the check box if you want **Allow access to profile data**. This selection enables the member to see reports based on user profiles if you set up the [connection to audience insights](configure-connections.md).

1. Select **Add members** to add them to your environment.

### Manage workspaces

1. Go to **Admin** > **Settings** > **General**.

1. Select **Go to admin center**.

1. Select **Workspaces**.

1. Select **...** next to the workspace name and choose one of the available options:
   - Choose **Edit name** to change the name of a workspace.
   - Choose **Delete** to remove a workspace.

### Manage connections

Establishing connections to audience insights lets you see reports in engagement insights based on unified customer profiles. 

For more information, see [Configure connections](configure-connections.md).

### Manage personal data

To protect your customer's personal data, you can delete or export end user identifiable data.

For more information, see [Delete and export event data containing personal information](delete-export-personal-data.md)
