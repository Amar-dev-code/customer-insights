---
title: "Custom machine learning models | Microsoft Docs"
description: "Work with custom models from Azure Machine Learning in Dynamics 365 Customer Insights."
ms.date: 11/19/2020
ms.reviewer: zacook
ms.service: dynamics-365-ai
ms.topic: "article"
author: m-hartmann
ms.author: mhart
manager: shellyha
---

# Custom machine learning models

**Intelligence** > **Custom models** lets you manage workflows based on Azure Machine Learning models. Workflows help you choose the data you want to generate insights from and map the results to your unified customer data. For more information about building custom ML models, see [Use Azure Machine Learning-based models](azure-machine-learning-experiments.md).

## Responsible AI

Predictions offer capabilities to create better customer experiences, improve business capabilities, and revenue streams. We strongly recommend you balance the value of your prediction against the impact it has and biases that may be introduced in an ethical manner. Learn more about how Microsoft is [addressing Responsible AI](https://www.microsoft.com/ai/responsible-ai?activetab=pivot1%3aprimaryr6). You can also learn about [techniques and processes for responsible machine learning](https://docs.microsoft.com/azure/machine-learning/concept-responsible-ml) specific to Azure Machine Learning.

## Prerequisites

- Currently, this feature only supports web services published through [Azure Machine Learning Classic](https://studio.azureml.net) and batch pipelines deployed through the methods described in [Deploy models with Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/how-to-deploy-and-where?tabs=azcli).

- You need an Azure Data Lake Gen2 storage account associated with your Azure Studio instance to use this feature. For more information, see [Create an Azure Data Lake Storage Gen2 storage account](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)

## Add a new workflow

1. Go to **Intelligence** > **Custom models** and select **New workflow**.

1. Give your custom model a recognizable name in the **Name** field.

   > [!div class="mx-imgBorder"]
   > ![Screenshot of the New workflow pane](media/new-workflowv2.png "Screenshot of the New workflow pane")

1. Select the organization that contains the web service in **Tenant that contains your web service**.

1. If your Azure Machine Learning subscription is in a different tenant than Customer Insights, select **Sign in** with your credentials for the selected organization.

1. Select the **Workspaces** associated with your web service. There are two sections listed, one for Azure Machine Learning v1 (Machine Learning Studio Classic) and Azure Machine Learning v2 (Azure Machine Learning). If you're not sure which workspace is the right one for your Machine Learning Studio Classic web service, select **Any**.

1. Choose the Machine Learning Studio Classic web service or Azure Machine Learning Pipeline in the **Web service that contains your model** dropdown. Then, select **Next**.
   - Learn more about [publishing a web service in Machine Learning Studio Classic](https://docs.microsoft.com/azure/machine-learning/studio/deploy-a-machine-learning-web-service#deploy-it-as-a-new-web-service)
   - Learn more about publishing a pipeline in Azure Machine Learning using the [Designer](https://docs.microsoft.com/en-us/azure/machine-learning/concept-ml-pipelines#building-pipelines-with-the-designer) or [SDK](https://docs.microsoft.com/en-us/azure/machine-learning/concept-ml-pipelines#building-pipelines-with-the-python-sdk). 
      > [!NOTE]
      > Please note, that your pipeline must be published under a [Pipeline Endpoint](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-run-batch-predictions-designer#submit-a-pipeline-run).

1. For each **Web service input**, select the matching **Entity** from audience insights and select **Next**.

   > [!div class="mx-imgBorder"]
   > ![Configure a workflow](media/intelligence-screen2-updated.png "Configure a workflow")

1. In the **Model Output Parameters** step, set the following properties:
   - Machine Learning Studio Classic
      1. Enter the output **Entity name** you want web service output results to flow into.
   - Azure Machine Learning
      1. Enter the output **Entity name** you want pipeline output results to flow into.
      1. Select the **Output data store parameter name** from your [pipeline output node](#output-parameters).
      1. Select the **Output Path parameter name** from your [pipeline output node](#output-parameters).
      > [!div class="mx-imgBorder"]
      > ![Model Output Parameter Pane](media/intelligence-screen3-outputparameters.png "Model Output Parameter Pane")

1. Select the matching attribute from the **Customer ID in results** drop-down list that identifies customers and select **Save**.
   
   > [!div class="mx-imgBorder"]
   > ![Relate results to Customer data pane](media/intelligence-screen4-relatetocustomer.png "Relate results to Customer data pane")

1. You'll see the **Workflow Saved** screen with details about the workflow.
   - If you just configured a workflow for an Azure Machine Learning Pipeline, Audience Insights will **attach** the workspace that houses the pipeline. Attach allow the Audience Insights application will be provided with a **Contributor** Azure Role to the workspace.

1. Select **Done**.

1. You may now run the workflow from the **Custom Models** page.

## Edit a workflow

1. On the **Custom Models** page, select the vertical ellipsis in the **Actions** column next to a workflow you've previously created and select **Edit**.

1. You can update your workflow's recognizable name in the **Display name** field, but you can't change the configured web service or pipeline. Select **Next**.

1. For each **Web service input**, you may update the matching **Entity** from Audience Insights. Then, select **Next**.

1. In the **Model Output Parameters** step, set the following properties:
   - Machine Learning Studio Classic
      1. Enter the output **Entity name** you want web service output results to flow into.
   - Azure Machine Learning
      1. Enter the output **Entity name** you want pipeline output results to flow into.
      1. Select the **Output data store parameter name** from your [pipeline output node](#output-parameters).
      1. Select the **Output Path parameter name** from your [pipeline output node](#output-parameters).

1. Select the matching attribute from the **Customer ID in results** drop-down list that identifies customers and select **Save**.

## Run a workflow

1. On the **Custom Models** page, select the vertical ellipsis in the **Actions** column next to a workflow you've previously created.

1. Select **Run**.

Your workflow also runs automatically with every scheduled refresh. Learn more about [setting up scheduled refreshes](system.md#schedule-tab).

## Delete a workflow

1. On the **Custom Models** page, select the vertical ellipsis in the **Actions** column next to a workflow you've previously created.

1. Select **Delete** and confirm your deletion.

Your workflow will be deleted. The [entity](entities.md) that was created when you created the workflow persists, and can be viewed from the **Entities** page.
