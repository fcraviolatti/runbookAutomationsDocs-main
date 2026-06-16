---
title: "Azure Node Steps (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/azure.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Azure Node Steps (Commercial)

## Getting Started

Follow the steps outlined in the [**Azure Plugins Overview**](https://docs.rundeck.com/docs/manual/plugins/azure-plugins-overview.html) to configure authentication for Azure Job steps. Credentials can be configured on a per Job Step basis, Project basis, or for the entire Runbook Automation system.

> **Rundeck OSS Installations**
>
> For Rundeck OSS installations, use the properties listed below to configure credentials at the Project or System levels.

**Client ID**  
The client ID for the application with access to the tenant to view VMs from.

- **Project setting**: `project.azure.clientId`
- **Framework Setting**: `azure.clientId`

**Tenant ID**  
The tenant (organization) in which the VMs live

- **Project setting**: `project.azure.tenantId`
- **Framework Setting**: `azure.tenantId`

**Subscription ID**  
The subscription ID for the application with access to the tenant to view VMs from.

- **Project setting**: `project.azure.subscriptionId`
- **Framework Setting**: `azure.subscriptionId`

**Azure Access Key**  
The access key for the Azure application that contains access to the proper VMs.

- **Project setting**: `project.azure.keyPath`
- **Framework Setting**: `azure.keyPath`

> **Tips**
>
> It is important to configure the azure resource model plugin before using these steps: [Azure Resource Model](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/azure.html#azure-enterprise)

### Azure / Node / Delete

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/azure-node-delete.png" alt="Azure - Delete Node" />
<figcaption aria-hidden="true">Azure - Delete Node</figcaption>
</figure>

- **Async** : Should be set to true if the vm should be deleted asynchronously.

> **Caution**
>
> Be very careful when using this step. It would be possible to remove a lot of instances by mistake if the node filter is too broad.

### Azure / Node / Start

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/azure-node-start.png" alt="Azure - Delete Node" />
<figcaption aria-hidden="true">Azure - Delete Node</figcaption>
</figure>

- **Async** : Should be set to true if the vm should be started asynchronously.

### Azure / Node / Stop

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/azure-node-stop.png" alt="Azure - Delete Node" />
<figcaption aria-hidden="true">Azure - Delete Node</figcaption>
</figure>

- **Async** : Should be set to true if the vm should be stopped asynchronously.

### Azure / Node / Restart

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/azure-node-restart.png" alt="Azure - Delete Node" />
<figcaption aria-hidden="true">Azure - Delete Node</figcaption>
</figure>

- **Async** : Should be set to true if the vm should be restart asynchronously.

### Azure / Node / Capture

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/azure-node-capture2.png" alt="Azure - Delete Node" />
<figcaption aria-hidden="true">Azure - Delete Node</figcaption>
</figure>

- **Async** : Should be set to true if the vm should be captured asynchronously.

- **containerName** : destination container name to store the captured VHD

- **vhdPrefix** : the prefix for the VHD holding captured image.

- **overwriteVhd** : whether to overwrites destination VHD if it exists. If set to true, it will be overwritten.
