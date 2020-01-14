---
uid: developers/downloads/js
title: Web/React (JavaScript)
author: ruthaisabokhae
description: Web/React (JavaScript)
ms.author: ruthai
ms.date: 12/27/2019
ms.service: product-insights
ms.topic: conceptual
---

# Getting started with the Product Insights SDK for JavaScript

[!INCLUDE [cc-beta-prerelease-disclaimer]( includes/cc-beta-prerelease-disclaimer.md)]

This tutorial will guide you through the process of using a Product Insights ingestion key and the Product Insights SDK for your existing JavaScript project. You'll start seeing signals in your portal in five minutes or sooner.

For this example, picture the following scenario: you work at a car manufacturing company, and the company has just released a new car. You want to know how the car is performing, your users' demographics, and their driving habits. Product Insight allows you to achieve these goals by sending real time signals and generating valuable insights in just a few simple steps.

## Prerequisites

* The SDK requires  the project or webpage to be hosted in order to send telemetry. Telemetry sent from a local file will not be accepted by the server.
* Ingestion key (see below for instructions on how to obtain)

## Get an ingestion key from Product Insights portal

1. From the [pi.dynamics.com](http://pi.dynamics.com) home screen, select your team from the left panel. If you do not already have a team, refer to [Create a team](xref:developers/quick-starts/create-a-team).
2. Add a new project to your team by selecting the **+ New Project** button from the top right corner.
3. Type in a project name in the **Name** field and any other text for **Description**. Select **Create** to commit the update.
4. Once your project is created, select the project.
5. Select **Settings** under your project. Your ingestion key is available under **Ingestion Key**.

> [!NOTE]
> Leave this tab open in your web browser, or copy the key to a clipboard because you will need to use it later.

## Integrate the Product Insights SDK into your webpage or project

1. Add the Product Insights SDK to your page:
    1. [Download](https://download.pi.dynamics.com/sdk/ProductInsightsSenders/pi_js_sdk.zip) the **Product Insights JavaScript SDK**.
    2. Add the SDK file to your project directory, and add it to your page using a script tag:

    ```javascript
       <script type="text/javascript" src="pi_js_sdk-1.0.0.min.js">
       </script>
    ```

2. Add the 1DS SDK to your page using a script tag, as shown:

    ```javascript
       <script type="text/javascript"
       src="https://az416426.vo.msecnd.net/scripts/c/ms.analytics-2.min.js">
       </script>
    ```

3. Start the SDKs (only required once):

    ```javascript
    var analytics = new oneDS.ApplicationInsights();
    var config = {
        instrumentationKey: "Your_Ingestion_Key"
    };

    analytics.initialize(config, []);
    var pia = new PI.ProductInsightsAnalytics(analytics, "Your_Ingestion_Key");
    ```

4. Track signals:

    ```javascript
    // Do a simple track signals call.
    pia.trackSignal({ name: "user_information"});

    // Track a signal with custom properties of various types.
    pia.trackSignal({
      name: "car_information",
      properties: {
        "engine_start": true,
        "car_model": "Star Car",
        "model_year": "2017",
        "rpm": 3000,
        "temperature": 74.3
      }
    });
    ```

    The following types are supported for event properties:
    * **String**
    * **Double**
    * **Boolean**

5. Teardown the SDK when application closes to ensure all signals currently in queue are sent:

    ```javascript
    analytics.getPostChannel().teardown();
    ```
