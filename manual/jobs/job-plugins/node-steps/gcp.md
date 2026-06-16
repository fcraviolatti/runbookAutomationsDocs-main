---
title: "Google Cloud Platform Node Steps"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/gcp.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Google Cloud Platform Node Steps

## Getting Started

> **Tips**
>
> It is helpful to configure the GCP Compute VM resource model plugin before using these steps: [GCP Compute VM Resource Model](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/gcp.html)

### Authentication & Configuration

Follow the steps outlined in the [**Google Cloud Integration Overview**](https://docs.rundeck.com/manual/plugins/gcp-plugins-overview) doc to configure credentials for the GCP plugins. Credentials can be configured on a per Project basis or for the entire Runbook Automation system.

## Compute VM Node Steps (Enterprise Only)

### GCP / VM / Start

Start the Compute VM instance.

### GCP / VM / Stop

Start the Compute VM instance.

### GCP / VM / Restart

Start the Compute VM instance.

### GCP / VM / Delete

Terminate the Compute VM instance.

> **Caution**
>
> Be very careful when using this step. It would be possible to remove a lot of instances by mistake if the node filter is too broad.
