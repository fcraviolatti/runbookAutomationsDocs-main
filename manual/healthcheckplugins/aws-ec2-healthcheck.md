---
title: "AWS EC2 Health Check"
source_url: https://docs.rundeck.com/docs/manual/healthcheckplugins/aws-ec2-healthcheck.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS EC2 Health Check

The AWS EC2 Health Check can provide health status updates based on whether the EC2 instance is running or not.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/healthcheck-aws-ec2.png" alt="AWS EC2 Health Check" />
<figcaption aria-hidden="true">AWS EC2 Health Check</figcaption>
</figure>

- **Node Filter:** This is the node filter that determines which nodes to run this health Check against. The default is `tags: EC2`. An `EC2` tag is applied automatically by the AWS EC2 Node Source.

  > If the Project is using more than one EC2 Node Source for multiple regions it would be important to add the region to the Node Filter to the region this Node Filter is targeting.

- **Label**: A user friendly label for the Health Check

- **Access Key ID**: AWS Access Key ID associated with access to these EC2 instances.

- **Secret Key Path**: Path in the Key Storage where the AWS Secret Key is stored.

- **Region**: The AWS Region where these nodes are running.
