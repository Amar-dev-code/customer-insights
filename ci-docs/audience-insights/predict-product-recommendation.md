---
title: "Product recommendation prediction"
description: "Predict the products a customer is likely to purchase or interact with."
ms.date: 02/15/2021
ms.reviewer: zacook
ms.service: customer-insights
ms.subservice: audience-insights
ms.topic: conceptual
author: m-hartmann
ms.author: mhart
manager: shellyha
---

# Product recommendation prediction (preview)

The product recommendation model creates sets of predictive product recommendations. Recommendations are based on previous purchase behavior and customers with similar purchase patterns. You can create new product recommendation predictions on the **Intelligence** > **Predictions** page. Select **My predictions** to see other predictions that you've created.

Product recommendations may be subject to local laws and regulations as well as customer expectations, which the model is not built to specifically take into account.  As a user of this predictive capability, **you must review the recommendations prior to delivering them to your customers** to ensure you are complying with any applicable laws or regulations, as well as customer expectations for what you may recommend. 

Additionally, the output of this model will give you recommendations based on the product ID. Your delivery mechanism will need to take predicted product IDs and map them to appropriate content for your customers to account for localization, image content, and other business specific content or behavior.

## Sample Guide

If you're interested in trying this feature but don't have data to complete the requirements below, you can [create a sample implementation](sample-guide-predict-product-recommendation.md).

## Prerequisites

- At least [Contributor permissions](permissions.md) in Customer Insights.
- Business knowledge to understand different types of products for your business and how your customers interact with them. We support recommending products that have been previously purchased by your customers or recommendations for new products.
- Data about transactions, purchases, and their history:
    - Transaction identifiers to distinguish purchases or transactions.
    - Customer identifiers to map transactions to your customers.
    - Transaction event dates that specify dates the transaction occurred on.
    - (Optional) Product ID information for the transaction.
    - (Optional) If a transaction is a return or not.
    - The semantic data schema requires the following information:
        - **Transaction ID:** A unique identifier of a purchase or transaction.
        - **Transaction date:** The date the of the purchase or transaction.
        - **Value of the transaction:** The numerical value of the purchase or transaction.
        - **Unique product ID:** The ID of the product or service purchased if your data is at a line item level.
        - (Optional) **Purchase or return:** A true/false field that identifies if the transaction was a return or not. If the **Value of the transaction** is negative, we will also use this information to infer a return.


## Create a product recommendation prediction

1. In Customer Insights, go to **Intelligence** > **Predictions**.

1. Select the **Product recommendations model (preview)** tile and select **Use this model**.
   > [!div class="mx-imgBorder"]
   > ![Product Recommendation model tile with Use this model button](media/product-recommendation-usethismodel.PNG "Product Recommendation model tile with Use this model button")

1. Review the information about the model requirements. If you have the required data, select **Get started**.

### Name model

1. Provide a name for the model to distinguish it from other models.

1. Enter a name for the output entity using letters and numbers only, without any spaces. That's the name that the model entity will use. Then, select **Next**.

### Define product recommendation configuration

1. Set the **Number of products** you want to recommend to a customer. This value depends on how your delivery method fills data. If you can recommend three products, set this value accordingly.
   
   >[!TIP]
   > You can select **Save and close** at any time to save the prediction as a draft. You'll find the draft prediction in the **My predictions** tab.

1. Choose if you want to **Suggest products customers have recently purchased**.

1. If you've selected to *not* recommend recently purchased products, set the **Look back window**. This setting specifies the time frame the model considers before recommending the product to the user again. For example, indicate a customer purchases a laptop every 2 years. This window will look at the purchase history for the last 2 years, and if they find an item, the item will be filtered from the recommendations.

1. Select **Next**

### Add required data

1. Select **Add data** for **Customer transaction history** and choose the entity that provides the transaction/purchase history information as described in the [prerequisites](#prerequisites).

1. Map the semantic fields to attributes within your purchase history entity and select **Next**. For descriptions of the fields, have a look at the [prerequisites](#prerequisites).
   > [!div class="mx-imgBorder"]
   > ![Define the entity relationship](media/product-recommendation-purchasehistorymapping.PNG "Purchase history page showing semantic attributes that are mapped to fields in the selected purchase history entity")

1. If the fields aren't filled in, configure the relationship from your purchase history entity to the *Customer* entity.
    1. Select the **Purchase history entity**.
    1. Select the **Field** that identifies the customer in the purchase history entity. It needs to relate to the primary customer ID of your *Customer* entity.
    1. Select the **Customer entity** that matches your primary customer entity.
    1. Enter a name that describes the relationship.
       > [!div class="mx-imgBorder"]
       > ![Purchase history page showing the creation of a relationship to customer](media/model-purchase-join.png "Purchase history page showing the creation of a relationship to customer")

1. Select **Save**.

1. Select **Next**.

### Configure product filters

Sometimes, only certain products are beneficial or appropriate for the type of prediction you build. Product filters let you identify a subset of products with specific characteristics to recommend to your customers. This may increase the personalization of the recommendations to your customers. The model will use all the products available to learn patterns but only use the products matching the product filter in its output.

1. In the **Add product information** step, add your product catalog with information for each product. Map the information required in select **Next**.

3. In the **Product filters** step, choose between the following options.

   * **No filters**: Use all products in the product recommendation prediction.

   * **Define specific product filters**: Use specific products in the product recommendation prediction.

1. Select **Next**.

1. If you choose to define a product filter, you need to define it now. In the **Product catalog attributes** pane, select the the attributes from your *Product Catalog entity* that you want include in the filter.

<!-- please introduce the product catalog entity in the setup above and also list it as an optional data prerequisite-->

   :::image type="content" source="media/product-filters-sidepane.png" alt-text="Side pane showing attributed in the product catalog entity to select for product filters.":::

1. Choose if you want the product filter to use **and** or **or** connectors to logically combine your selection of attributes from product catalog.
   
   :::image type="content" source="media/product-filters-sample.png" alt-text="Sample configuration of product filters combined with logical AND connectors.":::

1. Select **Next**.

### Set update schedule and review configuration

1. Set a frequency to retrain your model. This setting is important to update the accuracy of predictions as new data is imported into Customer Insights. Most businesses can retrain once per month and get a good accuracy for their prediction.

1. Select **Next**.

1. Review the configuration. You can go back to any part of the prediction configuration by selecting **Edit** under the shown value. Or you can select a configuration step from the progress indicator.

1. If all values are configured correctly, select **Save and run** to begin the prediction process. On the **My predictions** tab, you can see the status of your predictions. The process may take several hours to complete depending on the amount of data used in the prediction.

## Review a prediction status and results

1. Go to the **My predictions** tab on **Intelligence** > **Predictions**.
   > [!div class="mx-imgBorder"]
   > ![View of the My Predictions page](media/product-recommendation-mypredictions.PNG "View of the My Predictions page")

1. Select the prediction you want to review.
   - **Prediction name:** The name of the prediction provided when creating it.
   - **Prediction type:** The type of model used for the prediction
   - **Output entity:** Name of the entity to store the output of the prediction. You can find an entity with this name on **Data** > **Entities**.
   - **Predicted field:** This field is populated only for some types of predictions, and isn't used in churn prediction.
   - **Status:** The current status of the prediction's run.
        - **Queued:** The prediction is currently waiting for other processes to run.
        - **Refreshing:** The prediction is currently running the "score" stage of processing to produce results that will flow into the output entity.
        - **Failed:** the prediction has failed. Select **Logs** for more details.
        - **Succeeded:** the prediction has succeeded. Select **View** under the vertical ellipses to review the prediction
   - **Edited:** The date the configuration for the prediction was changed.
   - **Last refreshed:** The date the prediction refreshed results in the output entity.

1. Select the vertical ellipses next to the prediction you want to review results for and select **View**.
   > [!div class="mx-imgBorder"]
   > ![View of options in the vertical ellipses menu for a prediction including edit, refresh, view, logs, and delete](media/product-recommendation-verticalellipses.PNG "View of options in the vertical ellipses menu for a prediction including edit, refresh, view, logs, and delete")

1. There are three primary sections of data within the results page:
    1. **Training model performance:** A, B, or C are possible scores. This score indicates the performance of the prediction, and can help you make the decision to use the results stored in the output entity.
        - Scores are determined based on the following rules:
            - **A** The model will be considered **A** quality if the "Success @ K" metric is at least 10% more the baseline. 
            - **B** The model will be considered **B** quality if the "Success @ K" metric is 0 to 10% more than the baseline.
            - **C** The model will be considered **C** quality if the "Success @ K" metric is less than than the baseline.
               
               > [!div class="mx-imgBorder"]
               > ![View of the model performance result](media/product-recommendation-modelperformance.PNG "View of the model performance result")
            - **Baseline**: The model takes the top most recommended products by purchase count across all customers, and uses learned rules identified by the model to create a set of recommendations for the customers. The predictions are then compared to the top products, as calculated by the number of customers that had purchased the product. If a customer has at least one product in their recommended products that was also seen in the top purchased products, they're considered a part of the baseline. If there were 10 of these customers that had a recommended product purchased out of 100 total customers, the baseline would be 10%.
            - **Success @ K**: Using a validation set of time period of transactions, recommendations are created for all customers and compared against the validation set of transactions. For example, in a 12 month period, month 12 might be set aside as a validation set of data. If the model predicts at least one thing you would purchase in month 12 based on what it learned from the previous 11 months, the customer would increase the "Success @ K" metric.
    
    1. **Most suggested products (with tally):** The top 5 products that were predicted for your customers.
       > [!div class="mx-imgBorder"]
       > ![Graph showing the top 5 most recommended products](media/product-recommendation-topproducts.PNG "Graph showing the top 5 most recommended products")
    
    1. **High-confidence product recommendations:** A sample of recommendations provided to your customers that the model believes are likely to be purchased by the customer.
       > [!div class="mx-imgBorder"]
       > ![List showing high confidence suggestions for a select set of individual customers](media/product-recommendation-highconfidence.PNG "List showing high confidence suggestions for a select set of individual customers")

## Fix a failed prediction

1. Go to the **My predictions** tab on **Intelligence** > **Predictions**.

1. Select the prediction you would like to view error logs for and select **Logs**.

1. Review all the errors. There are several types of errors that can occur, and they describe what condition caused the error. For example, an error that there's not enough data to accurately predict is typically resolved by loading additional data into Customer Insights.

## Refresh a prediction

Predictions automatically refresh on the same [schedule your data refreshes](system.md#schedule-tab) as configured in settings.

1. Go to the **My predictions** tab on **Intelligence** > **Predictions**.

1. Select the vertical ellipses next to the prediction you want to refresh.

1. Select **Refresh**.

## Delete a prediction

Deleting a prediction will also remove its output entity.

1. Go to the **My predictions** tab on **Intelligence** > **Predictions**.

1. Select the vertical ellipses next to the prediction you want to delete.

1. Select **Delete**.


[!INCLUDE[footer-include](../includes/footer-banner.md)]
