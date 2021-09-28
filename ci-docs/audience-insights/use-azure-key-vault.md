---
title: "Bring your own Azure Key Vault to manage secrets"
description: "Learn how to configure Customer Insights to use your own Azure Key Vault."
ms.date: 09/28/2021
ms.reviewer: mhart
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: how-to
author: brndkfr
ms.author: bkief
manager: shellyha
---

# Bring your own Azure Key Vault (Preview)

Linking a dedicated [Azure Key Vault](azure/key-vault/general/basic-concepts) to an audience insights environment helps organizations to meet compliance requirements.
The dedicated Key Vault can be used to stage and use secrets in an organization's compliance boundary. Audience insights can use the secrets in Key Vault to [set up connections](connections.md) to third-party systems.

## Link the Key Vault to the audience insights environment

### Prerequisites

To configure the Key Vault in audience insights, the following prerequisites must be met:

* You have an active Azure subscription.

* You have an [Administrator](permissions.md#adminstrator) role in audience insights. Learn more about [user permissions in audience insights](permissions.md#assign-roles-and-permissions).

* You have the [Contributor](azure/role-based-access-control/built-in-roles#contributor) and [User Access Administrator](azure/role-based-access-control/built-in-roles#user-access-administrator) role on the Key Vault or the Resource Group the Key Vault is belonging to. For more information, see [Add or remove Azure role assignments using the Azure portal](azure/role-based-access-control/role-assignments-portal). If you don't have the **User Access Administrator** role on the Key Vault, the role-based access control permissions for the Azure service principal for Customer Insights must be set up separately. Follow the steps to [use an Azure service principal](connect-service-principal.md) for the Key Vault that should be linked.

* The Key Vault must have Key Vault firewall **disabled**.

* The Key Vault is in the same [Azure location](https://azure.microsoft.com/global-infrastructure/geographies/#overview) as the audience insights environment. The region of the environment in audience insights is listed under **Admin** > **System** > **About** > **Region**.

### Link a Key Vault to the Environment

1. Go to **Admin** > **System** and select the **Security** tab.
1. Select **Setup** on the Key Vault tile. <!-- set up?-->
1. Choose a **Subscription**.
1. Choose a **Key Vault** from the drop-down list. If too many Key Vaults are showing up, select a resource group to limit the search results.
1. Accept the **Data privacy and compliance** statement.
1. Select **Save**.

**TODO** - ADD SCREENSHOTS

The Key Vault tile now shows the linked Key Vault name, resource group, and subscription. It's ready to be used in the connection setup.
For details which permissions on the Key Vault are granted to audience insights see [Permissions granted on the Key Vault to audience insights](#permissions-granted-on-the-key-vault-to-audience-insights).

## Use the Key Vault in the Connection setup

When [setting up connections](dynamics365/customer-insights/audience-insights/connections) to third-party systems, the secrets from the linked Key Vault can be used to configure the connections.

1. Go to **Admin** > **Connections**.
1. Select **Add connection**.
1. For the supported connection types, a **Use Key Vault** toggle is available if you linked a Key Vault.
1. Instead of entering the secret manually, you can choose the secret name that points to the secret value in the Key Vault.

**TODO** - ADD SCREENSHOTS

## Supported Connection Types

The following [export](export-destinations.md) connections are supported.

* [ActiveCampaign](export-active-campaign.md)
* [Autopilot](export-autopilot.md)
* [DotDigital](export-dotdigital.md)
* [Google Ads](export-google-ads.md)
* [Klaviyo](export-klaviyo.md)
* [LiveRamp](export-liveramp.md)
* [Marketo](export-marketo)
* [Omnisend](export-omnisend.md)
* [Salesforce Marketing Cloud](export-salesforce.md)
* [Sendgrid](export-sendgrid.md)
* [Sendinblue](export-sendinblue.md)
* [SFTP](export-sftp.md)

Export connections that require you to sign in on the target system, the connection secrets are kept in the service. <!-- in the service = in AUI DB? -->

## Permissions granted on the Key Vault to audience insights

The following permissions are granted to audience insights on a linked Key Vault if [Key Vault access policy](azure/key-vault/general/assign-access-policy?tabs=azure-portal) or [Azure role-based access control](azure/key-vault/general/rbac-guide?tabs=azure-cli) is enabled.

### Key Vault access policy

| Type        | Permissions                                                                                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Key         | [Get Keys](rest/api/keyvault/get-keys), [Get Key](rest/api/keyvault/get-key)                                 |
| Secret      | [Get Secrets](rest/api/keyvault/get-secrets), [Get Secret](rest/api/keyvault/get-secret)                     |
| Certificate | [Get Certificates](rest/api/keyvault/get-certificates), [Get Certificate](rest/api/keyvault/get-certificate) |

The above values are the minimum to list and read during execution.

### Azure role-based access control

The **Key Vault Reader** and **Key Vault Secrets User** roles will be added for audience insights. For details on the roles see [Azure built-in roles for Key Vault data plane operations](azure/key-vault/general/rbac-guide?tabs=azure-cli).

## Recommendations

* Use a separate or dedicated Key Vault, which contains only the secrets required for audience insights. Read more about why [separate Key Vaults are recommended](azure/key-vault/general/best-practices#why-we-recommend-separate-key-vaults).

* Follow the [Best practices to use Key Vault](azure/key-vault/general/best-practices#turn-on-logging) for control access, backup, audit, and recovery options.

## Frequently asked questions

### Can audience insights write secrets or overwrite secrets into the Key Vault?

No. Only read and list permissions outlined in the [granted Permissions](#permissions-granted-on-the-key-vault-to-audience-insights) section are granted to audience insights. The system can't add, delete, or overwrite secrets in the Key Vault. That's also the reason why you can't enter when a connection uses Key Vault.

### Can I change a connection from using Key Vault secrets to default authentication?

No. You can't change back to a default connection after configuring it with a secret from a linked Key Vault. Create a separate connection and delete the old one if necessary.

### How can I revoke access to a Key Vault for audience insights?

Depending on whether [Vault access policy](azure/key-vault/general/assign-access-policy?tabs=azure-portal) or [Azure role-based access control](azure/key-vault/general/rbac-guide?tabs=azure-cli) are enabled, you need to remove the permissions for the Service Principal `0bfc4568-a4ba-4c58-bd3e-5d3e76bd7fff` with the name `Dynamics 365 AI for Customer Insights`. All connections using the Key Vault will stop working.

### A secret that is used in a connection got removed from the Key Vault, what can I do?

A notification shows in audience insights when a configured secret from the Key Vault isn't accessible anymore. Enable [soft-delete](azure/key-vault/general/soft-delete-overview) on the Key Vault to restore secrets if they're accidentally removed.

### A connection doesn't work but my secret is in the Key Vault, what might be the cause?

A notification shows in audience insights when it can't access the Key Vault.

* The permissions for the audience insights Service Principal got removed. They need to be manually restored.

* The firewall on the Key Vault is enabled. The firewall must be disabled to make the Key Vault accessible for audience insights again.
