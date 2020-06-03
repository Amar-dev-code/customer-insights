---
uid: topics/websdk-sample
title: Run Web SDK Sample
author: ruthaisabokhae
description: How to run the Web SDK Sample
ms.author: ruthai
ms.date: 06/03/2020
ms.service: product-insights
ms.topic: conceptual
---

# Run Product Insights Web SDK Sample

[!INCLUDE [cc-beta-prerelease-disclaimer]( includes/cc-beta-prerelease-disclaimer.md)]

## Prerequisites

- Visual Studio Code
- Ingestion key (see [here](js.md) for instructions on how to obtain)

## Run Sample

1. [Download](https://download.pi.dynamics.com/sdk/ProductInsightsSamples/pi_js_sample.zip) the **Product Insights Web/React (JavaScript) SDK sample**.
2. [Install](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) the Live Server extension in Visual Studio Code.
3. Unzip the compressed file `pi_js_sample.zip`.
4. Open the folder in Visual Studio Code.
5. Replace *Your_Ingestion_Key* with your ingestion key from the Product Insights portal.
6. Right click on the HTML file and select **Open with Live Server**.
...............................................................




•	Open the unzipped folder in Visual Studio Code.
o	Install Live Server extension for Visual Studio Code.
•	In the pi_js_sample.html file, replace the string “INGESTION_KEY” with the your ingestion key and the string “NAME” with the global name that you want the SDK to be instantiated in (replace all occurrences).
•	Open the pi_js_sample.html file using Live Server. 
