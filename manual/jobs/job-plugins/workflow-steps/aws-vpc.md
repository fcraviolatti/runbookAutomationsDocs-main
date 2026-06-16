---
title: "AWS VPC Workflow Steps"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-vpc.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS VPC Workflow Steps

> **Available in PagerDuty Runbook Automation Commercial products.**

AWS VPC (Virtual Private Cloud) is a service that contains AWS resources in a virtual network. Users define their own network topology, configure their own IP address range, and create subnets.

The following VPC plugins are available for PagerDuty Runbook Automation:

- [AWS VPC Workflow Steps](#aws-vpc-workflow-steps)
  - [Authentication](#authentication)
  - [Configure VPC Flow Logs](#configure-vpc-flow-logs)
  - [Enable VPC Network Peering](#enable-vpc-network-peering)

### Authentication

Follow the instructions outlined in the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html) for Runbook Automation to authenticate with AWS.

When defining the IAM Role for Runbook Automation, be sure to include the following permissions in the Policy associated with the role:

- **`ec2:CreateFlowLogs`** - Necessary for the ***Configure VPC Flow Logs*** plugin.
- **`ec2:CreateVpcPeeringConnection`** - Necessary for the ***Enable VPC Network Peering*** plugin.

Optionally authenticate within the Workflow Step itself by configuring the AWS Credentials.

### Configure VPC Flow Logs

The VPC Flow Log plugin provides a workflow step to create flow logs for VPC, Subnet, or Network Interface in AWS.

![VPC Flow Logs Plugin](https://docs.rundeck.com/docs/assets/img/vpc-flow-logs-plugin.png)  

The plugin requires the following fields:

- **Region**: AWS region to choose. Leave blank to set it at project (`project.aws.region`) or framework level (`aws.region`).
  - Example: `us-west-2`
- **Resource ID**: The ID of the subnet, network interface, or VPC for which you want to create a flow log.
  - Example: `subnet-12345678`
- **Resource Type**: Enter the resource type (VPC, Subnet, NetworkInterface).
  - Example: `VPC`
- **Traffic Type**: Enter the traffic type (Accept, Reject, All).
  - Example: `All`
- **Arn**: The ARN for the IAM role that permits Amazon EC2 to publish flow logs to a CloudWatch Logs log group in your account.
  - Example: `arn:aws:iam::123456789012:role/flow-log-role`
- **Log Group Name**: The name of a new or existing CloudWatch Logs log group where Amazon EC2 publishes your flow logs.
  - Example: `my-flow-logs`

### Enable VPC Network Peering

![VPC Network Peering Plugin](https://docs.rundeck.com/docs/assets/img/aws-vpc-peering-plugin.png)  

The **AWS / VPC / Enable Peering** plugin is a Node Step that enables VPC network peering between two VPCs in AWS. The plugin requires the following fields:

- **Region**: AWS region to choose. Leave blank to set it at project (`project.aws.region`) or framework level (`aws.region`).
  - Example: `us-west-2`
- **VPC ID**: Enter the VPC ID.
  - Example: `vpc-12345678`
- **Peer VPC ID**: Enter the Peer VPC ID.
  - Example: `vpc-87654321`
