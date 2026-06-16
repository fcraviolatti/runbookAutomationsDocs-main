---
title: "Log Filters"
source_url: https://docs.rundeck.com/docs/manual/log-filters/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Log Filters

A Log Filter processes the output of a workflow step and may transform that output, apply metadata to the output for use by later filters or renderers, or process the output in some way. Some Log Filters can be used to capture output as Rundeck variables for use in later steps, or to transform the output for better usability in the Rundeck GUI.

A Rundeck Job may define multiple Log Filters to process the output of steps within the workflow. A Job may define *global* Log Filters that apply to all steps, as well as *step* log filters that apply only to individual steps. All of the *global* Log Filters for a Job will be processed before individual step filters.

For example, given a job that pulls API results from a web service, the results from the API might be formatted in JSON. The Render Formatted Data log filter can format the output as an HTML table for users running the job.

Conversely, as a different example, for workflow steps that need to feed data to following steps, the Key Value Data filter will parse the assigned stepâ€™s output with a regular expression to create key-value data pairs for use in other workflow steps.

## Types of Log Filters:

- [Mask Passwords](https://docs.rundeck.com/docs/manual/log-filters/mask-passwords.html)
- [Render Formatted Data](https://docs.rundeck.com/docs/manual/log-filters/render-formatted-data.html)
- [Key Value Data](https://docs.rundeck.com/docs/manual/log-filters/key-value-data.html)
- [Quiet Output](https://docs.rundeck.com/docs/manual/log-filters/quiet-output.html)
- [Highlight Output](https://docs.rundeck.com/docs/manual/log-filters/highlight-output.html)
- [Progress Badge](https://docs.rundeck.com/docs/manual/log-filters/progress-badge.html)
- [JSON JQ](https://docs.rundeck.com/docs/manual/log-filters/json-jq.html)
- [Multi-line Regex](https://docs.rundeck.com/docs/manual/log-filters/multi-line-regex.html)

## Implementation

Log Filters can be configured at a Job Step, Job, and some can be configured at the Project, or Globally across all projects and jobs.

### Job Step Log Filters

Job Filters are added to a Job Step using the Add Log Filter button on the step:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-jobstep-add.png" alt="Add Job Step Log Filter" />
<figcaption aria-hidden="true">Add Job Step Log Filter</figcaption>
</figure>

Choose the type of Log Filter and configure it using the instruction in the links above for that Filter type.

### Job Log Filters

Log Filters can be configured to apply to all Job Steps by configuring them on the "Global Log Filters" section within the Job Edit screen.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-job-add.png" alt="Add Job Log Filter" />
<figcaption aria-hidden="true">Add Job Log Filter</figcaption>
</figure>

### Project Log Filters

The [Mask Passwords](https://docs.rundeck.com/docs/manual/log-filters/mask-passwords.html) and [Highlight Output](https://docs.rundeck.com/docs/manual/log-filters/highlight-output.html) Log Filters can be configured at the Project Level and would apply to all Jobs within that project. They are configured in the Project Configuration Settings window.

Open the Project \> Click *Project Settings* \> Click *Edit Configuration* \> Click **Edit Configuration File**

The example below will configure a blue Password Mask filter, and match the word "input" and highlight it yellow.

<div class="language-text line-numbers-mode">

``` text
project.globalfilter.1.config.color=blue
project.globalfilter.1.config.replacement=[SECURE]
project.globalfilter.1.type=mask-passwords
project.globalfilter.2.config.bgcolor=yellow
project.globalfilter.2.config.regex=input
project.globalfilter.2.type=highlight-output
```

</div>

### Application Global Log Filters

The [Mask Passwords](https://docs.rundeck.com/docs/manual/log-filters/mask-passwords.html) and [Highlight Output](https://docs.rundeck.com/docs/manual/log-filters/highlight-output.html) Log Filters can be configured in the Framework file to apply to all jobs run within Rundeck/Runbook Automation.

The example below will configure a blue Password Mask filter, and match the word "input" and highlight it yellow for any job run on the server.

<div class="language-text line-numbers-mode">

``` text
framework.globalfilter.1.config.color=blue
framework.globalfilter.1.config.replacement=[SECURE]
framework.globalfilter.1.type=mask-passwords
framework.globalfilter.2.config.bgcolor=yellow
framework.globalfilter.2.config.regex=input
framework.globalfilter.2.type=highlight-output
```

</div>
