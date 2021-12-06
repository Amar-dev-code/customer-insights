---
title: "Entities and datasets"
description: "View data on the Entities page."
ms.date: 12/06/2021
ms.reviewer: mhart
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: conceptual
author: mukeshpo
ms.author: mukeshpo
manager: shellyha
---

# Entities in audience insights

After [configuring your data sources](data-sources.md), go to the **Entities** page to evaluate the quality of the ingested data. Entities are considered datasets. Multiple capabilities of Dynamics 365 Customer Insights are built around these entities. Reviewing them closely can help you validate the output of those capabilities.

The **Entities** page lists entities and includes these columns:

- **Name**: The name of the data entity. If you see a warning symbol next to an entity name, it means that the data for that entity didn't load successfully.
- **Source**: Type of data source that ingested the entity.
- **Updated**: Time the entity was last updated.
- **Status**: Details about the last update of the entity.

[!INCLUDE [progress-details-include](../includes/progress-details-pane.md)]

## Explore a specific entity's data

1. In audience insights, go to **Data** > **Entities**.
1. From the **Entities** page, select an entity to open the details page.  
1. Explore the different fields and records included for that entity.

- The **Attributes** tab is selected by default and shows a table to review details for the selected entity, such as field names, data types, and types. The **Type** column shows Common Data Model associated types, which are either auto-identified by the system or [manually mapped](map-entities.md) by users. These types are semantic types that can differ from the attributes' data types. For example, the field *Email* below has a data type *Text* but its (semantic) Common Data Model type might be *Email* or *EmailAddress*.

> [!div class="mx-imgBorder"]
> ![Fields table.](media/data-manager-entities-fields.PNG "Fields table")

> [!NOTE]
> This page shows only a sample of your entity's data. To view the full data set, go to the **Data sources** page, select an entity, select **Edit**, and then view this entity's data with the Power Query editor as explained in [Data sources](data-sources.md).

To learn more about the data ingested in the entity, the **Summary** column provides you with some important characteristics of the data, such as nulls, missing values, unique values, counts, and distributions, as applicable to your data. Select the chart icon to see the summary of the data.

> [!div class="mx-imgBorder"]
> ![Summary symbol.](media/data-manager-entities-summary.png "Data summary table")

- The **Data** tab shows a table listing details about individual records of the entity. Details listed depend on the entity's data type.

> [!div class="mx-imgBorder"]
> ![Select an entity.](media/data-manager-entities-data.png "Select an entity")

- The **Reports** tab (available for some entities) enables you to visualize your data by creating a report, and includes these columns:

  - **Report name**: Name of the report.
  - **Created by**: Name of the person who created the entity.
  - **Created**: Date and time of the entity creation.
  - **Edited by**: Name of the person who modified the entity.
  - **Edited**: Date and time of the entity modification. 

## Entity-specific information

The following section provides information about some system-created entities.

### Corrupted data sources

Fields from an ingested data source can contain corrupted data. Records with corrupted fields are exposed in system-created entities. Knowing about corrupted records helps you identify which data to review and update on the source system. After the next refresh of the data source, the corrected records are ingested to Customer Insights and passed on to downstream processes. 

For example, a 'birthday' column has the datatype set as 'date'. A customer record has their birthday entered as '01/01/19777'. The system will flag this record as corrupted. Someone can now change the birthday in the source system to '1977'. After an automated refresh of data sources, the field now has a valid format and the record will be removed from the corrupted entity. 

Go to **Data** > **Entities** and look for the corrupted entities in the **System** section. Naming schema of corrupted entities: 'DataSourceName_EntityName_corrupt'.

Customer Insights still processes corrupted records. However, they might cause issues when working with the unified data.

The following checks run on the ingested data to expose corrupted records: 

- The value of a field doesn't match with the data type of its column.
- Fields contain characters that cause the columns to not match the expected schema. For example: incorrectly formatted quotes, unescaped quotes, or newline characters.
- If there are datetime/date/datetimeoffset columns, their format needs to be specified in the model if it doesn't follow the standard ISO format.


[!INCLUDE[footer-include](../includes/footer-banner.md)]
