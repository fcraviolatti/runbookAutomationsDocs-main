---
title: "Tabular Data Converter"
source_url: https://docs.rundeck.com/docs/manual/content-converters/tabular-data.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Tabular Data Converter

Parses Tabular text (csv) into a a Java object.

The [HTML Table View Converter](https://docs.rundeck.com/docs/manual/content-converters/html-table-view.html) plugin can render this as a HTML Table.

Expected content data type: `text/csv`.

The default separator is a comma, but another separator can be specified with the `sep` parameter:

- `space` - space character
- `tab` - tab character
- `comma` - comma character
- `vertbar` - vertical bar character (`|`)
- `<anything>` - any string

If the `header` parameter is `true`, Or if the second row of data is all `-` (hyphen) characters, the first row of data will be used as the header names.

Additionally if the data type contains `;header=present` a header is assumed present.

## Input Types

- `text/csv` - `String`
- `text/csv;header=present` - `String` CSV data with header row

## Output Types

- `application/x-java-col-list` - `List`

## Related Plugins

- [HTML Table View Converter](https://docs.rundeck.com/docs/manual/content-converters/html-table-view.html)
