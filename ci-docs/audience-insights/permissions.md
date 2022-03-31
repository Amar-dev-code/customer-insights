---
title: "Manage user permissions"
description: "Learn about permissions and user roles."
ms.date: 02/09/2022
ms.reviewer: mhart

ms.subservice: audience-insights
ms.topic: conceptual
author: NimrodMagen
ms.author: nimagen
manager: shellyha
searchScope: 
  - ci-permissions
  - ci-system-security
  - customerInsights
---

# User permissions

The **Permissions** page is where you'll set up roles and permissions for using audience insights.

You need to have administrator permissions to see the page. To access the permissions page in audience insights, go to **Admin** > **Permissions**.

There are three types of roles:

## Viewer

- Explore insights and segments within the **Home** and **Segments** pages.
- Search and filter customer profiles using the **Customers** page. Fields must be searchable.
- View and explore the **Enrichment** page.
- Explore and export entities using the **Entities** page.
- View the status of system processes  using the **System** page.
- View exports in **Exports** page.
- Install and use the **Power BI Customer Insights** dashboard.

## Contributor

- All permissions available to the Viewer.
- Load and transform data using the **Data sources** page.
- Complete ***Data Unification** which result in the unified customer profile entity.
- Define **Relationships** and **Activities**.
- Create segments using the **Segments** page.
- Create measures using the **Measures** page.
- Manage configuration and enrich customer profiles from the **Enrichment** page (for first party enrichments only).
- Manage and create exports based on connections shared with contributors. [Learn more about how administrators allow contributors to use a connection for exports](connections.md#allow-contributors-to-use-a-connection-for-exports).

## Admin

- All permissions available to the Contributor.
- Change settings on the **System** page, including the working language and refresh schedules for your system processes.
- View and add permissions using the **Permissions** page.
- Set search and filter definitions for the Customers page using the **Search & filter index** page (accessible via the **Customers** page).
- Manage connections and allow them for other user roles on **Connections** page.
- Manage configuration and enrich customer profiles from the **Enrichment** page (for all enrichments).
- Manage and create exports on **Exports** page.
- Install and use the **Customer Card Add-in**.
- Add and use the **Power Apps connector**.
- Enable usage of [Customer Insights APIs](apis.md).
- [Assign environment ownership](manage-environments.md#change-the-owner-of-an-environment) to another admin.

## Admin (owner)

- All permissions available to the Admin.
- [Reset and delete](manage-environments.md#reset-an-existing-environment) the environment.

## Assign roles and permissions

1. In audience insights, go to **Admin** > **Permissions**.

1. Select **Add users** to open the **Add/Edit permissions** pane.

1. Use the **Search** field to find the Azure Active Directory user or group whose permissions you want to adjust. Select a **Role** to assign to that user or group.

1. Select **Save**. The current environment will automatically be shared with the user or members of the group whose permissions you've changed. Users can access the Customer Insights app and work according to their specified role.

## View current permissions

In audience insights, go to **Admin** > **Permissions** to see what role assignments are currently active.

- The **Type** column specifies a single user, group, or application. The system supports individual users and groups.
- Roles are specified under the **Role** column.
- Select any column title to sort the results by that column's value.
- Use the **Search** field at the top of the page to locate specific users.


[!INCLUDE[footer-include](../includes/footer-banner.md)]
