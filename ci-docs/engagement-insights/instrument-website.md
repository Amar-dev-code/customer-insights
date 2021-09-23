---
title: Add code to your website
description: How to add a code snippet to capture events on your website.
author: britl
ms.reviewer: mhart
ms.author: britl
ms.date: 04/30/2021
ms.service: customer-insights
ms.subservice: engagement-insights
ms.topic: how-to
ms.manager: shellyha
---

# Install the web sdk on a website

[!INCLUDE [cc-beta-prerelease-disclaimer](includes/cc-beta-prerelease-disclaimer.md)]

This article describes how an administrator installs the web sdk on a website. You'll start seeing events in your workspace shortly after instrumenting your website. For more information, see [Manage workspaces and environment](manage-environments-workspaces.md). To capture events in mobile apps, see [Developer resources overview](developer-resources.md).


### Prerequisites

* You must have administrator permissions for the workspace to store the data.
* Your website or project must be hosted online to send activity data. Data sent from a local file will not be accepted by the server.


## Add web sdk to your website

Go to **Admin** > **Workspace**  and then select **Installation guide**. There are two options to install web sdk. The first is to use a download link, and the second is to install an NPM package

### Option 1: Using the download link
1. Select **Copy code** to copy the code snippet. By default, the ingestion key for your workspace is embedded in the code snippet.
:::image type="content" source="media/copy-code.png" alt-text="Screenshot of the code snippet page.":::
2. Add the copied code snippet to your website, near the <head> tag and before any other script or CSS tags.
3. Publish your updated website and wait a few minutes to capture the incoming web traffic.
4. To see your data, select your workspace from the workspace switcher in the navigation pane. Then, select one of the reports in the **Discover** section.

### Option 2: Using the NPM package (recommended for JavaScript-based web Apps)
1. Go to our [NPM webpage](https://www.npmjs.com/package/engagementinsights-web) and follow the instructions to install and set up our web sdk NPM pacakge
2. Publish your updated website and wait a few minutes to capture the incoming web traffic.
3. To see your data, select your workspace from the workspace switcher in the navigation pane. Then, select one of the reports in the **Discover** section.

## Configuration options

You can change the following configuration options in the code snippet:

- **ingestionKey**: The ingestion key used to send events to your workspace. You can change the ingestion key to send events to a different workspace. An ingestion key is unique to each workspace.
- **autoCapture**: Specifies if page views and interactions with the website are captured. It has two options:
    - **view**: Set to *true* to capture page views. Page views are captured as *View* [events](glossary.md#event), a type of [base event](glossary.md#base-event).
    - **click**: Set to *true* to capture visitor interactions on the website. Interactions are captured as *Action* [events](glossary.md#event), a type of [base event](glossary.md#base-event).

[!INCLUDE[footer-include](../includes/footer-banner.md)]