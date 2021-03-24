---
title: Manage cookies and user consent to store user data
description: Understand how cookies and user consent are used to identify website visitors.
author: pickwick129
ms.reviewer: ruthai
ms.author: v-salash
ms.date: 10/30/2020
ms.service: customer-insights
ms.subservice: engagement-insights 
ms.topic: conceptual
ms.manager: shellyha
---

# Manage cookies and user consent

[!INCLUDE [cc-beta-prerelease-disclaimer](includes/cc-beta-prerelease-disclaimer.md)]

Dynamics 365 Customer Insights engagement insights capability uses cookies and local storage (`localStorage`) to identify website visitors.

Cookies are small files that store bits of information about a user’s interactions with the website. They are stored in web browsers. When users visit a website for which your users have stored cookies, the browser sends that information to the server, which returns information that is unique to the user. This is the technology that allows, for example, an online shopping cart to keep selected items in it even if a user navigates away from the website.

## User consent

The [General Data Protection Regulation (GDPR)](/dynamics365/get-started/gdpr/) is a European Union (EU) regulation that mandates how organizations should handle their users’ privacy and security. Cookies often store or collect “personal data,” such as an online identifier, which is covered by the GDPR. If your business employs and/or sells to EU data subjects, the GDPR affects you. [Learn more about how Microsoft can help you comply with the GDPR](https://www.microsoft.com/trust-center/privacy/gdpr-faqs).

To allow the engagement insights SDK to store cookies or other sensitive information, you must specify whether your users have consented. This occurs on initialization of the SDK.

If you indicate that there is no user consent, the SDK will not store any data, and will not send events that can be used to track user behavior. Any previously stored data will be deleted from the browser.

If no user consent value is specified, the SDK will assume that the user has consented. This means that if you (as our customer) don't specify a value for user consent in the SDK, data will be collected. However, if you specify that the value for user consent needs to be “true,” data won't be collected if a user declines or fails to provide explicit consent.

## Visitor data storage in engagement insights capability

### Cookies

- _msei
    - Stores the anonymous user ID. This cookie is set in the customer domain and expires in 365 days.

### Local storage

Engagement insights capability also makes use of local storage (`localStorage`) to track non-sensitive data. This data is fully stored in the browser itself, with no traffic sent to or from your servers.

- *EISession.Id* 
    - Stores information about the ongoing user session, such as session ID, when it started, and when it expires.
- *EISession.Previous*
    - Stores the URL of the previously visited page in the current session.
    
Keys in local storage don't expire automatically. They'll be reset during the next session by the SDK.

## Deleting cookies

Your customers can manually delete cookies and local storage keys at any time through their browsers' settings.


[!INCLUDE[footer-include](../includes/footer-banner.md)]