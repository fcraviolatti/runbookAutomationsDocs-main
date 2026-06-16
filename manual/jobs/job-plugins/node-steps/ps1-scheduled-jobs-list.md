---
title: "PS1 Scheduled Jobs List"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/ps1-scheduled-jobs-list.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# PS1 Scheduled Jobs List

The **PS1 Scheduled Jobs List** plugin lists scheduled tasks on a Windows node.

## Prerequisites

This plugin utilizes the [WinRM Node Executor](https://docs.rundeck.com/docs/manual/projects/node-execution/powershell.html) to connect to target Windows node. The WinRM Node Executor must be configured for the Project or target node in order for the plugin to work.

This plugin will only execute through a Windows installation of Runbook Automation or the Enterprise Runner.

![PS1 Scheduled Jobs List Configuration](https://docs.rundeck.com/docs/assets/img/ps1-scheduled-jobs-list.png)
