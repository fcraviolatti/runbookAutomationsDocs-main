---
title: "Loop Script Plugins (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/loop-plugins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Loop Script Plugins (Commercial)

These plugins add the functionality of running inline scripts, using the node executor and file copier, inside a loop. So far the plugin has two different iteration types: iterating a JSON array and iterating the script until it finishes successful (exit code zero)

## Included Workflow steps Plugins

- Loop / Step / Run Script from a Json Array
- Loop / Step / Run Script until Success

## Run Script from a Json Array

This plugin runs an inline script based on a provided JSON Array.  
In order to capture the JSON array in previous steps (data context), you can use the [Loop / Log Filter / Store and Validate JSON](https://docs.rundeck.com/docs/manual/log-filters/loop-plugins.html) log filter plugging.

### Plugin Configuration

- ***Input array data from context***: JSON array from data context (eg: `data.json`). This value must be captured in a previous step with a Log Filter and is expecting an array element.
- ***Input Array (raw string)***: (Optional) If you don't want to use data context you can add a raw JSON array.
- ***Script***: Script to Run
- ***Invocation String***: (Optional) add the invocation string like: bash, powershell, python, etc.
- ***File Extension***: (Optional) add the file extension string like: `.sh`, `.ps1`, `.py`, etc.
- ***Stop Iteration on failure***: Stop execution if the iteration failed.

The input JSON array **must** be a simple key/value JSON array:

<div class="language-text line-numbers-mode">

``` text
[
  {"id":"1","name":"test 1"},
  {"id":"2","name":"test 2"}
]
```

</div>

Then, the script will run for each of JSON object included in the input array. Inside the inline scripts you can capture the variables from each JSON object using the following convention (\$vars.key):

<div class="language-text line-numbers-mode">

``` text
set -e
token="@option.token@"
id="$vars.id"
name="$vars.name"

echo "token: $token"
echo "id: $id"
echo "name: $name"
```

</div>

![plugin-config](https://docs.rundeck.com/docs/assets/img/loop-step-run-script-json-attributes.png)![plugin-config](https://docs.rundeck.com/docs/assets/img/loop-step-run-script-json-definition.png)![plugin-config](https://docs.rundeck.com/docs/assets/img/loop-step-run-script-json-output.png)

## Run Script until Success

This plugin runs an inline script until it finishes successfully

### Plugin Configuration

- ***Retries***: Max number of iterations.
- ***Retry Delay***: Retry Delay in seconds.
- ***Script***: Script to Run.
- ***Invocation String***: (Optional) add the invocation string like: bash, powershell, python, etc.
- ***File Extension***: (Optional) add the file extension string like: `.sh`, `.ps1`, `.py`, etc.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/loop-step-run-until-success.png" alt="plugin-config" />
<figcaption aria-hidden="true">plugin-config</figcaption>
</figure>
