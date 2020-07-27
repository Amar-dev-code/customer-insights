---
uid: topics/websdk-sample
title: Run Web SDK Sample
author: ruthaisabokhae
description: How to run the Web SDK Sample
ms.author: ruthai
ms.date: 07/27/2020
ms.service: product-insights
ms.topic: conceptual
---

# Run the Product Insights Web SDK sample

[!INCLUDE [cc-beta-prerelease-disclaimer]( includes/cc-beta-prerelease-disclaimer.md)]

## Prerequisites

- Visual Studio Code
- Ingestion key (see [Getting started with the Product Insights Web SDK](getting-started-websdk.md) for instructions on how to obtain this)

## Run Sample

1. [Download](https://download.pi.dynamics.com/sdk/ProductInsightsSamples/pi_websdk_sample.zip) the Product Insights Web SDK sample.
2. [Install](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) the Live Server extension in Visual Studio Code.
3. Unzip the compressed file `pi_websdk_sample.zip`.
4. Open the unzipped folder in Visual Studio Code.
5. In the `pi_websdk_sample.html` file, replace the string “INGESTION_KEY” with your ingestion key from the Product Insights portal, and the string “NAME” with the global name that you want the SDK to be instantiated in. Be sure to replace all occurrences.
6. Open the `pi_websdk_sample.html` file using Live Server in Visual Studio Code.
