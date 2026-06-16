---
title: "Store and Validate JSON (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/log-filters/loop-plugins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Store and Validate JSON (Commercial)

## Log Filter Store and Validate JSON

The "Store and Validate JSON" Log filter plugin validate and store a JSON string in the job context. It can be used to pass the input JSON parameter to the [Loop / Step / Run Script from a JSON Array](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/loop-plugins.html) and [Loop / Node Step / Run Script from a JSON Array](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/loop-plugins.html) plugins

### Plugin Configuration

- ***Group*** The group of the context variable
- ***Path*** The path of the context variable
- ***Log Data*** Print the captured value

you will access the context variable using `${group.path}`

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/loop-log-filter.png" alt="plugin-config" />
<figcaption aria-hidden="true">plugin-config</figcaption>
</figure>
