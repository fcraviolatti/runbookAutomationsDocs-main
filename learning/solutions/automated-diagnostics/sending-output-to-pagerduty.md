---
title: "Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/sending-output-to-pagerduty.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

## Sending Automation Output to PagerDuty Incidents

### Introduction

By default, your automated diagnostics jobs will display their results in logging visible in the Automation interface. There are a few extra steps necessary to transport those logs or some subset over to your PagerDuty incidents. This section will walk you through steps to simplify output in a job and send it to a PagerDuty incident. These steps assume that you have already completed **Tour 4: Send Diagnostic Data to PagerDuty**, which ensures that you have connected your Automation interface to your PagerDuty instance at the infrastructure level.

### Example

To carry out these steps, youâ€™ll need a job that we can modify for our purposes. Since most of the jobs in this Solution already have these steps completed, weâ€™ll start with a fresh job which you can import and work with. You can copy the job definition at the [bottom of the page](#job-definition).

1.  In the Jobs section of your project, click **New Job**![](https://docs.rundeck.com/docs/assets/img/sending1.png)  
      
2.  Click **Upload Definition**![](https://docs.rundeck.com/docs/assets/img/sending2.png)  
      
3.  Click **Choose File** to select the downloaded file ![](https://docs.rundeck.com/docs/assets/img/sending3.png)  
      
4.  Select **YAML format**
5.  Click **Upload**
6.  Edit your job using the **Actions** menu at the far right of the jobs list. ![](https://docs.rundeck.com/docs/assets/img/sending16.png)

#### Add an option for Incident ID

1.  Click **Workflow** at the top of the Job Edit page
2.  Toward the top of the Workflow section, click **Add an option**.  
    ![](https://docs.rundeck.com/docs/assets/img/sending5.png)
3.  Enter an **Option Name** and **Option Label** as specified in the screenshot. ![](https://docs.rundeck.com/docs/assets/img/sending6.png)
4.  Click **Save** for this option

#### Add a log filter to your job step

1.  Using the **gear icon** at the right of the job step, click **Add Log Filter**![](https://docs.rundeck.com/docs/assets/img/sending8.png)
2.  Choose **Progress Badge** from the available filters  
    ![](https://docs.rundeck.com/docs/assets/img/sending9.png)

#### Setting your Filter

1.  Set the following fields:  
    **Regex:** `.*Active: active.*`  
    **Text:** Healthy  
    **Status Symbol:** Select the Green Checkmark  
    **Context Variable:** ssh-status  
    ![](https://docs.rundeck.com/docs/assets/img/sending10.png)  
      
2.  **Save** your filter. You should see the log filter visually now as part of your job step. ![](https://docs.rundeck.com/docs/assets/img/sending11.png)  
      
3.  Click the **+Add** button to add another Progress Badge filter
4.  Set the following fields:  
    **Regex:**`!.*Active: active.*`  
    **Text:** Unhealthy  
    **Status Symbol:** Select the Red X  
    **Context Variable:** ssh-status  
    ![](https://docs.rundeck.com/docs/assets/img/sending12.png)

#### Add an Incident Note job step

1.  On the **Edit Job** page, click **Add a step**.  
    ![](https://docs.rundeck.com/docs/assets/img/sending13.png)  
      
2.  Under **Workflow Steps**, search for and select **PagerDuty Incident Note**  
    ![](https://docs.rundeck.com/docs/assets/img/sending14.png)

#### Configure the Incident Note job step

1.  Enter or select a PagerDuty **API Key**  
    If in keystore, use **Select** button. Otherwise, you can paste the API Key in this field
2.  Enter an **Email** to be used for incident updates. If youâ€™ve established a project variable, you can use that as specified in screenshot
3.  Update the **Incident ID** field as specified in screenshot to use the *pd_incident_id* variable
4.  Update the **Note** field to include variable reference (`${data.variablename}`) as shown in screenshot.
    <div class="language-text line-numbers-mode">

    ``` text
    SSH Status: ${data.ssh-status*}\n\nClick here for detailed diagnostics: ${job.url}#output
    ```

    </div>

    This note will show the resulting progress badge as well as a link to the full log
5.  Set a **Step Label** to identify what this job step does
6.  Save the job step and job to save your changes  
    ![](https://docs.rundeck.com/docs/assets/img/sending15.png)

### Job Definition

Copy and paste this content into a file and import to your project.

yaml

yaml

<div class="language-yaml line-numbers-mode">

``` yaml
- defaultTab: nodes
  description: ''
  executionEnabled: true
  group: Administration/Linux
  id: e4b9f6db-efda-43a4-8f10-52eba1b6c56d
  loglevel: INFO
  name: SSH Status
  nodeFilterEditable: true
  nodefilters:
    dispatch:
      excludePrecedence: true
      keepgoing: false
      rankOrder: ascending
      successOnEmptyNodeFilter: false
      threadcount: '1'
    filter: 'name: employees_mysql_db_1 '
  nodesSelectedByDefault: true
  plugins:
    ExecutionLifecycle: {}
  scheduleEnabled: true
  schedules: []
  sequence:
    commands:
    - description: Check status of SSH service
      exec: sudo systemctl status ssh
    keepgoing: false
    strategy: node-first
  uuid: e4b9f6db-efda-43a4-8f10-52eba1b6c56d
```

</div>
