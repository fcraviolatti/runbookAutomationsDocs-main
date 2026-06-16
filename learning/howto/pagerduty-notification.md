---
title: "Configure Notifications using PagerDuty Plugin"
source_url: https://docs.rundeck.com/docs/learning/howto/pagerduty-notification.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Configure Notifications using PagerDuty Plugin

Rundeck integrates with PagerDutyâ€™s incident management platform, which provides notifications, automatic escalations, on-call scheduling, and other functionality to help teams detect and fix problems quickly.

In this guide we will show you how to trigger an event in PagerDuty after executing a job in Rundeck. This functionality is available in both Rundeck Community and Enterprise.

> **Tips**
>
> Note, there are many more [PagerDuty plugins](https://docs.rundeck.com/docs/manual/webhooks/pagerduty-run-job.html) available for Runbook Automation users

Rundeck Notifications are actions triggered based on the result of a Job that was executed. There are five conditions that can trigger Rundeck notifications, those conditions are:

- `onstart` - Triggers an action when the Job **started**
- `onsuccess` - Triggers an action when the Job **completed without any errors**
- `onfailure` - Triggers an action when the Job **failed or was aborted**
- `onavgduration` - Triggers an action when the execution **exceeds the average duration of the Job.**
- `onretryablefailure` - Triggers an action when the Job **failed after a retry.**

The [Rundeck PagerDuty Notification Plugin](https://github.com/rundeck-plugins/pagerduty-notification) lets you send trigger events to your PagerDuty service. This plugin is available for the Community version and bundled with the Enterprise version of Rundeck.

## Installing the plugin

Community Install

Enterprise Install

Community Install

1.  Go to Gear Icon (upper right) \> Plugins \> Find plugins.  
      
    ![Find Plugins](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-findplugin.png)  
      
2.  On the Plugin Repository search, type "pagerduty" and enter.
3.  On the PagerDuty Notification block press the "Install" button.  
      
    ![alt_text](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-installplugin.png)  
      
4.  After a few seconds the plugins are installed on your Rundeck Instance.

Enterprise Install

The PagerDuty Notification plugin is bundled with Enterprise builds. No need to install separately.

## Configuring PagerDuty

> (Same Steps for Community and Enterprise)

A fundamental requirement is the PagerDuty integration key, which connects the Rundeck integration with a PagerDuty Service. To locate and copy it follow these steps:

1.  Log in to PagerDuty.
2.  Go to the Services menu click the button to create a New Service.
3.  Give the Service a name and assign it to an escalation policy. Add an integration by selecting the Events API V2, as seen below:  
      
    ![Create Service](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-createservice.png)  
      
4.  When the Service is created youâ€™ll be shown the Integrations tab. Inside that tab copy the value for the Integration Key and save it for later on in your setup.  
      
    ![Integration Key](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-integrationkey.png)  
      

## Configuring the Rundeck PagerDuty Notification

These steps will configure the Notification plugin globally (across all Rundeck projects). There are options to configure the plugin per project covered in the [main documentation](https://github.com/rundeck-plugins/pagerduty-notification#configuration).

Community Steps

Enterprise Steps

Community Steps

1.  Stop the Rundeck service: `systemctl stop rundeckd`.
2.  With any text editor open the `framework.properties` file (located at `/etc/rundeck` path).
3.  Add the following line to the `framework.properties` file (replace â€œyour-service-keyâ€? with the PagerDuty service key you copied earlier):

<div class="language-text line-numbers-mode">

``` text
framework.plugin.Notification.PagerDutyNotification.service_key=your-service-key
```

</div>

1.  Save the file.
2.  Start the Rundeck service: `systemctl start rundeckd.`

Enterprise Steps

Runbook Automation includes a Configuration Management module to set configuration settings via the GUI and store them in the Rundeck database. Database storage shares configuration options with all your cluster members and centralizes configuration.

1.  Click on the **System Menu \> System Configuration**.  
      
    ![System Configuration](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-systemconf.png)  
      
2.  Now, click on the **Add Config** button (top right)  
      
    ![Add Config Entry](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-addconf.png)  
      
3.  In the *Property Name* box add: `framework.plugin.Notification.PagerDutyNotification.service_key`. In the *Property Value* box add the PagerDuty integration key you copied earlier, set `Global` on the *Strata Menu* and press the **Add** button.  
      
    ![Add Notification Entry](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-addpdentry.png)  
      
4.  Press the **Save** button in the top right to save the Config changes.  
      
    ![Save Configuration](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-saveconf.png)  
      

Now, Runbook Automation is configured to use PagerDuty notifications, no restart is required.

## Sending Notifications to a PagerDuty Service.

1.  Create or edit a job.
2.  Go to the **Workflow** tab and add a step. For this example, use a Command step with an `echo "hello world!"` command.
3.  Go to the **Notifications** tab.
4.  On the â€œOn Successâ€? event, click the "+ Add Notification" Button.  
      
    ![Add Notification](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-addnotification.png)  
      
5.  In the Notification Type list select "PagerDuty".  
      
    ![Select PagerDuty](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-addpdnotif.png)  
      
6.  The Incident subject is editable, by default the plugins include [job context variables](https://docs.rundeck.com/docs/manual/jobs/job-variables.html#job-context-variables). Click on the **Save** button for the Notification and **Save** button for the job.
7.  Run the job.

When you check the PagerDuty service incidents, you should see a new triggered incident is created.

  
  
![Incident Created in PD](https://docs.rundeck.com/docs/assets/img/howto-pdnotif-incidentcreated.png)
