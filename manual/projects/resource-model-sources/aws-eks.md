---
title: "AWS EKS Node Source"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/aws-eks.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS EKS Node Source

> **Available in PagerDuty Runbook Automation Commercial products.**

The AWS EKS (Elastic Kubernetes Service) Node Source can be used to dynamically retrieve EKS clusters and add them as nodes to the node inventory. As new clusters are created or removed, the inventory will be automatically updated.

## Configuration

### Prerequisites

Before configuring the AWS EKS Node Source, the following permissions must be added to the IAM Role associated with the Runbook Automation instance:

<div class="language-text line-numbers-mode">

``` text
eks:DescribeCluster
eks:ListClusters
```

</div>

For steps on how to associate an IAM Role with Runbook Automation (SaaS or Self-Hosted), refer to the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html).

### Add EKS Node Source

To configure the AWS EKS Node Source:

1.  In your project, go to "Project Settings" \> "Edit Nodes".  

2.  Click "Add a new Node Source".

3.  Select "AWS Kubernetes Clusters" from the list of available node sources: ![AWS EKS Node Source](https://docs.rundeck.com/docs/assets/img/aws-eks-node-source.png)

4.  **Region**: The AWS region or regions where your EKS clusters are located.

5.  **Use Pod Service Account for Node Steps**: Select this option if you intend to deploy the Enterprise Runner into these clusters and use the pod service account for authentication.

    > **Using Pod Service Account Through Runners**
    >
    > This option is useful when you want to dynamically discover clusters using the EKS integration, but have a 1:1 relationship between Runners and clusters or do not have the option to use the cloud provider for retrieving cluster credentials.
    >
    > For instructions on how to use the pod service account as well as more detail on the various cluster authentication methods, see the [Kubernetes Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

6.  **Assume Role ARN**: Optionally specify an IAM Role ARN to assume for retrieving EKS Clusters. This is useful when you want to target EKS Clusters across multiple AWS Accounts within a single Runbook Automation Project.

7.  Click "Save".

### Clusters in the Node Inventory

Each EKS cluster will be represented as a node with the following attributes:

- **`AWS-EKS:region`**: The AWS region of the cluster
- **`AWS-EKS:cluster-status`**: The status of the cluster
- **`AWS-EKS:cluster-version`**: The Kubernetes version of the cluster
- **`kubernetes-cluster-endpoint`**: The API server endpoint of the cluster
- **`kubernetes-use-pod-service-account`**: Whether to use pod service account for authentication
- **`kubernetes-cloud-provider`**: "aws-eks"

![EKS Node Attributes](https://docs.rundeck.com/docs/assets/img/eks-clusters-as-nodes.png)  

If tags are associated with the EKS clusters, they will be added as node attributes as well.

### Troubleshooting

#### Node Source Unauthorized Error

**Some Node Source returned an "Unauthorized" message**: This error indicates that the proper ACL permissions are not configured for the node sources within this project to access the necessary secrets within key storage:

![Unauthorized Error](https://docs.rundeck.com/docs/assets/img/node-source-unauthorized-error.png)  

To resolve this issue, add an ACL Policy that grants the necessary permissions to the node sources within this project to access the required secrets: Here is an example ACL Policy that grants the `platform-engineering` project access to the `keys/project/platform-engineering` directory within Key Storage:

<div class="language-yaml line-numbers-mode">

``` yaml
by:
  urn: project:platform-engineering
context: 
   application: rundeck
for:
  storage:
    - match: 
        path: 'keys/project/platform-engineering/.*'
      allow: [read] 
description: Allow access to key storage
```

</div>

#### AWS EKS Clusters Not Found

If the EKS Node Source does not return any clusters, ensure that the IAM Role associated with Runbook Automation has the necessary permissions to describe and list EKS clusters. The IAM Role should have the permissions outlined in the [Prerequisites](#prerequisites) section.
