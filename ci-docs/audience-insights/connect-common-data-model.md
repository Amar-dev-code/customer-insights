---
title: "Connect Common Data Model data to an Azure Data Lake account"
description: "Work with Common Data Model data using Azure Data Lake Storage."
ms.date: 05/29/2020
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: conceptual
author: m-hartmann
ms.author: mhart
ms.reviewer: adkuppa
manager: shellyha
---

# Connect to a Common Data Model folder using an Azure Data Lake account

This article provides information on how to ingest data from a Common Data Model folder using your Azure Data Lake Storage Gen2 account.

## Important considerations

- Data in your Azure Data Lake needs to follow the Common Data Model standard. Other formats aren't supported at the moment.

- Data ingestion supports Azure Data Lake *Gen2* storage accounts exclusively. You can't use Azure Data Lake Gen1 storage accounts to ingest data.

- Audience Insights Azure AD Service Principal is provisioned in your tenant and has access to the storage account you want to connect to. Follow the instructions [here](connect-ADLS-SPN.md) on how to complete these two prerequisites.

- The Azure Data Lake you want to connect and ingest data from have to be in the same Azure region as the Dynamics 365 Customer Insights environment. Connecting to a Common Data Model folder from an Azure Data Lake in a different Azure region is not supported. To know the Azure region of the environment, go to **Admin** > **System** > **About** in audience insights.

- Data stored in online services, such as Azure Data Lake Storage, may be stored in a different location than where data is processed or stored in Dynamics 365 Customer Insights. By importing or connecting to data stored in online services, you agree that data can be transferred to and stored with Dynamics 365 Customer Insights. [Learn more at the Microsoft Trust Center.](https://www.microsoft.com/trust-center)

## Connect to a Common Data Model folder

1. In audience insights, go to **Data** > **Data sources**.

2. Select **Add data source**.

3. Select **Connect to a Common Data Model folder**, enter a **Name** for the data source and select **Next**.

5. Select an option from the "Connect your storage account using" field and fill in the details accordingly. Refer to this [document](connect-ADLS-SPN.md#enter-the-azure-resource-id-or-the-azure-subscription-details-in-the-storage-account-attachment-to-audience-insights) on what are the prerequisites, how to cpature the Azure artifact details and how to fill in. Enter the **Container** information and select **Next**.
   > [!div class="mx-imgBorder"]
   > ![Dialog box to enter connection details for Azure Data Lake](media/enter-new-storage-details.png)

6. In the **Select a Common Data Model folder** dialog, select the model.json file to import data from and select **Next**.
   > [!NOTE]
   > Any model.json file associated with another data source in the environment won't show in the list.

7. You'll get a list of available entities in the selected model.json file. You can review and select from the list of available entities and select **Save**. All of the selected entities will be ingested from the new data source.
   > [!div class="mx-imgBorder"]
   > ![Dialog box showing a list of entities from a model.json file](media/review-entities.png)

8. Indicate which data entities you want to enable data profiling and select **Save**. Data profiling enables analytics and other capabilities. You can select the whole entity which selects all attributes from the entity, or select certain attributes of your choice. By default, no entity is enabled for data profiling.
   > [!div class="mx-imgBorder"]
   > ![Dialog box showing a data profiling](media/dataprofiling-entities.png)

9. After saving your selections, the **Data sources** page opens. You should now see the Common Data Model folder connection as a data source.

> [!NOTE]
> A model.json file can only associate with one data source in the same environment. However, the same model.json file can be used for data sources in multiple environments.

## Edit a Common Data Model folder data source

You can update the access key for the storage account containing the Common Data Model folder. You may also change the model.json file. To connect to a different container from your storage account, or change the account name, [create a new data source connection](#connect-to-a-common-data-model-folder).

1. In audience insights, go to **Data** > **Data sources**.

2. Next to the data source you'd like to update, select the ellipsis.

3. Select the **Edit** option from the list.

4. Optionally, update the **Access key** and select **Next**.

   ![Dialog to edit and update an access key for an existing data source](media/edit-access-key.png)

5. Optionally, you can update from storage account key based connection to a resource or a subscription based connection. Once upgraded, you cannot revert to account key as this is a one time update. Select either of these options from the "Connect your storage account using" options and refer to this [document](connect-ADLS-SPN.md#enter-the-azure-resource-id-or-the-azure-subscription-details-in-the-storage-account-attachment-to-audience-insights) on what are the prerequisites, how to capture the Azure artifact details and how to fill in. Note that the **Container** information cannot be edited as we are only updating the connection mechanism to the storage account and not changing the container.
   > [!div class="mx-imgBorder"]
   > ![Dialog box to enter connection details for Azure Data Lake](media/enter-existing-storage-details.png)

6. Optionally, choose a different model.json file with a different set of entities from the container.

7. Optionally, you can select additional entities to ingest. You can also remove any already selected entities if there are no dependencies.

   > [!IMPORTANT]
   > If there are dependencies on the existing model.json file and the set of entities, you'll see an error message and can't select a different model.json file. Remove those dependencies before changing the model.json file or create a new data source with the model.json file that you want to use to avoid removing the dependencies.

8. Optionally, you can select additional attributes or entities to enable data profiling on or disable already selected ones.   
