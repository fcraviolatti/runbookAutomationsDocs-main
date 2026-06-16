---
title: "Kubernetes Clusters - Run Command"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-run-command.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Kubernetes Clusters - Run Command

> **Available in PagerDuty Runbook Automation Commercial products.**

## Overview

This plugin executes a command in a specified pod within a Kubernetes cluster. Since this is a node-step plugin, multiple Kubernetes clusters or namespaces can be targeted within a single Job.

## Configuration

### Prerequisites

Before configuring the Kubernetes Object Logs plugin, the target clusters must be added to the Runbook Automation instance and the authentication method must be configured. This is done by following the steps outlined in the [Kubernetes Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

### Add Kubernetes Run Command Step

When building a Job, add the **Kubernetes / Clusters / Run Command** node step:

![Kubernetes Run Command](https://docs.rundeck.com/docs/assets/img/k8s-cluster-run-command.png)  

Configure the following fields:

- **Pod Name**: The name of the pod to execute the command in.
- **Namespace**: The namespace where the pod resides.
- **Command**: The command to execute in the pod.
- **Container**: (Optional) Specify a particular container within the pod to execute the command in.
- **Shell**: Specific shell to use for executing the command in the container. Default is `/bin/sh`.
