---
uid: developers/downloads/ingest
title: Getting started with the Ingestion Tool
---

The Ingestion Tool can be used to send data from a CSV file to Aria.

The first line of the CSV file must contain the header that specifies the field names.
Each subsequent line in the CSV file must contain data (field values) for one event.

## Download the Ingestion Tool

To download the tool, click the following link.

[Download the Ingestion Tool](https://ariamediahost.blob.core.windows.net/sdk/aria-powershell.zip)

## Run the Ingestion Tool

You can run the Ingestion Tool in PowerShell as follows:

```powershell
.\IngestionTool.ps1 -CsvFile YOUR_CSV_FILE -schema YOUR_SCHEMA_FILE -EventName YOUR_EVENT_NAME -ApiToken YOUR_API_KEY
```

The `-CsvFile` and `-ApiToken` parameters are mandatory, and the user
must provide either the `-schema` or `-EventName` parameter.

> **Note**: Provide a -schema parameter if you already have a data schema defined
> according to the Ingestion Data Scheme (link). 
> Alternatively, you can simply provide an event name for the data you are sending, and a schema will be auto-generated. 
> To override the system timestamp, you will need a custom schema. 
> Without a schema, all events will have the ingestion time set to the timestamp.

If you run the Ingestion Tool in the directory where you put it, it
will print the results on screen.

## Get a project key

To find `YOUR_API_KEY`, you'll create a project (previously known as
tenant), which generates a project key (a string of hexadecimal
digits) that you'll use to authenticate your app to Aria. Visit the
Aria Instrument Wizard and follow the instructions on the first page.
For **Project**, specify the name of your local project or solution.
On the second page, select any platform and click **Skip this wizard**.
On the third page, copy the Ingestion Key. Use it for your 
API token.

[Aria Instrument Wizard](https://portal.aria.ms/instrument/project)

## For more information

For more details on running this program, type `help .\IngestionTool`
in your PowerShell window.

See also the [Ingestion Data Scheme](https://www.aria.ms/developers/downloads/IngestionDataScheme).
