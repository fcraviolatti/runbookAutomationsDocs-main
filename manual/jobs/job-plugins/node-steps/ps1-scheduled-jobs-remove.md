---
title: "Remove Scheduled Powershell Job"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/ps1-scheduled-jobs-remove.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Remove Scheduled Powershell Job

The **PS1 Scheduled Jobs Remove** plugin removes a scheduled task on a Windows node.

## Prerequisites

This plugin utilizes the [WinRM Node Executor](https://docs.rundeck.com/docs/manual/projects/node-execution/powershell.html) to connect to the target Windows node. The Node Executor must be configured for the Project or for the target node in order for the plugin to work.

This plugin will only execute through a Windows installation of Runbook Automation or the Enterprise Runner.

## Configuration

The following fields are required for configuration:

- **Name**: The name of the scheduled task to remove.

![PS1 Scheduled Jobs Remove Configuration](https://docs.rundeck.com/docs/assets/img/ps1-scheduled-jobs-remove.png)
