---
title: "Connect to an Azure Data Lake Storage account by using a service principal"
description: "Use an Azure service principal to connect to your own data lake."
ms.date: 12/06/2021
ms.subservice: audience-insights
ms.topic: how-to
author: adkuppa
ms.author: adkuppa
ms.reviewer: mhart
manager: shellyha
searchScope: 
  - ci-system-security
  - customerInsights
---

# Connect to an Azure Data Lake Storage account by using an Azure service principal

This article discusses how to connect Dynamics 365 Customer Insights with an Azure Data Lake Storage account by using an Azure service principal instead of storage account keys. 

Automated tools that use Azure services should always have restricted permissions. Instead of having applications sign in as a fully privileged user, Azure offers service principals. You can use service principals to securely [add or edit a Common Data Model folder as a data source](connect-common-data-model.md) or [create or update an environment](create-environment.md).

> [!IMPORTANT]
> - The Data Lake Storage account that will use the service principal must be Gen2 and have [hierarchical namespace enabled](/azure/storage/blobs/data-lake-storage-namespace). Azure Data Lake Gen1 storage accounts are not supported.
> - You need admin permissions for your Azure subscription to create a service principal.

## Create an Azure service principal for Customer Insights

Before creating a new service principal for Customer Insights, check whether it already exists in your organization.

### Look for an existing service principal

1. Go to the [Azure admin portal](https://portal.azure.com) and sign in to your organization.

2. From **Azure services**, select **Azure Active Directory**.

3. Under **Manage**, select **Enterprise Applications**.

4. Search for the Microsoft application ID `0bfc4568-a4ba-4c58-bd3e-5d3e76bd7fff` with the name `Dynamics 365 AI for Customer Insights`.

5. If you find a matching record, it means that the service principal already exists. 
   
   :::image type="content" source="media/ADLS-SP-AlreadyProvisioned.png" alt-text="Screenshot showing an existing service principal.":::
   
6. If no results are returned, create a new service principal.

>[!NOTE]
>To make use of the full power of Dynamics 365 Customer Insights, we suggest that you add both apps to the service principal.

### Create a new service principal

1. Install the latest version of Azure Active Directory PowerShell for Graph. For more information, go to [Install Azure Active Directory PowerShell for Graph](/powershell/azure/active-directory/install-adv2).

   1. On your PC, select the Windows key on your keyboard and search for **Windows PowerShell** and select **Run as administrator**.
   
   1. In the PowerShell window that opens, enter `Install-Module AzureAD`.

2. Create the service principal for Customer Insights with the Azure AD PowerShell module.

   1. In the PowerShell window, enter `Connect-AzureAD -TenantId "[your tenant ID]" -AzureEnvironmentName Azure`. Replace *[your tenant ID]* with the actual ID of your tenant where you want to create the service principal. The environment name parameter, `AzureEnvironmentName`, is optional.
  
   1. Enter `New-AzureADServicePrincipal -AppId "0bfc4568-a4ba-4c58-bd3e-5d3e76bd7fff" -DisplayName "Dynamics 365 AI for Customer Insights"`. This command creates the service principal for Customer Insights on the selected tenant. 

## Grant permissions to the service principal to access the storage account

Go to the Azure portal to grant permissions to the service principal for the storage account you want to use in Customer Insights.

1. Go to the [Azure admin portal](https://portal.azure.com) and sign in to your organization.

1. Open the storage account you want the service principal for Customer Insights to have access to.

1. On the left pane, select **Access control (IAM)**, and then select **Add** > **Add role assignment**.

   :::image type="content" source="media/ADLS-SP-AddRoleAssignment.png" alt-text="Screenshot showing the Azure portal while adding a role assignment.":::

1. On the **Add role assignment** pane, set the following properties:
   - Role: **Storage Blob Data Contributor**
   - Assign access to: **User, group, or service principal**
   - Select: **Dynamics 365 AI for Customer Insights** (the [service principal](#create-a-new-service-principal) you created earlier in this procedure)

1.	Select **Save**.

It can take up to 15 minutes to propagate the changes.

## Enter the Azure resource ID or the Azure subscription details in the storage account attachment to Customer Insights

You can attach a Data Lake Storage account in Customer Insights to [store output data](manage-environments.md) or [use it as a data source](/dynamics365/customer-insights/audience-insights/connect-dataverse-managed-lake). This option lets you choose between a resource-based or a subscription-based approach. Depending on the approach you choose, follow the procedure in one of the following sections.

### Resource-based storage account connection

1. Go to the [Azure admin portal](https://portal.azure.com), sign in to your subscription, and open the storage account.

1. On the left pane, go to **Settings** > **Properties**.

1. Copy the storage account resource ID value.

   :::image type="content" source="media/ADLS-SP-ResourceId.png" alt-text="Copy the storage account resource ID.":::

1. In Customer Insights, insert the resource ID in the resource field displayed on the storage account connection screen.

   :::image type="content" source="media/ADLS-SP-ResourceIdConnection.png" alt-text="Enter the storage account resource ID information.":::   

1. Continue with the remaining steps in Customer Insights to attach the storage account.

### Subscription-based storage account connection

1. Go to the [Azure admin portal](https://portal.azure.com), sign in to your subscription, and open the storage account.

1. On the left pane, go to **Settings** > **Properties**.

1. Review the **Subscription**, **Resource group**, and the **Name** of the storage account to make sure you select the right values in Customer Insights.

1. In Customer Insights, choose the values for the corresponding fields when attaching the storage account.

1. Continue with the remaining steps in Customer Insights to attach the storage account.


[!INCLUDE [footer-include](includes/footer-banner.md)]