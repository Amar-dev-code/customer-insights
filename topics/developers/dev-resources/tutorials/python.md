---
uid: developers/downloads/python
title: Get Started with Python
author: vroha
description: Get Started with Python
ms.author: hakrou
ms.date: 04/12/2019
ms.service: product-insights
ms.topic: conceptual
---
# Getting Started with Product Insights SDK

## Installing Dependencies
As this is the Python SDK, the only required dependency is Python! The SDK supports both Python 2.7 and 3.x. There are no further dependencies, as they are bundled with the SDK.

## Installing the SDK
There are 2 primary ways to use the Python SDK:
* Install the SDK to your Python interpreter's `site-packages` folder, or
* Place the SDK `.egg` file somewhere and add it to `sys.path`

This file describes how to do both.

#### Installing to site-packages
1. Open your terminal and `cd` to the directory containing the file `product_insights-x.y.z.egg`.
2. Run `python -m easy_install product_insights-x.y.z.egg`
3. Import the SDK
```python
import product_insights
from product_insights import LogManager, EventProperties
```

#### Adding to the Import Path
The SDK can also be used without installation using only the .egg file.
In any Python script, use the following code recipe to use the SDK:
```python
import sys
sys.path.append('/path/to/product_insights-2.0.0.egg')

# Import the SDK!
import product_insights
from product_insights import LogManager, EventProperties
```

## Using the SDK
While a full example can be seen in the SDK's `sample.py` file, the basic usage pattern is demonstrated here.

```python
from product_insights import LogManager, EventProperties, PiiKind

# Initialize the SDK and get a logger
# Use your actual tenant token - it will be longer than this example
logger = LogManager.initialize('0123456789abcdef-01234567-89abcdef')

# Create an event
event = EventProperties('some_event_name')

# fill the event values
event.set_property('rpm', 50)
event.set_property('device_name', 'Test Device 9000')
event.set_property('active', True)

# Maybe even set a PII (Personally Identifiable Information) value
# This value will be obfuscated on upload, and will be unreadable
event.set_property('username', 'SuperCoolUsername_42', pii_kind=PiiKind.PiiKind_DistinguishedName)

# log the event
logger.log_event(event)
```

Keep in mind that the SDK batches events and uploads them periodically (by default, a little over 3 times a second) rather than immediately when calling `log_event()`.

To force all events to be uploaded, call
```python
LogManager.flush()
```

Before your program exits, you should be sure to call
```python
LogManager.flush_and_tear_down()
```

This convenience method flushes the SDK and ensures it shuts down cleanly. 

 
