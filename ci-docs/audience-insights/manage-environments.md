---
title: "Create and manage environments"
description: "Learn how to sign up for the service and how to manage environments."
ms.date: 03/16/2022
ms.subservice: audience-insights
ms.topic: how-to
ms.reviewer: mhart
author: NimrodMagen, Aditya Kuppa
ms.author: nimagen, adkuppa
manager: shellyha
searchScope: 
  - ci-system-about
  - customerInsights
---

# Manage environments

## Switch environments

Select the **Environment** control in the upper-right corner of the page to change environments.

:::image type="content" source="media/home-page-environment-switcher.png" alt-text="Screenshot of the control to switch environments.":::

Administrators can [create](create-environment.md) and manage environments.

## Edit an existing environment

You can edit some of the details of existing environments.

1.	Select the **Environment** picker in the header of the app.

2.	Select the **Edit** icon.

3. In the **Edit environment** box, you can update the environment settings.

For more information on environment settings, see [Create a new environment](create-environment.md).

## Connect to Microsoft Dataverse
   
The **Microsoft Dataverse** step lets you connect Customer Insights with your Dataverse environment.

To use [out-of-box prediction models](predictions-overview.md#out-of-box-models), configure data sharing with Dataverse. Or you can enable data ingestion from on-premises data sources, providing the Microsoft Dataverse environment URL that your organization administers.

> [!IMPORTANT]
> Customer Insights and Dataverse have to be in the same region to enable data sharing.
> You must have global administrator role on the Dataverse environment
> There should not be any previous/existing CI instance associated with that Dataverse environment aleady. Refer [here](manage-environments.md#Remove an existing/previous connection from a CI instance to a Dataverse environment) on how to remove any existing associations

:::image type="content" source="media/dataverse-provisioning.png" alt-text="Configuration options to enable data sharing with Microsoft Dataverse.":::

> [!NOTE]
> Customer Insights does not support the following data sharing scenarios:
> - If you save all data to your own Azure Data Lake Storage, you won't be able to enable data sharing with a Dataverse-managed data lake.
> - If you enable data sharing with Dataverse, you won't be able to [create predicted or missing values in an entity](predictions.md).

### Remove an existing/previous connection from a CI instance to a Dataverse environment
If you get an error message "This CDS organization is already attached to another Customer Insights instance." when connecting to a Dataverse environment, it implies  that specific Dataverse environment has already has an association with an existing/previously active CI instance. Follow the below steps to remove that association to a previous CI instance. You must be a global administrator on the Dataverse environment to perform these changes. Note that these changes might not be synchronous and can take anywhere from a couple of minutes to a couple of hours.

1. Go to the maker portal https://make.powerapps.com
1. Select the appropriate environment from the top right side environment picker.
1. Go to the left side navigation and select "Solutions"
1. Uninstall/delete the solution named "Dynamics 365 Customer Insights Customer Card Add-in (Preview)"

Alternatively,
1. Go to the Dataverse environment (the https://xyz.crm.dynamics.com  link)
2. Navigate to "Advanced Settings" -> "Solutions"
3. Uninstall the solution named "CustomerInsightsCustomerCard"

## Copy the environment configuration

When you create a new environment, you can choose to copy the configuration from an existing environment. 

:::image type="content" source="media/environment-settings-dialog.png" alt-text="Screenshot of the settings options in the environment settings.":::

You'll see a list of all available environments in your organization where you can copy data from.

The following configuration settings are copied:

- Ingested/imported data sources
- Data unification (Map, Match, Merge) configuration
- Segments
- Measures
- Relationships
- Activities
- Search & filter Index
- Export destinations
- Scheduled refresh
- Enrichments
- Model management
- Role assignments

The following data is *not* copied:

- Customer profiles.
- Data source credentials. You'll have to provide the credentials for every data source and refresh the data sources manually.

- Data sources from the Common Data Model folder and Dataverse-managed data lake. You'll have to create those data sources manually with the same name as in the source environment.

When you copy an environment, you'll see a confirmation message that the new environment has been created. Select **Go to data sources** to see the list of data sources.

All the data sources will show a **Credentials Required** status. Edit the data sources and enter the credentials to refresh them.

:::image type="content" source="media/data-sources-copied.png" alt-text="List of data sources that were copied and need authentication.":::

After refreshing the data sources, go to **Data** > **Unify**. Here you'll find settings from the source environment. Edit them as needed or select **Run** to start the data unification process and create the unified customer entity.

When the data unification is complete, go to **Measures** and **Segments** to refresh them too.

## Change the owner of an environment

While several users can have admin permissions in Customer Insights, only one user is the owner of an environment. By default, it's the admin who creates an environment initially. As the admin of an environment, you can assign ownership to another user with admin permissions.

1. Select the **Environment** picker in the header of the app.

1. Select the **Edit** icon.

1. In the **Edit environment** box, go to the **Basic information** step.

1. In the **Change owner of environment** field, choose the new owner of the environment.  

1. Select **Review and finish**, then **Update** to apply the changes. 

## Claim ownership of an environment

If the owner of an environment leaves the organization or their user account is deleted, the environment will have no owner. A user with admin permissions can claim the ownership and become the new owner. They can continue to own the environment or [change the ownership to another admin](#change-the-owner-of-an-environment). 

To claim ownership, select the **Take ownership** button that shows at the top of every page in Customer Insights when the original owner left the organization.

## Reset an existing environment

As the owner of an environment, you can reset an environment to an empty state if you want to delete all configurations and remove the ingested data.

1.	Select the **Environment** picker in the header of the app. 

2.	Select the environment you want to reset and select the ellipsis (**...**). 

3. Choose the **Reset** option. 

4.	To confirm the deletion, enter the environment name and select **Reset**.

## Delete an existing environment

As the owner of an environment, you can delete an environment you administer.

1.	Select the **Environment** picker in the header of the app.

2.	Select the environment you want to reset and select the ellipsis (**...**). 

3. Choose the **Delete** option. 

4.	To confirm the deletion, enter the environment name and select **Delete**.


[!INCLUDE[footer-include](../includes/footer-banner.md)]
