---
title: "JSON jq key/value mapper"
source_url: https://docs.rundeck.com/docs/manual/log-filters/json-jq.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# JSON jq key/value mapper

This log filter will parse JSON data in a rundeck job step and create key-value data as Rundeck variables in the data context. The filter uses the jq library to make jquery searches into the data returns.

## Usage

The filter has 3 fields:

- *jq Filter* - jquery-style filter against the log output for the Rundeck job step this filter is attached to. Required.
- *Prefix* - optional result prefix that will be used in the Rundeck data context as the variable key.
- *Log Data* - checkbox. If true, log the captured data to the jobâ€™s log stream.

The example below will filter the log results of a Rundeck API query. Using the HTTP Request Node Step and a working API token for your Rundeck user:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-jsonjq-example1.png" />
</figure>

The API results in our demo Rundeck instance look like this:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-jsonjq-example2.png" />
</figure>

Apply the JSON jq key/value Mapper filter to the HTTP Request node step:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-jsonjq-example3.png" />
</figure>

Now, when running the job, the log filter creates the following data variable:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-jsonjq-example4.png" />
</figure>

So it can be used in later job steps:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-jsonjq-example5.png" />
</figure>

With the results:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-jsonjq-example6.png" />
</figure>
