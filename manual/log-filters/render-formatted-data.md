---
title: "Render Formatted Data"
source_url: https://docs.rundeck.com/docs/manual/log-filters/render-formatted-data.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Render Formatted Data

This is a data presentation log filter - meaning that this filter doesnâ€™t alter the log output from the job step itâ€™s applied to; instead, it adds some metadata to the logs allowing Rundeck to render it in sanitized HTML by use of [Content Converter Plugins](https://docs.rundeck.com/docs/developer/content-converter-plugins.html). This is particularly useful to display the return values of scripts and API calls.

Output will be an HTML table with the data formatted appropriately.

## Usage

First, ensure that the job step is returning output that is able to be parsed by one of the filter datatypes. If the job output will be entirely the expected datatype, then set the Data Type field in the log filter to the appropriate type. Otherwise, Rundeck expects a prefix and suffix to the parsable data. To mark a section of output with a datatype, echo this marker defining it:

    `#BEGIN:RUNDECK:DATATYPE:<datatype>`

Replacing `<datatype>` with one of the supported data types.

You can mark the section as ending by echoing the line below. Otherwise, when the step ends the plugin will treat it as ended.

    `#END:RUNDECK:DATATYPE`

Supported datatypes:

- `application/json` [JSON](http://json.org) (synonyms: `json`)
- `application/x-java-properties` [Java Properties](https://docs.oracle.com/javase/7/docs/api/java/util/Properties.html#load(java.io.Reader)) (synonyms: `properties`)
- `text/csv` CSV (synonyms: `csv`)
- `text/html` HTML (synonyms: `html`)
- `text/x-markdown` [Markdown](https://en.wikipedia.org/wiki/Markdown) (synonyms: `markdown`,`md`)

### Use for all output

You can also choose a value for the `Data Type` property, to preset a datatype to use for the entire output log data. If this is set, then no "BEGIN" marker is looked for.

The data can then be rendered in the Rundeck Log output GUI. The specific renderer for the data type is determined by available ViewConverter plugins.

For example, you can emit JSON data, and prefix it with:

    echo "#BEGIN:RUNDECK:DATATYPE:application/json"

Then emit json data (only)

    cat file.json

Then END the datatype:

    echo "#END:RUNDECK:DATATYPE"

The log output will then capture all of the JSON data in a single log event, and mark it as `application/json` data type.

## Examples

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-render-example1.png" />
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-render-example2.png" />
</figure>

### See Also

- [Content Converter Plugins](https://docs.rundeck.com/docs/developer/content-converter-plugins.html)
