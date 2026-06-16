---
title: "Azure AKS Node Source"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/azure-aks.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Azure AKS Node Source

> **Available in PagerDuty Runbook Automation Commercial products.**

The Azure AKS (Azure Kubernetes Service) Node Source can be used to dynamically retrieve AKS clusters and add them as nodes to the node inventory. As new clusters are created or removed, the inventory will be automatically updated.

## Configuration

### Prerequisites

Before configuring the Azure AKS Node Source, the following permissions must be added to the Azure Service Principal associated with the Runbook Automation instance:

<div class="language-text line-numbers-mode">

``` text
Microsoft.ContainerService/managedClusters/read
```

</div>

1.  Create a service principal and add the credential to Runbook Automation. If you have already created a service principal and added the credentials to Runbook Automation, skip to step 2. Otherwise, refer to the [Azure Plugins Overview](https://docs.rundeck.com/manual/plugins/azure-plugins-overview).  

2.  Navigate to either the **Subscription** or **Resource Group** where your Kubernetes clusters reside.

3.  Click on **Access Control (IAM)** -\> **Add** -\> **Add Role Assignment**: ![Add Role Assignment](https://docs.rundeck.com/docs/assets/img/azure-add-role-assignment.png)

4.  You can then use any of the Roles that have **`Microsoft.ContainerService/managedClusters/read`** as a permission.

    - There are many Built In Roles that Azure provides that has this permission, such as **Azure Kubernetes Service Cluster Monitoring User**.

5.  Select a role and then on the next screen click **+Select Members** and then select your App Registration (service principle) from the list: ![Select Members](https://docs.rundeck.com/docs/assets/img/azure-select-members.png)

6.  Click **Review + assign** and then **Save**.

### Add AKS Node Source in Runbook Automation

To configure the Azure AKS Node Source:

1.  In your project, go to "Project Settings" \> "Edit Nodes".  

2.  Click "Add a new Node Source".

3.  Select "Azure Kubernetes Clusters" from the list of available node sources.

4.  If credentials for the Azure service principal have already been added to the **Project** or **System Configuration** then adding them to this Node Source is optional. Adding them here will override the Project or System Configuration.

    - **Subscription**: The Azure Subscription ID. If not provided, the value from the Azure plugin group at the Project or System context will be used.
    - **Tenant ID**: The Azure Tenant ID. If not provided, the value from the Azure plugin group at the Project or System context will be used.
    - **Client ID**: The path to the Key Storage entry for the Azure Client ID. If not provided, the Client ID value from the Azure plugin group at the Project or System context will be used. If an "Unauthorized" error occurs, ensure that the proper policy is added to ACLs.
    - **Azure Client Secret**: The path to the Key Storage entry for the Client Secret. If not provided, the value from the Azure plugin group at the Project or System context will be used. If an "Unauthorized" error occurs, ensure that the proper policy is added to ACLs.

5.  **Resource Group**: Optionally filter the clusters listed from a specific Resource Group.

6.  **Use Pod Service Account for Node Steps**: Choose whether to authenticate with the Pod Service Account for Job steps.

    > **Using Pod Service Account Through Runners**
    >
    > This option is useful when you want to dynamically discover clusters using the AKS integration, but have a 1:1 relationship between Runners and clusters or do not have the option to use the cloud provider for retrieving cluster credentials.
    >
    > For instructions on how to use the pod service account as well as more detail on the various cluster authentication methods, see the [Kubernetes Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

7.  Click **Save**.

### Clusters in the Node Inventory

Each AKS cluster will be represented as a node within the node inventory:

![AKS Node Attributes](https://docs.rundeck.com/docs/assets/img/ask-clusters-as-nodes.png)  

By default, the following attributes will be added to each node:

- **`Azure-Kubernetes:resource-group`**: The Azure Resource Group where the cluster resides.
- **`Azure-Kubernetes:region`**: The Azure region where the cluster is located.
- **`Azure-Kubernetes:power-state`**: The power-state of the cluster.
- **`Azure-Kubernetes:node-resource-group`**: The Azure Resource Group where the nodes reside.
- **`Azure-Kubernetes:cluster-id`**: The Azure Cluster ID.
- **`kubernetes-cloud-provider`**: The cloud provider, which will be "azure-kubernetes".

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

#### Azure AKS Clusters Not Found

If the Azure AKS Node Source does not return any clusters, ensure that the Azure Service Principal has the necessary permissions to read the AKS clusters. The Service Principal must have the **`Microsoft.ContainerService/managedClusters/read`** permission.
