---
title: "List Largest Files in Directory"
source_url: https://docs.rundeck.com/docs/learning/solutions/storage-management/storage-list-largest-files.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# List Largest Files in Directory

This documentation provides details on how to use a Rundeck job to list the largest files by file size in a specified directory and its subdirectories. This job is useful for identifying large files that may be consuming significant disk space.

## Job Description

This job will:

- List the largest files by file size in the current directory and its subdirectories.

### Assumptions

- The job assumes the node is a Linux endpoint with `find`, `du`, `sort`, and `head` installed.
- The default start directory is the Runner Execution folder or the home folder of the authenticated user on remote nodes.

### Notes

- No nodes are selected by default. Change Target Nodes and select the endpoint to run against.
- The job can **take a long time to run** if the directory has a lot of files in it.

## Configuration

### Job Options

- **Start Directory:** The path where the scan will start. The default is the current execution directory (`.`).
- **Number of Results:** Choose how many results should be returned in the list. Some dropdown options are provided, but any number can be specified.

![job-options](https://docs.rundeck.com/docs/assets/img/storage-largest-files-job.png)  

## Successful Execution

![success-output](https://docs.rundeck.com/docs/assets/img/storage-list-largest-output.png)
