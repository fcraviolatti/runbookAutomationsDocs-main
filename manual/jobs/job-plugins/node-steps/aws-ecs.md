---
title: "AWS Elastic Container Service (ECS) Node Steps"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/aws-ecs.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS Elastic Container Service (ECS) Node Steps

> **Available in PagerDuty Runbook Automation Commercial products.**

Amazon ECS is a fully managed container orchestration service that makes it easy for you to deploy, manage, and scale containerized applications.

The following plugins are available for PagerDuty Runbook Automation:

- [**ECS Stop Task (AWS / ECS/ Stop / Task)**](#ecs-stop-task)

### Authentication

Follow the instructions outlined in the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html) for Runbook Automation to authenticate with AWS.

When defining the IAM Role for Runbook Automation, be sure to include the permissions required by the specific plugins in the Policy associated with the role:

- **Stop ECS Task**:
  - `ecs:StopTask`

### Pre-requisites

This plugin operates on ECS Tasks that are present in the Node Inventory through the [ECS Node Source Plugin](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/ecs-fargate.html).

Be sure to configure that plugin to populate the Node Inventory with ECS Tasks prior to executing this plugin.

### ECS Stop Task

The **AWS / ECS / Stop Task** plugin stops a running ECS Task. This plugin is useful for stopping tasks that are no longer needed or are causing issues.

Because this plugin operates against ECS Tasks in the Node Inventory, there is very little configuration required to use it.

The plugin will stop the ECS Task on the specified cluster and service.

Optionally define the AWS connection credentials to use for the plugin. All other configuration is handled by the [ECS Node Source Plugin](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/ecs-fargate.html).
