---
uid: topics/manage-cookies-user-consent
title: Manage cookies and user consent
author: ruthaisabokhae
description: Cookies and user consent
ms.author: ruthai
ms.date: 06/08/2020
ms.service: product-insights
ms.topic: conceptual
---

# Manage cookies and user consent

Dynamics 365 Product Insights uses cookies and local storage (`localStorage`) to identify website visitors.

Cookies are small files that store bits of information about a user’s interactions with the website. They are stored in the browser. When you visit a website for which you have stored cookies, the browser sends that information to the server, which returns information that is unique to you. This is the technology that allows, for example, an online shopping cart to keep selected items in it even if a customer navigates away from the website.

## User consent

Cookies are considered “personal data” under the [General Data Protection Regulation (GDPR)](https://docs.microsoft.com/en-us/dynamics365/get-started/gdpr/), a European Union (EU) regulation that mandates how organizations should handle their users’ privacy and security. If your business employs and/or sells to EU citizens, the GDPR affects you. [Learn more about how Microsoft can help you reach GDPR compliance](https://www.microsoft.com/en-ww/trust-center/privacy/gdpr-faqs).

To allow the Product Insights SDK to store cookies or other sensitive information, you must specify whether your users have consented. This occurs on initialization of the SDK.

If you indicate that there is no user consent, the SDK will not store any data, and will not send signals that can be used to track user behavior. Any previously stored data will be deleted from the browser.

If no user consent value is specified, the SDK will assume that the user has consented.

## Visitor data storage in Product Insights

### Cookies

-	_mspi
    -	Stores the anonymous user ID. This cookie is set in the customer domain and expires in 365 days.

### Local storage

Product Insights also makes use of local storage (`localStorage`) to track non-sensitive data. This data is fully stored in the browser itself, with no traffic sent to or from your servers.

-	*PISession.Id* 
    - Stores information about the ongoing user session, such as session ID, when it started, and when it expires.
- *PISession.Previous*
    - Stores the URL of the previously visited page in the current session.
    
Keys in local storage don't expire automatically. They'll be reset during the next session by the SDK.

## Deleting cookies

Your customers can manually delete cookies and local storage keys at any time through their browser's settings.
