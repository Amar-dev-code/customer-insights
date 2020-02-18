---
uid: developers/tutorials/csv-drag-drop
title: CSV drag and drop
author: ruthaisabokhae
description: CSV drag and drop
ms.author: ruthai
ms.date: 12/31/2019
ms.service: product-insights
ms.topic: conceptual
---
# CSV drag and drop

[!INCLUDE [cc-beta-prerelease-disclaimer]( includes/cc-beta-prerelease-disclaimer.md)]
Use the drag and drop tool to ingest signals into Product Insights from CSV files that are less than 10 MB.

## Get an ingestion key from Product Insights portal

Your ingestion key is located on your Product Insights project's **Settings** page. [Find and copy your key.](api-token.md)

## Upload a CSV file

### Option 1

1. Select your team and project.
2. Go to the **Settings** page.
3. Scroll down to **CSV Files**.
4. Select **+ Upload** or **+ Add** if CSV files already exist.
5. Select the CSV file you want to upload from your local storage.
6. In the **Timestamp column** field, enter the header name of your CSV file's timestamp column.
7. Select **Create**.
    ![CSV drag drop settings screenshot](media/csv-uploader-screenshot-annotated.png)

### Option 2

1. Select your team and project.
2. Go to the default **Signals** page.
3. Select **+ Add signals**.
4. Check **Import a CSV**.
5. Select **Next** Button.
6. The same form as in Option 1 above will appear. Refer to Option 1 to fill out the form.
    ![CSV drag drop signals screenshot](media/add-signals-wizard-screenshot-annotated.png)
