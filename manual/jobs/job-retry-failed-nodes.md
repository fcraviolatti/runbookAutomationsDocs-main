---
title: "Job Retry Failed Nodes (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-retry-failed-nodes.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Job Retry Failed Nodes (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

This plugin allows Jobs to *retry* failed executions just on failed nodes.

When you enable this plugin for a job, with retry options set, the plugin will review the previous execution's list of succeeded nodes and will just select on the next execution the nodes that either *failed* or were *not started*.

## Requirements

> **Warning**
>
> This plugin works in conjunction with the "Retry" options for Jobs enabled. [Please read more about those settings here](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html#retry).

## Usage

To use this plugin, edit or create a Job, and under the "Execution Plugins" tab, and configure the [Retry options](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html#retry). ![Retry Job Settings](https://docs.rundeck.com/docs/assets/img/retry-failed-jobs-retry.png)

On the Execution Plug-ins tab enable the checkbox next to the "Retry on failed nodes" plugin.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/retry-failed-jobs-conf.png" alt="Execution Plugins" />
<figcaption aria-hidden="true">Execution Plugins</figcaption>
</figure>

When the job runs and fails, subsequent retry executions will only run on the nodes that didn't succeed.

## Example

The following job ran on 4 nodes: 2 succeeded, 1 failed, and 1 wasn't started.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/retry-failed-jobs-execution-failed.png" alt="Failed Execution" />
<figcaption aria-hidden="true">Failed Execution</figcaption>
</figure>

Then, on the next retry executions, just the remaining nodes were targeted.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/retry-failed-jobs-execution-succeed-resume.png" alt="Next Retry Execution Resume" />
<figcaption aria-hidden="true">Next Retry Execution Resume</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/retry-failed-jobs-execution-succeed-log.png" alt="Next Retry Execution Log" />
<figcaption aria-hidden="true">Next Retry Execution Log</figcaption>
</figure>
