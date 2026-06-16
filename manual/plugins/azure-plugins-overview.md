---
title: "Azure Plugins"
source_url: https://docs.rundeck.com/docs/manual/plugins/azure-plugins-overview.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Azure Plugins

## Overview

Runbook Automation integrates with Azure through a variety of plugins listed below. By integrating Runbook Automation with Azure, users can automate and provide self-service interfaces for operations of their infrastructure and applications. These integrations allow operations teams to provide self-service mechanisms to users throughout the business, as well as setup event-driven automation for workflows with Azure.

| Plugin Name                                                                                                                | Plugin Type    | Description                                                                  |
|----------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------------------------------------|
| [**Azure Node Source**](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/azure.html)                   | Node Source    | Retrieve Azure virtual machines for Node Inventory.                          |
| [**Delete Azure VM**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/azure.html#azure-node-delete)       | Node Step      | Delete an virtual machine.                                                   |
| [**Start Azure VM**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/azure.html#azure-node-start)         | Node Step      | Start (power on) an existing virtual machine.                                |
| [**Stop Azure VM**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/azure.html#azure-node-stop)           | Node Step      | Stop (power off) an existing virtual machine.                                |
| [**Restart Azure VM**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/azure.html#azure-node-restart)     | Node Step      | Restarts an existing virtual machine.                                        |
| [**Capture VM Snapshot**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/azure.html#azure-node-capture)  | Node Step      | Capture a snapshot of an existing virtual machine.                           |
| [**Storage Copy**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html#azure-storage-copy)     | Workflow Step  | Copy or get objects from Azure storage to/from Runbook Automation (Rundeck). |
| [**Storage Delete**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html#azure-storage-delete) | Workflow Step  | Delete blob storage from Azure storage container.                            |
| [**Storage List**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html#azure-storage-list)     | Workflow Step  | List blobs from Azure storage container.                                     |
| [**Create Azure VM**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html#azure-vm-create)     | Workflow Step  | Create a new Azure virtual machine.                                          |
| [**List Azure VMs**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html#azure-vm-list)        | Workflow Step  | List Azure virtual machines.                                                 |
| [**Start Azure VM**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html#azure-vm-start)       | Workflow Step  | Start (power on) an Azure virtual machines.                                  |
| [**Stop Azure VM**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html#azure-vm-stop)         | Workflow Step  | Stop (power off) an Azure virtual machines.                                  |
| [**Azure Log Storage**](https://docs.rundeck.com/docs/administration/cluster/logstore/azure.html)                          | Log Storage    | Send execution log files to Azure Storage Account.                           |
| [**VM Health Check**](https://docs.rundeck.com/docs/manual/healthcheckplugins/azure-healthcheck.html)                      | Health Check   | Check the status of Azure virtual machines.                                  |
| [**Azure Active Directory SSO**](https://docs.rundeck.com/docs/administration/security/sso/azure-sso.html)                 | Single Sign On | Use Azure Active Directory to authenticate users.                            |

  
*Click to expand to see the full list of Runbook Automation plugins for Azure.*

## Setup

### Create a New App Registration in Azure

Use the following steps to create and authorize an app in Azure to provide access to Runbook Automation plugins:

> **Tip**
>
> If you have already created an Azure AD application for Runbook Automation, skip to [Existing App Registration](#existing-app-registration).

1.  Sign in to the [Azure Portal](https://portal.azure.com/)

2.  Select ***Azure Active Directory***

3.  Click the **+ Add** dropdown and select **App Registration**![Add app reg](https://docs.rundeck.com/docs/assets/img/azure-add-app-reg.png)  
      

4.  On the **Register an application** page, provide a name for your application and then select **Accounts in this organizational directory only**.

5.  Click **Register**.

6.  On the **Overview** page, copy the **Application (client) ID** and the **Directory (tenant) ID** and save them to a secure location.

7.  Select **Certificates & secrets** and then select **New client secret**![New Client Secret](https://docs.rundeck.com/docs/assets/img/azure-new-client-secret.png)  
      

8.  On the **Add a client secret** panel, enter a **Description** and select an **Expires** value (in months). ![Client Secret Config](https://docs.rundeck.com/docs/assets/img/azure-client-secrets-config.png)  
      

9.  Click **Add**.

10. Copy the **Value** and **Secret ID** from the **Certificates & secrets** page and save them to a secure location.

    > **Heads Up!**
    >
    > Do not skip this step. These values will not be retrievable after you navigate away from this page. The **Value** is required when configuring the plugins in Runbook Automation.

11. Navigate to **Azure Services** \> **Subscriptions** and select the link for the **Subscription name**: ![Subscription ID](https://docs.rundeck.com/docs/assets/img/azure-subscription-id.png)

12. On the **Subscriptions** page, copy the **Subscription ID** and save it to a secure location.

13. Select **Access control (IAM)** and then select **Add** \> **Add role assignment**:

14. On the **Add role assignment** page, use the search field to find and select a **Role**. You must select at least a **Reader** role to continue.

15. Select **Next**.

16. On the **Members** tab, click **Select members**.

17. On the **Select members** panel, search for and select the App Registration (member) that you added in **Step 5**.

18. Review the information on the Members tab and then select Next.

19. Review the information on the Review + assign tab and then select Review + assign.

### Use Existing App Registration

**Tenant ID**: This is the ID for the trust relationship between the Azure subscription and Azure Active Directory.

1.  Sign in to the [Azure portal](https://portal.azure.com).
2.  Select *Azure Active Directory*.
3.  Select *Properties*.
4.  Then, scroll down to the *Tenant ID* field. Your *Tenant ID* will be in the box.

**Client ID**: This is also referred to as the *Application ID*

1.  Select *Azure Active Directory* in the left sidebar.
2.  Click *Enterprise Applications*.
3.  Click *All Applications*.
4.  Select the application which you have created.
5.  Click *Properties*.
6.  Copy the *Application ID* .

**Subscription ID**:

1.  Select *Subscriptions* in the left sidebar.
2.  Select whichever subscription is needed.
3.  Click on *Overview*.
4.  Copy the *Subscription ID*.

**Generating Azure Client Key**

1.  Sign in to the [Azure portal](https://portal.azure.com).
2.  Select *Azure Active Directory* in the left sidebar.
3.  Click *App Registrations*.
4.  Select the application which you have created.
5.  Click on *Certificates and Secrets*.
6.  Add a new *Client Secret*.
7.  Provide a memorable *Key Description* and choose an *Expiration*.
8.  Click *Add*.
9.  Copy and store the key value in a temporary location

> **Heads Up!**
>
> You won't be able to see this value again after you leave this page.

### Configure Azure Plugin Suite in Runbook Automation

Authentication for the Azure plugins can be configured for the entire system or for an individual project. Credentials can be optionally be overwritten on a per-plugin basis, such as an individual Job Step.

### Project Level Configuration

Use the following steps to configure authentication for the Azure plugins for a specific project:

1.  In the specific project, click on **Project Settings** in the lower left.
2.  Click on **Edit Configuration** then click on **Plugins**. ![Plugin Suite Project Settings](https://docs.rundeck.com/docs/assets/img/plugin-groups-project-settings.png)  
3.  Click on **+PluginGroup**.
4.  Select **Azure** from the list.
5.  Click **Select** next to the **Azure API Key** field.
6.  Click **+ Add or Upload a Keys**
7.  For the **Key Type** dropdown, choose the **Password** option.
8.  Enter the **Client Secret** value from **Step 10** above.
9.  Provide a **Name** for the secret and click **Save**.
10. Click **Save** to now use the saved secret from Key Storage.
11. Enter the **Tenant ID**, **Subscription ID** and **Client ID** from the prior sections into their associated fields: ![Azure Plugins Project](https://docs.rundeck.com/docs/assets/img/azure-plugingroup-project.png)
12. Click **Save** for the plugin configuration.
13. Click **Save** for the Project Settings.

### System Level Configuration

Use the following steps to configure authentication for the Azure plugins for the whole Runbook Automation system.

1.  Click on the **System Menu** (gear icon) in the upper right.
2.  Click on **System Configuration**.
3.  Navigate to the **Azure** section and click on the **Pencil Icon** in the upper right: ![Edit Plugin Suite Sysytem Level](https://docs.rundeck.com/docs/assets/img/azure-edit-plugingroup-system.png)
4.  Click **Select** next to the **Azure API Key** field.
5.  Click **+ Add or Upload a Keys**
6.  For the **Key Type** dropdown, choose the **Password** option.
7.  Enter the **Client Secret** value from **Step 10** above.
8.  Provide a **Name** for the secret and click **Save**.
9.  Click **Save** to now use the saved secret from Key Storage.
10. Enter the **Tenant ID**, **Subscription ID** and **Client ID** from the prior sections into their associated fields: ![Azure PluginGroup System](https://docs.rundeck.com/docs/assets/img/azure-plugingroup-system-config.png)
11. Click **Save** to commit these changes to the **System Configuration**.
