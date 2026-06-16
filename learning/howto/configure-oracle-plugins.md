---
title: "Configure Oracle Cloud Infrastructure Plugins"
source_url: https://docs.rundeck.com/docs/learning/howto/configure-oracle-plugins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Configure Oracle Cloud Infrastructure Plugins

Oracle Cloud Infrastructure (OCI) is a deep and broad platform of public cloud services that enables customers to build and run a wide range of applications in a scalable, secure, highly available, and high-performance environment.  
*-Oracle Website*

[Read more about Oracle Cloud here.](https://www.oracle.com/cloud/)

This How To will highlight some of the key steps to configuring the Oracle Cloud plugins included in our Runbook Automation version. The background for these steps is covered in detail on Oracle's support site here: [Launching your first Linux Instance](https://docs.oracle.com/en-us/iaas/Content/GSG/Reference/overviewworkflow.htm#Tutorial__Launching_Your_First_Linux_Instance)

> Note: These instructions are based on the Welcome Project and provide an example of how to use the plugins in the easiest way. For full documentation and implementation please refer to the User Manual.

## Pre-Requisites

This How To is based on the Runbook Automation [Welcome Projects](https://docs.rundeck.com/docs/learning/howto/welcome-project-starter.html).

- Rundeck Welcome Project version 1.5  
  *(Runbook Automation 3.4.4 is min product version)*
- Administrative access to an Oracle Cloud environment
- Create at least one [Virtual Machine Instance](https://docs.oracle.com/en-us/iaas/Content/Compute/Tasks/launchinginstance.htm) and note which *Zone* it is created in.

## Creating Service Account Keys

1.  Login to your Oracle Cloud Console at [oracle.com/cloud/sign-in.html](https://docs.rundeck.com/docs/learning/howto/oracle.com/cloud/sign-in.html).
2.  Navigate to your User Profile by clicking on the icon in the upper right and selecting `User Settings`[Oracle User Profile Menu](https://docs.rundeck.com/assets/img/howto-oracle-usermenu.png)
3.  Choose *API Keys* from the menu.
4.  Click **Add API Key**.
5.  Select **Generate API Key Pair** and **Download the Private Key** prior to clicking the *Add* button.
6.  Copy and Paste the *Configuration File Preview* content somewhere for use in future steps.

## Configuring Rundeck

1\. Upload Key

2\. Configure Node Source

3\. Configure Settings for Job Steps

4\. Configure Health Check

1\. Upload Key

1.  Login to Rundeck as `admin`.
2.  Open the **Welcome to Rundeck** project entry.
3.  Open the **Key Storage** entry from the *Project Settings* menu.
4.  Select the `oracle-key.pem` and click **Overwrite Key**.
5.  In the dropdown select **Upload File** and choose the `oracle-key.pem` file from the earlier steps.
6.  Click **Save**

2\. Configure Node Source

1.  Open the **Welcome to Rundeck** project.
2.  Open **Project Settings** \> **Edit Nodes**.
3.  Click on the *Sources* tab.
4.  Click **Edit** on the *Oracle Cloud / Resource Model*
5.  Enter the **Tenant ID**
6.  Enter the **User ID**
7.  Enter the **Fingerprint**
8.  Enter the Region value where your nodes will be gathered from.

3\. Configure Settings for Job Steps

1.  Open **System Menu** (gear icon) \> **System Configuration**.
2.  Using the filter at the top enter `oracle` to list only the Oracle Plugin Configurations.
3.  Enter the **Tenant ID**
4.  Enter the **User ID**
5.  Enter the **Fingerprint**
6.  Enter a Zone that can be used by default. Job Steps can override the zone at each step or dynamically per node on Node Steps.
7.  Click **Save**

4\. Configure Health Check

1.  Open the **Welcome to Rundeck** project.
2.  Click on **Health Checks**
3.  Click on **Configure**
4.  Click on **Edit** on the *Oracle Cloud / Instance Healthcheck Plugin*
5.  Enter the **Tenant ID**
6.  Enter the **User ID**
7.  Enter the **Fingerprint**
8.  Enter the Region value where your nodes are gathered from.

### Confirming oracle Plugins are working

#### Nodes

1.  Navigate to the **Nodes** section in the *Welcome to Rundeck* project.
2.  Search for nodes using `tags: OracleVM`.  
    If your Node Source is configured correctly and there are VMs in the configured zone they will be listed in the Nodes list.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/howto-oracle-oraclenodes.png" alt="Oracle Nodes" />
<figcaption aria-hidden="true">Oracle Nodes</figcaption>
</figure>

#### Job Steps

After confirming Nodes are being listed choose one that can safely be restarted. **Choose wisely**

1.  Navigate to the **Jobs** section in the *Welcome to Rundeck* project.
2.  Open *Cloud Services* \> *Oracle Cloud* \> *Node Steps* \> and choose **Restart Instance**.
3.  Select the node to be restarted and click **Run Job Now**.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/howto-oracle-restartnode.png" alt="Restart Oracle Node" />
<figcaption aria-hidden="true">Restart Oracle Node</figcaption>
</figure>

## More Information

- [Oracle Node Step Plugins](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/oracle.html)
- [Oracle Workflow Step Plugins](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/oracle.html)
- [Oracle Node Source Plugin](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/oracle.html)
