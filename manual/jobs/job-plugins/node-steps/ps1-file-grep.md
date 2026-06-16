---
title: "PS1 File Grep - Wait for Windows File Text"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/ps1-file-grep.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# PS1 File Grep - Wait for Windows File Text

The **PS1 File Grep** plugin waits for a file on a Windows node to contain specific text. The plugin is useful for waiting for a file at a specific path to contain specific text.

## Prerequisites

This plugin utilizes the [WinRM Node Executor](https://docs.rundeck.com/docs/manual/projects/node-execution/powershell.html) to connect to the target Windows node. The Node Executor must be configured for the Project or for the target node in order for the plugin to work.

This plugin will only execute through a Windows installation of Runbook Automation or the Enterprise Runner.

## Configuration

The following fields are required for configuration:

- **Number of tries**: The number of times **`File path`** will be checked. Each attempt will be spaced by **`Interval`** milliseconds.
- **Interval**: The timeout in milliseconds between **`Number of Tries`** of checking the **`File path`** for the file.
- **File Path**: The file-path (directory and file name) to check for having the text specified in **`Having Text`**.
- **Having Text**: Text to match inside **`File Path`**.

![PS1 File Grep Configuration](https://docs.rundeck.com/docs/assets/img/ps1-file-grep.png)
