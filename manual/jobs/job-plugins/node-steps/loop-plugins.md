---
title: "Loop Script Plugins (Self Hosted)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/loop-plugins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Loop Script Plugins (Self Hosted)

These plugins add the functionality of running inline scripts, using the node executor and file copier, inside a loop. So far the plugin has two different iteration types: iterating a JSON array and iterating the script until it finishes successful (exit code zero)

> **Note**
>
> This plugin is only available in the Self Hosted version of the product.

## Included Plugins

- Loop / Node Step / Run Script from a Json Array
- Loop / Node Step / Run Script until Success

## Run Script from a Json Array

This node step plugin runs an inline script based on a provided JSON Array (per each node). In order to capture the JSON array in previous steps (data context), you can use the [Loop / Log Filter / Store and Validate JSON](https://docs.rundeck.com/docs/manual/log-filters/loop-plugins.html) log filter plugging.

### Plugin Configuration

- ***Input array data from context***: JSON array from data context (eg: `data.json`). This value must be captured in a previous step with a Log Filter.
- ***Input Array (raw string)***: (Optional) If you don't want to use data context you can add here the raw JSON array.
- ***Script***: Script to Run
- ***Invocation String***: (Optional) add the invocation string like: bash, powershell, python, etc
- ***File Extension***: (Optional) add the file extension string like: .sh, .ps1, .py, etc
- ***Stop Iteration on failure***: Stop execution if the iteration failed

The input JSON array must be a simple key/value JSON array:

> **Tips**
>
> The JSON provided cannot have spaces in the attribute name, this is allowed just for the values

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
token="@option.token"
id="$vars.id"
name="$vars.name"

echo "token: $token"
echo "id: $id"
echo "name: $name"
```

</div>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/loop-nodestep-run-script-json-atrributes.png" alt="plugin-step-config" />
<figcaption aria-hidden="true">plugin-step-config</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/loop-nodestep-run-script-definition.png" alt="plugin-step-definition" />
<figcaption aria-hidden="true">plugin-step-definition</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/loop-nodestep-run-script-output.png" alt="plugin-step-output" />
<figcaption aria-hidden="true">plugin-step-output</figcaption>
</figure>

## Run Script until Success

This node step plugin runs an inline script until it finishes successfully (per each node)

### Plugin Configuration

- ***Retries***: Max number of iterations
- ***Retry Delay***: Retry Delay in seconds
- ***Script***: Script to Run
- ***Invocation String***: (Optional) add the invocation string like: bash, powershell, python, etc
- ***File Extension***: (Optional) add the file extension string like: .sh, .ps1, .py, etc

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/loop-nodestep-run-until-success.png" alt="plugin-step-config" />
<figcaption aria-hidden="true">plugin-step-config</figcaption>
</figure>
