---
layout: page
title: Explore raw data 
sub_title:

---

## Use the Event Explorer to view raw data

You have downloaded the SDK and sent data. To verify this, you can use Event Explorer to view incoming events. 

To view your events, open the **Explorer** menu, and then select your project. You'll see a sample of your app's recent events, but it might take a few minutes for them to appear. Simply select the event you want to inspect.
You can also select **Event Explorer** from the **Applications** menu on the left.

Try selecting the event at the top, waiting for sample events, and clicking an event to see what type of data it contains.

The video below shows

- How you can start the Event Explorer from the side menu
- A list of events flowing in
- Clicking on a single row to check a single record
- Selecting the event type you want from the dropdown above
- Using the **Schema** tab to get metadata on properties

{% include video.html src="EventExplorer.mp4" %}

To run more complex queries, try out our [Kusto Explorer](/developers/how-to/kusto-explorer-get-started/). Kusto Explorer enables searching and queries over your raw Aria event data. 

To connect to your Aria project in Kusto, use this connection string: [https://kusto.aria.microsoft.com:443](https://kusto.aria.microsoft.com:443)
