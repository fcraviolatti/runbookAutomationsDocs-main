---
title: "GCP GKE Resource Model Source"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/gcp-gke.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# GCP GKE Resource Model Source

> **Available in PagerDuty Runbook Automation Commercial products.**

The GCP GKE (Google Kubernetes Engine) Node Source can be used to dynamically retrieve GKE clusters and add them as nodes to the node inventory. As new clusters are created or removed, the inventory will be automatically updated with clusters represented as nodes.

## Configuration

### Prerequisites

Before configuring the GCP GKE Node Source, permissions must be allowed for the service account associated with Runbook Automation to list the GKE clusters.

See the [Google Cloud Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/gcp-plugins-overview.html) for steps on how to associate a service account with Runbook Automation.

A predefined role such as **Kubernetes Engine Cluster Viewer** can be used to grant the necessary permissions. This role has the following permissions:

- `container.clusters.get`
- `container.clusters.list`
- `resourcemanager.projects.get`
- `resourcemanager.projects.list`

![GCP GKE Node Source](https://docs.rundeck.com/docs/assets/img/gke-cluster-viewer-role.png)  

### Add GKE Node Source in Runbook Automation

To configure the GCP GKE Node Source plugin:

1.  In your project, go to "Project Settings" \> "Edit Nodes".  

2.  Click "Add a new Node Source".

3.  Select "GCP Kubernetes Engine Clusters" from the list of available node sources.

4.  Configure the following settings:

    - **Project ID**: The GCP Project ID to use for accessing the GKE clusters.
    - **Region or Zone**: The GCP region or zone where your GKE clusters are located. You can use `-` to include all regions or zones.
    - **Access Key Path**: The Key Storage path for the GCP Access Key credentials.
      - **GCP Authentication at Project or System Level**
        >
        > Authentication for GCP plugins can be configured at the Project or System levels by following the [Google Cloud Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/gcp-plugins-overview.html). If the GCP authentication is already set in the Project or System Configuration, this field can be left blank.

5.  **Use Pod Service Account for Node Steps**: Choose whether to authenticate with the Pod Service Account for Job steps. Set to `True` if Runbook Automation or a Runner is executing within the targeted cluster.

    > **Using Pod Service Account Through Runners**
    >
    > This option is useful when you want to dynamically discover clusters using the GKE integration, but have a 1:1 relationship between Runners and clusters or do not have the option to use the cloud provider for retrieving cluster credentials.
    >
    > For instructions on how to use the pod service account as well as more detail on the various cluster authentication methods, see the [Kubernetes Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

### Node Attributes

Each GKE cluster will be represented as a node with the following attributes:

- `gcp-location`: The GCP region/zone of the cluster
- `kubernetes-cluster-endpoint`: The API server endpoint of the cluster
- `kubernetes-cloud-provider`: Set to **"gcp-gke"**

![GKE Node Attributes](https://docs.rundeck.com/docs/assets/img/gke-cluster-as-node.png)  

### Troubleshooting

#### Node Source Unauthorized Error

**Some Node Source returned an "Unauthorized" message**: This error indicates that the proper ACL permissions are not configured for the node sources within this project to access the necessary secrets within key storage:

![Unauthorized Error](https://docs.rundeck.com/docs/assets/img/gke-node-source-unauthorized-error.png)  

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

#### GKE Clusters Not Found

If the GKE clusters have not been added to the node inventory, verify the following:

1.  Verify your GCP credentials and permissions:
    - Ensure the service account has the necessary GKE permissions
    - Verify the credentials file is properly stored in Key Storage
2.  Ensure your GKE cluster is running and accessible.
3.  Verify the correct Project ID and Region/Zone settings.
4.  If running the Self-Hosted solution, check the Runbook Automation logs for any error messages.

### Additional Resources

For more detailed information, refer to:

- [Google Kubernetes Engine documentation](https://cloud.google.com/kubernetes-engine/docs)
- [GCP IAM documentation](https://cloud.google.com/iam/docs)
