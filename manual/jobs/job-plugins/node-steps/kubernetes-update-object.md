---
title: "Kubernetes Clusters - Update Object"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-update-object.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Kubernetes Clusters - Update Object

> **Available in PagerDuty Runbook Automation Commercial products.**

## Overview

This plugin updates a specified object of a selected kind within a Kubernetes cluster. Since this is a node-step plugin, multiple Kubernetes clusters or namespaces can be targeted within a single Job.

## Configuration

### Prerequisites

Before configuring the Kubernetes Update Object plugin, the target clusters must be added to the Runbook Automation instance and the authentication method must be configured. This is done by following the steps outlined in the [Kubernetes Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

### Add Kubernetes Update Object Step

When building a Job, add the **Kubernetes / Clusters / Update Object** node step:

![Kubernetes Update Object](https://docs.rundeck.com/docs/assets/img/k8s-cluster-update-object.png)  

Configure the following fields:

- **Object Name**: The name of the object to be updated.
- **YAML Definition**: The YAML definition of the object to be updated.
- **Namespace**: The namespace where the object resides. Default is `default`.
- **Object Type**: Select the type of object to update (e.g., Pods, Deployments, Services). Default is "Pods".
