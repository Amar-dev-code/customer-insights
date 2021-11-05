---
title: "Audit and Observe Dynamics 365 Customer Insights with Azure Monitor | Microsoft Docs"
description: "Learn how to send logs to Microsoft Azure Monitor."
ms.date: 04/11/2021
ms.reviewer: mhart
ms.service: dynamics-365-ai
ms.topic: "article"
author: brndkfr, andbalan
ms.author: bkief, andbalan
manager: shellyha
---

# Observe Dynamics 365 Customer Insights with Azure Monitor (Preview)

Dynamics 365 Customer Insights is integrated with Microsoft Azure Monitor. With Azure Monitor resource logs, you can monitor and send logs to [Azure Storage](https://azure.microsoft.com/services/storage/), to [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/logs/log-analytics-overview) or stream them to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).

Dynamics 365 Customer Insights is sending event logs to the destination :

- **Audit Events**
  - **APIEvents** - enables change tracking done via the Dynamics 365 Customer Insights UI.
- **Operational Events**
  - **Workflow Monitoring** - The Workflow allows one to setup [Data Sources](data-sources.md), [unify](data-unification.md) and [enrich](enrichment-hub.md) and finally [export](export-destinations.md) data into other systems. All those steps can be done individually (e.g. trigger a single export) or orchestrated (e.g. data refresh from data sources which trigger the unification process which will pull in additional enrichments and once done export the data into another system). For more details see the [WorkflowEvent Schema](#workflow-event-schema).
  - **APIEvents** - all API calls to the customers instance to Dynamics 365 Customer Insights. For more details see the [APIEvent Schema](#api-event-schema).

## Set up the diagnostic settings

### Prerequisites

To configure the diagnostic setup in Customer Insights, the following prerequisites must be met:

- You have an active [Azure Subscription](https://azure.microsoft.com/pricing/purchase-options/pay-as-you-go/).
- You have [Administrator](permissions.md#administrator) permissions in Customer Insights.
- You have the **Contributor** and **User Access Administrator** role on the destination resource on Azure. The resource can be an Azure Storage account, an Azure Event Hub or an Azure Log Analytics workspace. For more information, see [Add or remove Azure role assignments using the Azure portal](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).
- Ensure that the [Destination requirements](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings#destination-requirements) for Azure Storage, Azure Event Hub or Azure Log Analytics are met.
- You have at least the **Reader** role on the resource group the resource belongs to.

### Set up diagnostics with Azure Monitor

1. In Customer Insights, select **System** > **Diagnostic** to see the diagnostics destinations configured this instance.

1. Select **Add destination**.

   > [!div class="mx-imgBorder"]
   > ![Diagnostics connection](media/diagnostics-pane.png "Diagnostics connection")

1. Provide a name in the **Name for diagnostics destination** field.

1. Choose the **Tenant** of the Azure subscription with the destination resource and select **Sign in**.

1. Select the **Resource Type** (Storage account, Event hub or Log Analytics).

1. Select the **Subscription** containing the destination resource.

1. Select the **Resource group** containing the destination resource.

1. Select the **Resource**.

1. Confirm the **Data privacy and compliance** statement.

- Select **Connect to system** to connect to the destination resource. The logs start to appear in the destination after 15 minutes, assuming the API is in use and generates events.

### Remove a destination

1. Go to **System** > **Diagnostics**.

1. Select the diagnostics destination in the list.

1. In the **Actions** column, select the trash bin icon.

1. Confirm the deletion to stop the log forwarding. The resource on the Azure subscription won't be deleted. You can select the link in the Actions column to open the Azure portal for the selected resource and delete it there.

## Log Categories and Event Schemas

Currently [API events](apis.md) and Workflow events are supported and the following categories and schema apply.
The log schema is following the [Azure Monitor common schema](https://docs.microsoft.com/azure/azure-monitor/platform/resource-logs-schema#top-level-common-schema).

### Categories

Customer Insights provides two categories:

- **Audit Events** -  [API Events](#api-event-schema) tracking the configuration changes on the service. `POST|PUT|DELETE|PATCH` operations go into this category.
- **Operational Events** - [API](#api-event-schema) or [Workflow Events](#workflow-event-schema) generated while using the service, for example `GET` requests or the execution events of a workflow.

### Configuration on the destination resource

Based on your choice on the resource type the following steps will automatically apply:

#### **Storage Account**

Customer Insights Service Principal will be granted `Storage Account Contributor` permission on the selected resource and will create two containers under the selected namespace:

- `insight-logs-audit` containing **Audit Events**
- `insight-logs-operational` containing **Operational Events**

#### **Event Hub**

Customer Insights Service Principal will be granted `Azure Event Hubs Data Owner` permission on the resource and will create two EventHubs under the selected namespace:

- `insight-logs-audit` containing **Audit Events**
- `insight-logs-operational` containing **Operational Events**

#### **Log Analytics**

Customer Insights Service Principal will be granted `Log Analytics Contributor` permission to the resource. The logs will be available under `Logs > Tables > LogManagement` on the selected LogAnalitycs workspace. Expand the Log Management solution and locate the `CIEventsAudit` and `CIEventsOperational` tables.

- `CIEventsAudit` containing **Audit Events**
- `CIEventsOperational` containing **Operational Events**

Under the Queries window expand the Audit solution and locate the example queries provided by searching for `CIEvents`.

### General Schema

API events and Workflow events have a common structure and details where they differ, see [API event schema](#api-event-schema) or [Workflow event schema](#workflow-event-schema).

### API event schema

| Field             | DataType  | Required/Optional | Description                                                                                                                                                     | Example                                                                                                                                                                  |
| ----------------- | --------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `time`            | Timestamp | Required          | Timestamp of the event (UTC)                                                                                                                                    | `2020-09-08T09:48:14.8050869Z`                                                                                                                                           |
| `resourceId`      | String    | Required          | ResourceId of the instance that emitted the event                                                                                                               | `/SUBSCRIPTIONS/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX/RESOURCEGROUPS/<RESOURCEGROUPNAME>/PROVIDERS/MICROSOFT.D365CUSTOMERINSIGHTS/INSTANCES/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX` |
| `operationName`   | String    | Required          | Name of the operation represented by this event.                                                                                                                | `Workflows.GetWorkFlowStatusAsync`                                                                                                                                       |
| `category`        | String    | Required          | Log category of the event. Either `Operational` or `Audit`. All POST/PUT/PATCH/DELETE HTTP Requests are tagged with `Audit`, everything else with `Operational` | `2020-09-08T09:48:14.8050869Z`                                                                                                                                           |
| `resultType`      | String    | Required          | Status of the event. `Success`, `ClientError`, `Failure`                                                                                                        |                                                                                                                                                                          |
| `resultSignature` | String    | Optional          | Sub status of the event. If the operation corresponds to a REST API call, it's the HTTP status code.                                                            | `200`                                                                                                                                                                    |
| `durationMs`      | Long      | Optional          | Duration of the operation in milliseconds                                                                                                                       | `133`                                                                                                                                                                    |
| `callerIpAddress` | String    | Optional          | Caller IP address, if the operation corresponds to an API call that would come from an entity with a publicly available IP address                              | `144.318.99.233`                                                                                                                                                         |
| `identity`        | String    | Optional          | JSON blob describing the identity of the user or application that did the operation.                                                                            | See sub section [Identity](#identity-schema)                                                                                                                             |  |
| `properties`      | String    | Optional          | JSON blob with additional properties to the particular category of events.                                                                                      | See sub section [Properties](#api-properties-schema)                                                                                                                     |
| `level`           | String    | Required          | Severity level of the event                                                                                                                                     | Is one of `Informational`, `Warning`, `Error`, or `Critical`                                                                                                             |
| `uri`             | String    | Optional          | Absolute request URI                                                                                                                                            |                                                                                                                                                                          |

#### Identity schema

The `identity` JSON blob has the following structure

```json
{
  "Authorization" : {
    "UserRole": "Admin",
    "RequiredRoles": [
      "Contributor",
      "Viewer"
      ]
    },
  "Claims" {
    "claimNameX" : "claimValueX",
    "claimNameY" : "claimValueY"
   }
}  
```

| Field                         | Description                                                                                                                                               |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Authorization.UserRole`      | Assigned role for the user or app. For more information, see [User permissions](https://docs.microsoft.com/dynamics365/ai/customer-insights/permissions). |
| `Authorization.RequiredRoles` | Required roles to do the operation. `Admin` role is allowed to do all operations.                                                                         |
| `Claims`                      | Claims of the user or app JSON web token (JWT). Claim properties vary per organization and the Azure Active Directory configuration.                      |

#### API Properties schema

[API events](apis.md) have following properties.

| Field                        | Description                                                                                                            |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `properties.eventType`       | always `ApiEvent`, marking the log event as API event                                                                  |
| `properties.userAgent`       | Browser agent sending the request or `unknown`                                                                         |
| `properties.method`          | HTTP method: GET/POST/PUT/PATCH/HEAD                                                                                   |
| `properties.path`            | Relative path of the request                                                                                           |
| `properties.origin`          | URI indicating where a fetch originates from or `unknown`                                                              |
| `properties.operationStatus` | `Success` for HTTP Status code < 400 <br> `ClientError` for HTTP Status code < 500 <br> `Error` for HTTP Status >= 500 |
| `properties.tenantId`        | Organization ID                                                                                                        |
| `properties.tenantName`      | Name of the organization                                                                                               |
| `properties.callerObjectId`  | Azure Active Directory ObjectId of the caller                                                                          |
| `properties.instanceId`      | Customer Insights `instanceId`                                                                                         |

### Workflow event schema

The Workflow allows one to setup [Data Sources](data-sources.md), [unify](data-unification.md) and [enrich](enrichment-hub.md) and finally [export](export-destinations.md) data into other systems. All those steps can be done individually (e.g. trigger a single export) or orchestrated (e.g. data refresh from data sources which trigger the unification process which will pull in additional enrichments and once done export the data into another system).
Following the available operations.

#### Operation Types

| OperationType     | Group                                   |
| ----------------- | --------------------------------------- |
| Ingestion         | [Data sources](data-sources.md)         |
| DataPreparation   | [Data sources](data-sources.md)         |
| Map               | [Data unification](data-unification.md) |
| Match             | [Data unification](data-unification.md) |
| Merge             | [Data unification](data-unification.md) |
| ProfileStore      |                                         |
| Search            |                                         |
| Activity          |                                         |
| AttributeMeasures | [Segments and Measures](segments.md)    |
| EntityMeasures    | [Segments and Measures](segments.md)    |
| Measures          | [Segments and Measures](segments.md)    |
| Segmentation      | [Segments and Measures](segments.md)    |
| Enrichment        |                                         |
| Intelligence      |                                         |
| AiBuilder         |                                         |
| Insights          |                                         |
| Export            |                                         |
| ModelManagement   |                                         |
| Relationship      |                                         |

#### Field Description

| Field           | DataType  | Required/Optional | Description                                                                                                                                                   | Example                                                                                                                                                                  |
| --------------- | --------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `time`          | Timestamp | Required          | Timestamp of the event (UTC)                                                                                                                                  | `2020-09-08T09:48:14.8050869Z`                                                                                                                                           |
| `resourceId`    | String    | Required          | ResourceId of the instance that emitted the event                                                                                                             | `/SUBSCRIPTIONS/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX/RESOURCEGROUPS/<RESOURCEGROUPNAME>/PROVIDERS/MICROSOFT.D365CUSTOMERINSIGHTS/INSTANCES/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXX` |
| `operationName` | String    | Required          | Name of the operation represented by this event. `{OperationType}.[WorkFlow|Task][Started|Completed]`. See [Operation Types](#operation-types) for reference. | `Segmentation.WorkflowStarted`,<br> `Segmentation.TaskStarted`, <br> `Segmentation.TaskCompleted`, <br> `Segmentation.WorkflowCompleted`                                 |
| `category`      | String    | Required          | Log category of the event. Always `Operational` for Workflow events                                                                                           | `Operational`                                                                                                                                                            | `2020-09-08T09:48:14.8050869Z` |
| `resultType`    | String    | Required          | Status of the event. `Running`, `Skipped`, `Successful`, `Failure`                                                                                            |                                                                                                                                                                          |
| `durationMs`    | Long      | Optional          | Duration of the operation in milliseconds                                                                                                                     | `133`                                                                                                                                                                    |
| `properties`    | String    | Optional          | JSON blob with additional properties to the particular category of events.                                                                                    | See sub section [Workflow Properties](#workflow-properties-schema)                                                                                                       |
| `level`         | String    | Required          | Severity level of the event                                                                                                                                   | Is one of `Informational`, `Warning` or `Error`                                                                                                                          |
|                 |

#### Workflow Properties schema

Workflow events have following properties.

| Field                                        | Workflow | Task | Description                                                                                                                                                                                                                                             |
| -------------------------------------------- | -------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `properties.eventType`                       | Yes      | Yes  | always `WorkflowEvent`, marking the event as Workflow event                                                                                                                                                                                             |
| `properties.workflowJobId`                   | Yes      | Yes  | Identifier of the workflow run. All Workflow and Tasks events within the workflow execution have the same `workflowJobId`                                                                                                                               |
| `properties.operationType`                   | Yes      | Yes  | Identifier of the operation, see [Operation Types](#operation-types)                                                                                                                                                                                    |
| `properties.tasksCount`                      | Yes      | No   | Workflow only. Number of tasks the Workflow triggers                                                                                                                                                                                                    |
| `properties.submittedBy`                     | Yes      | No   | Optional. Workflow events only. The Azure Active Directory [objectId of the user](https://docs.microsoft.com/azure/marketplace/find-tenant-object-id#find-user-object-id) who triggered the workflow, see also `properties.workflowSubmissionKind`      |
| `properties.workflowType`                    | Yes      | No   | `full` or `incremental` refresh                                                                                                                                                                                                                         |
| `properties.workflowSubmissionKind`          | Yes      | No   | `OnDemand` or `Scheduled`                                                                                                                                                                                                                               |
| `properties.workflowStatus`                  | Yes      | No   | `Running`, `Successful`                                                                                                                                                                                                                                 |
| `properties.startTimestamp`                  | Yes      | Yes  | UTC Timestamp `yyyy-MM-ddThh:mm:ss.SSSSSZ`                                                                                                                                                                                                              |
| `properties.endTimestamp`                    | Yes      | Yes  | UTC Timestamp `yyyy-MM-ddThh:mm:ss.SSSSSZ`                                                                                                                                                                                                              |
| `properties.submittedTimestamp`              | Yes      | Yes  | UTC Timestamp `yyyy-MM-ddThh:mm:ss.SSSSSZ`                                                                                                                                                                                                              |
| `properties.instanceId`                      | Yes      | Yes  | Customer Insights `instanceId`                                                                                                                                                                                                                          |  |
| `properties.identifier`                      | No       | Yes  | - For OperationType = `Export` the identifier is the guid of the export configuration. <br> - For OperationType = `Enrichment` it's the guid of the Enrichment <br> - For OperationType `Measures` and `Segmentation` the identifier is the Entity Name |
| `properties.friendlyName`                    | No       | Yes  | User friendly Name of the Export or the Entity which is processed.                                                                                                                                                                                      |
| `properties.error`                           | No       | Yes  | Optional. Error Message with more details.                                                                                                                                                                                                              |
| `properties.additionalInfo.Kind`             | No       | Yes  | Optional. For OperationType `Export` only. Identifies the kind of the export. See also the [overview of Export destinations](https://docs.microsoft.com/en-us/dynamics365/customer-insights/audience-insights/export-destinations).                     |
| `properties.additionalInfo.AffectedEntities` | No       | Yes  | Optional. For OperationType `Export` only. Identifies the kind of the export. Contains a ist of configured entities in the export.                                                                                                                      |
| `properties.additionalInfo.MessageCode`      | No       | Yes  | Optional. For OperationType `Export` only. Detailed Message for the export.                                                                                                                                                                             |
| `properties.additionalInfo.entityCount`      | No       | Yes  | Optional. For OperationType `Segmentation` only. Indicating the total numbers of members the segment has.                                                                                                |
