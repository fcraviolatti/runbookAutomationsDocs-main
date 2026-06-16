---
title: "AWS ELB Workflow Steps"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-elb-workflow-plugin.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS ELB Workflow Steps

> **Available in PagerDuty Runbook Automation Commercial products.**

Elastic Load Balancing (ELB) is an AWS service that automatically distributes incoming application traffic across multiple targets and virtual appliances in one or more Availability Zones (AZs).

The following ELB plugins are available for PagerDuty Runbook Automation:

- [Target Group Instance Statuses](#target-group-instance-statuses)

### Authentication

Follow the instructions outlined in the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html) for Runbook Automation to authenticate with AWS.

When defining the IAM Role for Runbook Automation, be sure to include the following permissions in the Policy associated with the role:

- **`loadBalancing:describeLoadBalancers`**
- **`loadBalancing:describeTargetGroups`**
- **`loadBalancing:describeTargetHealth`**

### Target Group Instance Statuses

The **AWS / ELB / Target Unhealthy** plugin is a Workflow Step that checks to see if any instances within the Target Groups of a particular ELB are reporting *unhealthy*:

![ELB Status Plugin](https://docs.rundeck.com/docs/assets/img/aws-elb-status-check-plugin.png)  

Identifying unhealthy instances for a given load balancer can be a challenge because there can be multiple target-groups associated with a given load balancer, and multiple instances associated within a Target Group. This plugin checks all instances for all Target Groups "within" a given ELB and returns any that are "unhealthy."

#### Plugin Field Descriptions

- **Target Load Balancer**: The name of the Elastic Load Balancer (ELB) that routes traffic to the Target Group instances.
- **Target Load Balancer Region**: The AWS region where the ELB resides.

### See it in Action

This plugin is used in one of the prebuilt Jobs in our [***Automated Diagnostics Solution***](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/). Try out the Solution to see how this plugin can be used as part of incident-response workflows.
