---
title: "Merge entities in data unification"
description: "Merge entities to create unified customer profiles."
ms.date: 01/28/2022

ms.subservice: audience-insights
ms.topic: tutorial
author: adkuppa
ms.author: adkuppa
ms.reviewer: mhart
manager: shellyha
searchScope: 
  - ci-match
  - ci-merge
  - ci-relationships
  - customerInsights
---

# Merge entities

The merge phase is the last phase in the data unification process. Its purpose is reconciling conflicting data. Examples of conflicting data could include a customer name found in two of your datasets but that shows up a little differently in each ("Grant Marshall" versus "Grant Marshal"), or a phone number that differs in format (617-803-091X versus 617803091X). Merging those conflicting data points is done on an attribute-by-attribute basis.

:::image type="content" source="media/merge-fields-page.png" alt-text="Merge page in the data unification process showing table with merged fields that define the unified customer profile.":::

After completing the [match phase](match-entities.md), you start the merge phase by selecting the **Merge** tile on the **Unify** page.

## Review system recommendations

On **Data** > **Unify** > **Merge**, you choose and exclude attributes to merge within your unified customer profile entity. The unified customer profile is the result of the data unification process. Some attributes are automatically merged by the system.

To view the attributes that are included in one of your automatically merged attributes, select that merged attribute in the **Customer fields** tab of the table. The attributes that compose that merged attribute display in two new rows beneath the merged attribute.

## Separate, rename, exclude, and edit merged fields

You can change how the system processes merged attributes to generate the unified customer profile. Select **Show more** and choose what you want to change.

:::image type="content" source="media/manage-merged-attributes.png" alt-text="Options in the Show more dropdown menu to manage merged attributes.":::

For more information, see the following sections.

## Separate merged fields

To separate merged fields, find the attribute in the table. Separated fields show as individual data points on the unified customer profile. 

1. Select the merged field.
  
1. Select **Show more** and choose **Separate fields**.
 
1. Confirm the separation.

1. Select **Save** and **Run** to process the changes.

## Rename merged fields

Change the display name of merged attributes. You can't change the name of the output entity.

1. Select the merged field.
  
1. Select **Show more** and choose **Rename**.

1. Confirm the changed display name. 

1. Select **Save** and **Run** to process the changes.

## Exclude merged fields

Exclude an attribute from the unified customer profile. If the field is used in other processes, for example in a segment, remove it from these processes before excluding it from the customer profile. 

1. Select a merged field.
  
1. Select **Show more** and choose **Exclude**.

1. Confirm the exclusion.

1. Select **Save** and **Run** to process the changes. 

On the **Merge** page, select **Excluded fields** to see the list of all excluded fields. This pane lets you add excluded fields back.

## Edit a merged field

1.	Select a merged field.

1.	Select **Show more** and choose **Edit**.

1.	Specify how to combine or merge the fields from one of three options:
    - **Importance**: Identifies the winner value based on importance rank specified for the participating fields. It's the default merge option. Select **Move up/down** to set the importance ranking.
    :::image type="content" source="media/importance-merge-option.png" alt-text="Importance option in the merge fields dialog."::: 
    - **Most recent**: Identifies the winner value based on the most recency. Requires a date or a numeric field for every participating entity in the merge fields scope to define the recency.
    :::image type="content" source="media/recency-merge-option.png" alt-text="Recency option in the merge fields dialog.":::
    - **Least recent**: Identifies the winner value based on the least recency. Requires a date or a numeric field for every participating entity in the merge fields scope to define the recency.

1.	You can add more fields to participate in the merge process.

1.	You can rename the merged field.

1. Select **Done** to apply your changes.

1. Select **Save** and **Run** to process the changes. 

## Combine fields manually

Specify a merged attribute manually.

1. On the **Merge** page, select **Combine**.

1. Choose the **Fields** option.

1. Specify the merge winner policy in the **Combine fields by** dropdown.

1. Choose a field to add. Select **Add fields** to combine more fields.

1. Provide a **Name** and an **Output field name**.

1. Select **Done** to apply the changes.

1. Select **Save** and **Run** to process the changes. 

## Combine a group of fields

Treat a group of fields as a single unit. For example, when if our records contain the fields Address1, Address2, City, State, and Zip. We likely don't want to merge in a different record’s Address2, thinking it would make our data more complete

1. On the **Merge** page, select **Combine**.

1. Choose the **Group of fields** option.

1. Specify the merge winner policy in the **Rank groups by** dropdown.

1. Select **Add** and choose if you want to add more fields or additional groups to the fields.

1. Provide a **Name** and an **Output name** for every combined field.

1. Provide a **Name** for the group of fields. 

1. Select **Done** to apply the changes.

1. Select **Save** and **Run** to process the changes.

## Change the order of fields

Some entities contain more details than others. If an entity includes the latest data about a field, you can prioritize it over other entities when merging values.

1. Select the merged field.
  
1. Select **Show more** and choose **Edit**.

1. In the **Combine fields** pane, select **Move up/down** to set the order or drag and drop them in the desired position.

1. Confirm the change.

1. Select **Save** and **Run** to process the changes.

## Configure Customer ID generation 

After configuring merging fields, you can define how to generate CustomerId values, the unique customer profile identifiers. 
The merge step in the data unification process generates the unique customer profile identifier. The identifier is the CustomerId in the *Customer* entity that results from the data unification process. 

The CustomerId in the Customer entity is based on a hash of the first value of the non-null winner primary keys. These keys come from the entities used in the match and merge phase and are influenced by the match order. So the generated CustomerID can change when a primary key value changes in the primary entity of the match order. So the primary key value might not always represent the same customer.

Configuring a stable customer ID enables you to avoid that behavior.

**Configure a unique customer ID**

1. Go to **Unify** > **Merge**.

1. Select the **Keys** tab. 

1. Hover on the **CustomerId** row and select the **Configure** option.
   :::image type="content" source="media/customize-stable-id.png" alt-text="Control to customize the ID generation.":::

1. Select up to five fields that will comprise a unique customer ID and are more stable. Records that don’t match your configuration use a system-configured ID instead.  

1. Select **Done** and run the merge process to apply your changes.

## Group profiles into households or clusters

As part of the customer profile generation configuration process, you can define rules to group related profiles into a cluster. There are currently two types of clusters available – household and custom clusters. The system automatically chooses a household with predefined rules if the *Customer* entity contains the semantic fields *Person.LastName* and *Location.Address*. You can also create a cluster with your own rules and conditions, similar to [match rules](match-entities.md#define-rules-for-match-pairs).

**Define a household or a cluster**

1. Go to **Unify** > **Merge**.

1. On the **Merge** tab, select **Advanced** > **Create cluster**.

   :::image type="content" source="media/create-cluster.png" alt-text="Control to create a new cluster.":::

1. Choose between a **Household** or a **Custom** cluster. If the semantic fields *Person.LastName* and *Location.Address* exist in the *Customer* entity, household is automatically selected.

1. Provide a name for the cluster and select **Done**.

1. Select the **Clusters** tab to find the cluster you created.

1. Specify the rules and conditions to define your cluster.

1. Select **Run** to run the merge process and create the cluster.

After running the merge process, the cluster identifiers are added as new fields to the *Customer* entity.

## Run your merge

Whether you manually merge attributes or let the system merge them, you can always run your merge. Select **Run** on the **Merge** page to start the process.

> [!div class="mx-imgBorder"]
> ![Data merge Save and Run.](media/configure-data-merge-save-run.png "Data merge Save and Run")

Choose **Run only Merge** if you only want to see the output reflected in the unified customer entity. Downstream processes will be refreshed as [defined in the refresh schedule](system.md#schedule-tab).

Choose **Run Merge and downstream processes** to refresh the system with your changes. All processes, including enrichment, segments, and measures will rerun automatically. After all downstream processes have completed, the customer profiles reflect any changes you made.

To make more changes and rerun the step, you can cancel an in-progress merge. Select **Refreshing ...** and select **Cancel job**  in the side pane that appears.

[!INCLUDE [progress-details-include](../includes/progress-details-pane.md)]

:::image type="content" source="media/process-detail-path.png" alt-text="Drill-down path to get to process details from the task status link.":::

## Next Step

Configure [activities](activities.md), [enrichment](enrichment-hub.md), or [relationships](relationships.md) to gain more insights about your customers.

If you already configured activities, enrichment, or segments, they'll be processed automatically to use the latest customer data.

[!INCLUDE[footer-include](../includes/footer-banner.md)]
