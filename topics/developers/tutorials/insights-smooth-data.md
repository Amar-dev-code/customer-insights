---
uid: developers/tutorials/insights-smooth-data
title: Smooth data
author: vroha
description: Smooth data
ms.author: v-roha
ms.date: 05/22/2019
ms.service: product-insights
ms.topic: conceptual
---
# Smooth data

Some signals are noisy. To reduce fluctuations and noise, you can use the methods built into Product Insights, such as rolling averages, exponential rolling averages, and rolling medians, to smooth out variability and outliers. These methods work by giving more weight to the latest data and reacting faster to recent changes. They also make trends much easier to spot. 

Choose an automatic time grain to let the system find the optimal window size.

## Example

1. Select the data set to smooth.
2. Select a method from the **Smooth** menu such as **Rolling average**.
3. Product Insights will smooth the data on your chart according to the method you have selected.

> [!VIDEO https://ariamediahost.blob.core.windows.net/media/videos/ProductInsights/insights-smoothing.mp4]
