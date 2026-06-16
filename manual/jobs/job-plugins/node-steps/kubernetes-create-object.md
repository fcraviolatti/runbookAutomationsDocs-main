---
title: "Kubernetes Clusters - Create Object"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-create-object.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Kubernetes Clusters - Create Object

> **Available in PagerDuty Runbook Automation Commercial products.**

## Overview

This plugin creates an object of a selected kind within a Kubernetes cluster. Since this is a node-step plugin, multiple Kubernetes clusters or namespaces can be targeted within a single Job.

The types of objects that can be created within a Kubernetes cluster include:

- **ConfigMaps**
- **DaemonSets**
- **Deployments**
- **Jobs**
- **Namespaces**
- **Pods**
- **ReplicaSets**
- **Secrets**
- **Services**
- **StatefulSets**

## Configuration

### Prerequisites

Before configuring the Kubernetes Create Object plugin, the target clusters must be added to the Runbook Automation instance and the authentication method must be configured. This is done by following the steps outlined in the [Kubernetes Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

### Add Kubernetes Create Object Step

When building a Job, add the **Kubernetes / Clusters / Create Object** node step:

![Kubernetes Create Object](https://docs.rundeck.com/docs/assets/img/k8s-clusters-create-object.png)  

- **Object Type**: Select the type of object to create (Pods, ConfigMaps, Deployments, etc.)
- **YAML Definition**: The YAML definition of the object to be created. This can be a data-variable that is passed from a prior step - such as a YAML definition that is retrieved from a git repository.
- **Namespace**: The namespace where the object will be created. Default is `default`.
- **Output Format**: Choose the format for the output (JSON or YAML). Default is JSON.

### Invocation Output

The output of the step will be the object that was created in the Kubernetes cluster. The output format will be the same as the format selected in the step configuration:

![Kubernetes Create Object Output](https://docs.rundeck.com/docs/assets/img/k8s-create-object-output.png)
