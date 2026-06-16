---
title: "Kubernetes Clusters - List Objects"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-list-objects.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Kubernetes Clusters - List Objects

> **Available in PagerDuty Runbook Automation Commercial products.**

## Overview

This plugin lists objects of a selected kind within a Kubernetes cluster. Since this is a node-step plugin, multiple Kubernetes clusters or namespaces can be targeted within a single Job.

The types of objects that can be listed within a Kubernetes cluster include:

- **ConfigMaps**
- **Cron Jobs**
- **Custom Resource Definitions**
- **DaemonSets**
- **Deployments**
- **Ingresses**
- **Jobs**
- **Namespaces**
- **Nodes**
- **Persistent Volumes**
- **Persistent Volume Claims**
- **Pods**
- **Pod Disruption Budgets**
- **ReplicaSets**
- **Secrets**
- **Services**
- **StatefulSets**
- **Storage Classes**

## Configuration

### Prerequisites

Before configuring the Kubernetes List Objects plugin, the target clusters must be added to the Runbook Automation instance and the authentication method must be configured. This is done by following the steps outlined in the [Kubernetes Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

### Add Kubernetes List Objects Step

When building a Job, add the **Kubernetes / Clusters / List Objects** node step:

![Kubernetes List Objects](https://docs.rundeck.com/docs/assets/img/k8s-clusters-list-objects.png)  

Configure the following fields:

- **Object Type**: Select the type of object to list (e.g., Pods, ConfigMaps, Deployments).
- **Namespace**: The namespace to list objects from. Default is `default`.
- **All Namespaces**: If selected, retrieve objects from across all namespaces. The 'Namespace' field will be ignored.
- **Label Selector**: Filter objects based on labels. Supports equality-based and set-based selectors.
  - - For detailed information on field selectors, refer to the [Kubernetes documentation on field selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/field-selectors/).
- **Field Selector**: Filter objects based on fields. Supports equality-based and set-based selectors.
  - For detailed information on label selectors, refer to the [Kubernetes documentation on label selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#label-selectors).
- **Output Format**: Choose the format for the output (Simple List, JSON, or YAML).

### Invocation Output

The output of the step will be the objects that were listed in the Kubernetes cluster. The output format will be the same as the format selected in the step configuration:

![Kubernetes List Objects Output](https://docs.rundeck.com/docs/assets/img/k8s-clusters-list-objects-output.png)
