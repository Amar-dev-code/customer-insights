---
title: "Activate consent rules for segments"
description: "Follow these steps to link consent data and activate consent checks in Dynamics 365 Customer Insights. An admin can also disable consent checks."
ms.date: 11/12/2021
ms.subservice: audience-insights
ms.topic: how-to
author: smithy7
ms.author: smithc
ms.reviewer: mhart
manager: shellyha
---

# Activate consent rules

The [Consent Center (preview)](consent-management/overview.md) helps you to harmonize consent data from various sources. Use the unified *Consent* entity to apply default consent checks. After importing consent data into the Consent Center and configuring the rules for the data, the *Consent* entity is automatically synced to Dynamics 365 Customer Insights.

## Enable consent checks

With consent data imported to the Consent Center (preview) and the rules set up, you can enable consent checks. 

:::image type="content" source="consent-management/media/enable-consent-checks.png" alt-text="Consent tab in Customer Insights settings with activated consent data.":::

1. In Customer Insights, go to **Admin** > **System**.

1. Select the **Consent (preview)** tab.

1. In the **Enable consent checks** section, set the toggle to **On** for all the areas you want to enable.

1. Select the **Allow override of default consent rules** checkbox to remove the default consent checks enforced on a particular segment. 

1. In the dropdown menu, select where you want to allow overrides.     

1. In the **Link consent to customer profiles** section, choose the attribute that's used as an identifier to link consent data to customer data. It will likely be a phone number or email address. 

1. Select **Save** to apply your settings.

## Disable consent checks

To stop using consent data in Customer Insights, an admin has to update the system settings accordingly.

1. In Customer Insights, go to **Admin** > **System**.

1. Select the **Consent (preview)** tab.

1. In the **Enable consent checks** section, set the toggle to **Off**.

> [!TIP]
> To stop using the consent management capability, see [System settings in Consent Center (preview)](consent-management/system-settings.md).
