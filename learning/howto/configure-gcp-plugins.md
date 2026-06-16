---
title: "Integrate with Google Cloud Using the Welcome Project"
source_url: https://docs.rundeck.com/docs/learning/howto/configure-gcp-plugins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Integrate with Google Cloud Using the Welcome Project

Google Cloud consists of a set of physical assets, such as computers and hard disk drives, and virtual resources, such as virtual machines (VMs), that are contained in Google's data centers around the globe.

[Read more about Google Cloud here.](https://cloud.google.com/docs/overview)

This How To will highlight some of the key steps to configuring the Google Cloud plugins included in our Runbook Automation version. The background for these steps is covered in detail on Google's support site here: [Creating and Managing Service Account Keys](https://cloud.google.com/iam/docs/creating-managing-service-account-keys).

## Pre-Requisites

This How To is based on the Runbook Automation [Welcome Projects](https://docs.rundeck.com/docs/learning/howto/welcome-project-starter.html).

- Rundeck Welcome Project version 1.5  
  *(Runbook Automation 3.4.4 is min product version)*
- Administrative access to a Google Cloud environment
- Create at least one [Virtual Machine Instance](https://cloud.google.com/compute/docs/instances) and note which *Zone* it is created in.

### Authentication & Configuration

Follow the steps outlined in the [**Google Cloud Integration Overview**](https://docs.rundeck.com/manual/plugins/gcp-plugins-overview) doc to configure credentials for the GCP plugins. Credentials can be configured on a per Project basis or for the entire Runbook Automation system.

## Configuring Runbook Automation

1\. Upload Key

2\. Configuring Node Source

3\. Configure Settings for Job Steps

1\. Upload Key

1.  Login to Rundeck as `admin`.
2.  Open the **Welcome to Rundeck** project entry.
3.  Open the **Key Storage** entry from the *Project Settings* menu.
4.  Select the `gcp-access-key.json` and click **Overwrite Key**.
5.  In the dropdown select **Upload File** and choose the JSON file from the earlier steps.
6.  Click **Save**

2\. Configuring Node Source

1.  Open the **Welcome to Rundeck** project.
2.  Open **Project Settings** \> **Edit Nodes**.
3.  Click on the *Sources* tab.
4.  Click **Edit** on the *GCP Cloud / Resource Model*
5.  Enter the **Project ID** from your GCP Project. ![GCP Project ID](https://docs.rundeck.com/docs/assets/img/howto-gcp-projectid.png)  
      
6.  Select the **Zone** where this Node Source will gather a list of Compute VMs from.
7.  Leave the **Key Path** set to `keys/project/welcome-project/gcp-access-key.json`

3\. Configure Settings for Job Steps

1.  Open **System Menu** (gear icon) \> **System Configuration**.
2.  Using the filter at the top enter `gcp` to list just the GCP Plugin Configurations.
3.  Leave the **GCP Access Key Path** entry as `keys/project/welcome-project/gcp-access-key.json`.
4.  Gather the **Project ID** from your GCP Project. ![GCP Project ID](https://docs.rundeck.com/docs/assets/img/howto-gcp-projectid.png)  
      
5.  Enter a Zone that can be used by default. Job Steps can override the zone at each step or dynamically per node on Node Steps.
6.  Click **Save**

### Confirming GCP Plugins are working

#### Nodes

1.  Navigate to the **Nodes** section in the *Welcome to Rundeck* project.
2.  Search for nodes using `tags: gcpcompute`.  
    If your Node Source is configured correctly and there are VMs in the configured zone they will be listed in the Nodes list.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/howto-gcp-gcpnodes.png" alt="GCP Nodes" />
<figcaption aria-hidden="true">GCP Nodes</figcaption>
</figure>

#### Job Steps

After confirming Nodes are being listed choose one that can safely be restarted. **Choose wisely**

1.  Navigate to the **Jobs** section in the *Welcome to Rundeck* project.
2.  Open *Cloud Services* \> *GCP* \> *Node Steps* \> *VM* and choose **Restart VM Instance**.
3.  Select the node to be restarted and click **Run Job Now**.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/howto-gcp-restartnode.png" alt="Restart GCP Node" />
<figcaption aria-hidden="true">Restart GCP Node</figcaption>
</figure>

## More Information

- [Information about Zones in GCP](https://cloud.google.com/compute/docs/regions-zones)
