---
title: "Amazon Web Services (AWS) Node Steps"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/aws.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Amazon Web Services (AWS) Node Steps

[Amazon's EC2](https://aws.amazon.com/ec2/) (Elastic Cloud Compute) provides scalable, on-demand cloud computing capacity that forms the backbone of many modern infrastructure deployments. These Rundeck Node Steps enable automated management of your EC2 resources, allowing you to programmatically control instance life-cycles while maintaining operational consistency and reducing manual intervention.

> **Tips**
>
> For optimal workflow efficiency, implement the AWS EC2 resource model plugin, which enhances these Node Step plugins. Follow the setup guide here: [AWS EC2 Resource Model](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/aws.html)

## Authentication

Follow the instructions outlined in the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html) for Runbook Automation to authenticate with AWS.

When defining the IAM Role for Runbook Automation, be sure to include the following permissions in the Policy associated with the role:

`ec2:StartInstances``ec2:StopInstances``ec2:terminateInstances``ec2:runInstances``ec2:createSnapshot``Networking and Monitoring:`

**Region**  
Specify the region for the node. If using the EC2 Node Source it's possible to use `${node.region}` and the region will be dynamically populated with the region for that node. (recommended) The value can also be set a a higher scope using the settings below.

- **Project setting**: project.aws.region
- **Configuration Management**/**Framework Setting**: aws.region

## EC2 VM Node Steps (Enterprise Only)

### AWS / VM / Start

This step initiates and boots up a specified EC2 instance, bringing it online and ready for use. This is crucial for businesses that need to dynamically scale their computing resources during peak hours or need to start pre-configured instances for specific workloads

### AWS / VM / Stop

This step safely shuts down a specified EC2 instance, ensuring all processes are properly terminated. This capability is essential for cost optimization by stopping unused instances during off-hours and managing resource utilization effectively.

### AWS / VM / Restart

This step performs a graceful reboot of a specified EC2 instance, which is equivalent to an operating system reboot command rather than a power cycle. This operation is crucial for applying system updates or resolving performance issues while maintaining instance data and configuration, making it a safer option than a stop/start cycle since it preserves the instance's attributes and network settings.

### AWS / VM / Delete

This step permanently terminates and removes an EC2 instance from your AWS environment, freeing up associated resources. This is important for cleaning up unused resources to reduce costs and maintain a clean infrastructure, though it should be used with extreme caution as the action is irreversible.

> **Caution**
>
> Be very careful when using this step. It would be possible to remove a lot of instances by mistake if the node filter is too broad.
