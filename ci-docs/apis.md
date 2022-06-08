---
title: Work with APIs
description: Use APIs and understand limitations.
ms.date: 05/10/2021
ms.reviewer: wimohabb

ms.subservice: audience-insights
ms.topic: conceptual
author: m-hartmann
ms.author: wimohabb
manager: shellyha
searchScope: 
  - ci-system-api-usage
  - customerInsights
---

# Work with Customer Insights APIs

Dynamics 365 Customer Insights provides APIs to build your own applications based on your data in Customer Insights.

> [!IMPORTANT]
> Details of these APIs are listed on the [Customer Insights APIs reference](https://developer.ci.ai.dynamics.com/api-details#api=CustomerInsights). They include additional information about operations, parameters, and responses.

This article describes how to access the Customer Insights APIs, create an Azure App Registration, and get started with client libraries.

## Get started trying the Customer Insights APIs

1. [Sign in](https://home.ci.ai.dynamics.com) to Customer Insights. If you don't have a subscription yet, [sign up for a trial of Customer Insights](https://aka.ms/tryci).

1. To enable APIs on your Customer Insights environment, go to **Admin** > **Security**. You'll need admin permissions to do so.

1. Go to the **APIs** tab and select the **Enable** button.    
 
   Enabling the APIs creates a primary and secondary subscription key for your instance that gets used in the API requests. You can regenerate the keys by selecting the **Regenerate primary** or **Regenerate secondary** on **Admin** > **Security** > **APIs**.

<!--  :::image type="content" source="media/enable-apis.gif" alt-text="Enable Customer Insights APIs."::: -->

1. Select **Explore our APIs** to [try out the APIs](https://developer.ci.ai.dynamics.com/api-details#api=CustomerInsights&operation=Get-all-instances).

1. Choose an API operation and select **Try it**.

1. In the side pane, set the value in the **Authorization** dropdown menu to **implicit**. The `Authorization` header gets added with a bearer token. Your subscription key will be automatically populated.
  
1. Optionally, add all necessary query parameters.

1. Scroll to the bottom of the side pane and select **Send**.

The HTTP response will soon appear below.

<!--   :::image type="content" source="media/try-apis.gif" alt-text="How to test the APIs."::: -->

## Create a new app registration in the Azure portal

These steps help you get started with using the Customer Insights APIs in an Azure application using delegated permissions. Make sure to complete the [Getting started section](#get-started-trying-the-customer-insights-apis) first.

1. Sign in to the [Azure portal](https://portal.azure.com) with the account that can access the Customer Insights data.

1. On the left, select **App registrations**.

1. Select **New registration**, provide an application name and choose the account type.

   Optionally, add a redirect URL. http://localhost is sufficient for developing an application on your local computer.

1. On your new App registration, go to **API permissions**.

1. Select **Add a permission** and select **Dynamics 365 AI for Customer Insights** in the side pane.

1. For **Permission type**, select **Delegated permissions** and then select the **user_impersonation** permission.

1. Select **Add permissions**. If you need to access the API without a user signing in, review the [Server-to-server application permissions](#server-to-server-application-permissions) section.

1. Select **Grant admin consent for...** to complete the app registration.

You can use the Application/Client ID for this app registration with the Microsoft Authentication Library (MSAL) to obtain a bearer token to send with your request to the API.

<!-- :::image type="content" source="media/grant-admin-consent.gif" alt-text="How to grant admin consent."::: -->

For more information about MSAL, see [Overview of Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-overview).

For more information about app registration in Azure, see [Register an application](/graph/auth-register-app-v2).

For information on using the APIs in our client libraries, see [Customer Insights client libraries](#customer-insights-client-libraries).

### Server-to-server application permissions

The [app registration section](#create-a-new-app-registration-in-the-azure-portal) outlines how to register an app that requires a user to sign in for authentication. Learn how to create an app registration that doesn't need user interaction and can be run on a server.

1. On your App registration in the Azure portal, go to **API permissions**.

1. Select **Add a permission**. 

1. Select the **APIs my organization uses** tab and choose **Dynamics 365 AI for Customer Insights** from the list. 

1. For **Permission type**, select **Application permissions** and then select the **CustomerInsights.Api.All** permission.

1. Select **Add permissions**.

1. Go back to **API permissions** for your app registration.

1. Select **Grant admin consent for...** to complete the app registration.

 <!--  :::image type="content" source="media/grant-admin-consent.gif" alt-text="How to grant admin consent."::: -->

1. To conclude, we have to add the name of the app registration as a user in Customer Insights.  
   
   Open Customer Insights, go to **Admin** > **Security** and select **Add user**.

1. Search for the name of your app registration, select it from the search results, and select **Save**.

## Sample queries

We've compiled a short list of OData sample queries to work with the APIs: [OData query examples](odata-examples.md).

## Customer Insights client libraries

This section helps you get started using the client libraries available for the Customer Insights APIs. All library source code and sample applications can be found on the [Customer Insights GitHub page](https://github.com/microsoft/Dynamics365-CustomerInsights-Client-Libraries). 

### C# NuGet

Learn how to get started using the C# client libraries from NuGet.org. For more information on the NuGet package, see [Microsoft.Dynamics.CustomerInsights.Api](https://www.nuget.org/packages/Microsoft.Dynamics.CustomerInsights.Api/). Currently, this package targets the netstandard2.0 and netcoreapp2.0 frameworks.

#### Add the C# client library to a C# project

1. In Visual Studio, open the **NuGet Package Manager** for your project.

1. Search for **Microsoft.Dynamics.CustomerInsights.Api**.

1. Select **Install** to add the package to the project.
 
   Alternatively, run this command in the **NuGet Package Manager Console**: `Install-Package -Id Microsoft.Dynamics.CustomerInsights.Api -Source nuget.org -ProjectName <project name> [-Version <version>]`

 <!--  :::image type="content" source="media/visual-studio-nuget-package.gif" alt-text="Add NuGet package to Visual Studio project."::: -->

#### Use the C# client library

1. Use the [Microsoft Authentication Library (MSAL)](/azure/active-directory/develop/msal-overview) to get an `AccessToken` using your existing [Azure app registration](#create-a-new-app-registration-in-the-azure-portal).

1. After successfully authenticating and acquiring a token, construct a new or use an existing `HttpClient` with the **DefaultRequestHeaders "Authorization"** set to **Bearer "access token"** and **Ocp-Apim-Subscription-Key** set to the [**subscription key** from your Customer Insights environment](#get-started-trying-the-customer-insights-apis).   
 
   Reset the **Authorization** header when appropriate. For example, when the token expired.

1. Pass this `HttpClient` into the construction of the `CustomerInsights` client.

<!--   :::image type="content" source="media/httpclient-sample.png" alt-text="Sample of httpclient."::: -->

1. Make calls with the client to the "extension methods"—for example, `GetAllInstancesAsync`. If access to the underlying `Microsoft.Rest.HttpOperationResponse` is preferred, use the "http message methods"—for example, `GetAllInstancesWithHttpMessagesAsync`.

1. The response will likely be of type `object` because the method can return multiple types (for example, `IList<InstanceInfo>` and `ApiErrorResult`). To check the return type, you use the objects in the response types specified on the [API details page](https://developer.ci.ai.dynamics.com/api-details#api=CustomerInsights) for that operation.    
   
   If more information on the request is needed, use the **http message methods** to access the raw response object.

### NodeJS package

Use the NodeJS client libraries available through NPM: https://www.npmjs.com/package/@microsoft/customerinsights

### Python package

Use the Python client libraries available through PyPi: https://pypi.org/project/customerinsights/

[!INCLUDE [footer-include](includes/footer-banner.md)]
