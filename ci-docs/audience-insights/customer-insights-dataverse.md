---
title: "Customer Insights data in Microsoft Dataverse"
description: "Use Customer Insights entities as tables in Microsoft Dataverse."
ms.date: 04/05/2022
ms.reviewer: mhart

ms.subservice: audience-insights
ms.topic: conceptual
author: m-hartmann
ms.author: wimohabb
manager: shellyha
searchScope: 
  - ci-system-diagnostic
  - customerInsights
---

# Work with Customer Insights data in Microsoft Dataverse

Customer Insights provides the option to make output entities available in [Microsoft Dataverse](/powerapps/maker/data-platform/data-platform-intro). This integration enables easy data sharing and custom development through a low code/no code approach. The [output entities](#output-entities) are available as tables in a Dataverse environment. You can use the data for any other application based on Dataverse tables. These tables enable scenarios like automated workflows through Power Automate or building apps with Power Apps. The current implementation mainly supports lookups where data from the available Customer Insights entities can be fetched for a given customer ID.

## Attach a Dataverse environment to Customer Insights

**Existing organization**

Administrators can configure Customer Insights to [use an existing Dataverse environments](create-environment.md) when they create a Customer Insights environment. By providing the URL to the Dataverse environment, it's attaching to their new audience insights environment. Customer Insights and Dataverse environments must be hosted in the same region. 

If you don't want to use an existing Dataverse environment, the system creates a new environment for the Customer Insights data in your tenant. 

> [!NOTE]
> If your organizations already uses Dataverse in their tenant, it’s important to remember that [Dataverse environment creation is controlled by an admin](/power-platform/admin/control-environment-creation). For example, if a you're setting up a new audience insights environment with your organizational account and the admin has disabled the creation of Dataverse trial environments for everyone except admins, you can't create a new trial environment.
> 
> The Dataverse trial environments created in Customer Insights have 3 GB of storage which won't count towards the overall capacity entitled to the tenant. Paid subscriptions get Dataverse entitlement of 15 GB for database and 20 GB for file storage.

**New organization**

If you create a new organization when setting up Customer Insights, the system automatically creates a new Dataverse environment in your organization for you.

## Output entities

Some output entities from audience insights are available as tables in Dataverse. The sections below describe the expected schema of these tables.

- [CustomerProfile](#customerprofile)
- [AlternateKey](#alternatekey)
- [UnifiedActivity](#unifiedactivity)
- [CustomerMeasure](#customermeasure)
- [Enrichment](#enrichment)
- [Prediction](#prediction)
- [Segment membership](#segment-membership)


### CustomerProfile

This table contains the unified customer profile from Customer Insights. The schema for a unified customer profile depends on the entities and attributes used in the merge process. A customer profile schema usually contains a subset of the attributes from the [Common Data Model definition of CustomerProfile](/common-data-model/schema/core/applicationcommon/foundationcommon/crmcommon/solutions/customerinsights/customerprofile).

### AlternateKey

The AlternateKey table contains keys of the entities, which participated in the unify process.

|Column  |Type  |Description  |
|---------|---------|---------|
|DataSourceName    |String         | Name of the data source. For example: `datasource5`        |
|EntityName        | String        | Name of the entity in audience insights. For example: `contact1`        |
|AlternateValue    |String         |Alternative ID that is mapped to the customer ID. Example: `cntid_1078`         |
|KeyRing           | Multiline text        | JSON value  </br> Sample: [{"dataSourceName":" datasource5 ",</br>"entityName":" contact1",</br>"preferredKey":" cntid_1078",</br>"keys":[" cntid_1078"]}]       |
|CustomerId         | String        | ID of the unified customer profile.         |
|AlternateKeyId     | GUID         |  AlternateKey deterministic GUID based on msdynci_identifier       |
|msdynci_identifier |   String      |   `DataSourceName|EntityName|AlternateValue`  </br> Sample: `testdatasource|contact1|cntid_1078`    |

### UnifiedActivity

This table contains activities by users that are available in Customer Insights.

| Column            | Type        | Description                                                                              |
|-------------------|-------------|------------------------------------------------------------------------------------------|
| CustomerId        | String      | Customer Profile ID                                                                      |
| ActivityId        | String      | Internal ID of the customer activity (primary key)                                       |
| SourceEntityName  | String      | Name of the source entity                                                                |
| SourceActivityId  | String      | Primary key from the source entity                                                       |
| ActivityType      | String      | Semantic activity type or name of custom activity                                        |
| ActivityTimeStamp | DATETIME    | Activity Time stamp                                                                      |
| Title             | String      | Title or name of the activity                                                               |
| Description       | String      | Activity description                                                                     |
| URL               | String      | Link to an external URL specific to the activity                                         |
| SemanticData      | JSON String | Includes a list of key value pairs for semantic mapping fields specific to the type of activity |
| RangeIndex        | String      | Unix timestamp used for sorting activity timeline and effective range queries |
| mydynci_unifiedactivityid   | GUID | Internal ID of the customer activity (ActivityId) |

### CustomerMeasure

This table contains the output data of customer attribute-based measures.

| Column             | Type             | Description                 |
|--------------------|------------------|-----------------------------|
| CustomerId         | String           | Customer profile ID        |
| Measures           | JSON String      | Includes a list of key value pairs for measure name and values for the given customer | 
| msdynci_identifier | String           | `Customer_Measure|CustomerId` |
| msdynci_customermeasureid | GUID      | Customer profile ID |


### Enrichment

This table contains the output of the enrichment process.

| Column               | Type             |  Description                                          |
|----------------------|------------------|------------------------------------------------------|
| CustomerId           | String           | Customer profile ID                                 |
| EnrichmentProvider   | String           | Name of the provider for the enrichment                                  |
| EnrichmentType       | String           | Type of enrichment                                      |
| Values               | JSON String      | List of attributes produced by the enrichment process |
| msdynci_enrichmentid | GUID             | Deterministic GUID generated from msdynci_identifier |
| msdynci_identifier   | String           | `EnrichmentProvider|EnrichmentType|CustomerId`         |

### Prediction

This table contains the output of the model predictions.

| Column               | Type        | Description                                          |
|----------------------|-------------|------------------------------------------------------|
| CustomerId           | String      | Customer Profile ID                                  |
| ModelProvider        | String      | Name of the provider of the model                                      |
| Model                | String      | Model name                                                |
| Values               | JSON String | List of attributes produced by the model |
| msdynci_predictionid | GUID        | Deterministic GUID generated from msdynci_identifier | 
| msdynci_identifier   | String      |  `Model|ModelProvider|CustomerId`                      |

### Segment membership

This table contains segment membership information of the customer profiles.

| Column        | Type | Description                        |
|--------------------|--------------|-----------------------------|
| CustomerId        | String       | Customer Profile ID        |
| SegmentProvider      | String       | App that publishes the segments. Default: Audience insights         |
| SegmentMembershipType | String       | Type of the customer this segment membership record. Supports multiple types such as Customer, Contact, or Account. Default: Customer  |
| Segments       | JSON String  | List of unique segments the customer profile is a member of      |
| msdynci_identifier  | String   | Unique identifier of the segment membership record. `CustomerId|SegmentProvider|SegmentMembershipType|Name`  |
| msdynci_segmentmembershipid | GUID      | Deterministic GUID generated from `msdynci_identifier`          |
