---
title: "Kubernetes StatefulSet Plugins"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-statefulset-plugins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Kubernetes StatefulSet Plugins

## Setup

Follow the steps outlined in the [**Kubernetes Plugins Overview**](https://docs.rundeck.com/manual/plugins/kubernetes-plugins-overview) to configure authentication for Kubernetes Job steps. Credentials can be configured on a per Job Step basis, Project basis, or for the entire Runbook Automation system.

To see property syntax for configuring properties at the Project or System level, navigate to **System Menu** (gear icon in the upper-right) -\> **Plugins** -\> **Installed Plugins**. Locate the specific plugin and click on the **i** icon. All of the plugin properties will be listed.

## Kubernetes / StatefulSet / Waitfor

This plugin pauses the workflow until the specified StatefulSet has been successfully deployed.
