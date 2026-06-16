---
title: "Run Job Webhook Plugin"
source_url: https://docs.rundeck.com/docs/manual/webhooks/run-job.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Run Job Webhook Plugin

The *Run Job* webhook plugin receives a webhook event and executes the configured job. You can pass the payload of the webhook to the job or use the event payload information to supply Options, a Node Filter, and/or *Run As* user to the job as inputs.

> **Tips**
>
> This Plugin only handles JSON payloads.

## Usage

Add a new webhook in the UI, then pick the *Run Job* webhook event plugin.  
You will see the following configuration options in the `Plugin Configuration` section.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/webhook-run-job-plugin.png" alt="Run Job Config" />
<figcaption aria-hidden="true">Run Job Config</figcaption>
</figure>

Once you have saved the webhook, you will see a `Post Url`. You can post a test message to that Url using curl, httpie or your favorite API Client to ensure that it runs the job as expected.

### Response

The Webhook Run Job plugin will return the job id and execution id to the caller upon a successful job kickoff. You can use the execution id to check the progress of the job execution.

Example Response:

<div class="language-text line-numbers-mode">

``` text
{
    "executionId": "7",
    "jobId": "9bb310cf-fa0a-4a66-89a0-1892d73021e2"
}
```

</div>

## Configuration

The JSON that is received by the plugin can be used to supply Job Options, Node Filter, and/or the *Run As* user.

#### Using parsed data

If the plugin received the following JSON

<div class="language-json line-numbers-mode">

``` json
{"field1":"value1","sub1":{"subfield": "subval"}}
```

</div>

You could use that data by specifying:

`${data.field1}1`

or

`${data.sub1.subfield}`

These values are used in the Webhook configuration fields as shown in the example below.

#### Using the raw payload

If you had a job that had an option named `whkpayload` you could send the entire JSON payload to that option like this: `-whkpayload ${raw}`

#### Webhook context variables

The following context variables can be used:

<div class="language-properties line-numbers-mode">

``` properties
id:unique event id
project:the project that owns the webhook
sender:the ip address of the sending system
timestamp:the epoch milliseconds when the event was received
```

</div>

These variables can be used in the webhook setting for Options by specifying:

`${webhook.id}``${webhook.project}``${webhook.sender}``${webhook.timestamp}`

### Example

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/webhook-run-job-example.png" alt="Run Job Example" />
<figcaption aria-hidden="true">Run Job Example</figcaption>
</figure>

Another note is that the Options will be sent to the job even if those options have not been configured on that job. To reference the values passed from the webhook use `${option.<value>}` to reference the values in the job steps. Below is an example job definition that corresponds with the example Webhook image shown above.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/webhook-run-job-examplejob.png" alt="Run Job Workflow Example" />
<figcaption aria-hidden="true">Run Job Workflow Example</figcaption>
</figure>

<div class="language-yaml line-numbers-mode">

``` yaml
- defaultTab: nodes
  description: Shows all variables available using Log Data Step
  executionEnabled: true
  group: Demo/Echo
  id: 80623689-77ee-4bce-a342-ff669eac397e
  loglevel: INFO
  name: Show All Variables
  nodeFilterEditable: false
  plugins:
    ExecutionLifecycle: {}
  scheduleEnabled: true
  schedules: []
  sequence:
    commands:
    - description: Echo Raw Input
      exec: echo ${option.raw}
    - description: Show Field 1 Value
      exec: 'echo "This is Field 1: ${option.field1}"'
    - configuration:
        debugOnly: 'false'
      description: Show all variables in execution
      nodeStep: false
      type: log-data-step
    keepgoing: false
    strategy: node-first
  tags: demo
  uuid: 80623689-77ee-4bce-a342-ff669eac397e
```

</div>
