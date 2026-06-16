---
title: "Missed Job Fires (Enterprise Only)"
source_url: https://docs.rundeck.com/docs/manual/schedules/missedjobfires.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Missed Job Fires (Enterprise Only)

> **Available in PagerDuty Runbook Automation Commercial products.**

Scheduled business tasks are essential to internal processes that keep the business running (Financial operations, inventory operations, fulfillment requests, etc.) Scheduled operations tasks are essential to keep infrastructure running (rotating logs, cleaning up temp files, restarting known faulty services, validating configuration and security settings/conditions, etc.). Unknowingly missing either is a business continuity issue. Also unknowingly missing a run and then running again can cause bigger problems. (data corruption, bad configuration, runaway processes, etc)

Missed Jobs marking will keep track of the jobs scheduled, and if one of the jobs doesn't run at the time when it was scheduled to run, an execution with a status of "missed" will be added to the activity page. Additionally, if the job is configured with a failure notification, the notification will be triggered reporting that the job was missed.

> Note: This feature only checks the last "next execution" time of each job, if this next execution time is above the misfire threshold it is considered a missed execution. Thus, if more than one execution of the same job were missed, there will be only **one** missed mark.

> Note: "Next Execution" times are calculated based on calendars, project, system and job schedules.

### Configuration

Misfire detection is enabled by default. If there is a need to change settings use the information below.

> Note: Please make sure all the systems in your cluster have the same configuration. Otherwise, you may experience unexpected results.

1.  Open **System Menu \> Configuration Management**
2.  Click **Add Config**
3.  Add the setting from the list below that needs to be changed.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/misfire-config-mgmt.png" alt="Job Misfire Config" />
<figcaption aria-hidden="true">Job Misfire Config</figcaption>
</figure>

[More information about Configuration Management](https://docs.rundeck.com/docs/manual/configuration-mgmt/configmgmt.html)

Alternatively it's possible to configure the Missed Job Fires feature by adding the following settings in [`rundeck-config.properties`](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#rundeck-config-properties):

<div class="language-properties line-numbers-mode">

``` properties
#Enable the misfire marking feature
rundeck.feature.misfireDetection.enabled=true
#Set the threshold at which a schedule will be marked as missed. Default is 60000ms. The value should be in milliseconds.
rundeck.scheduler.misfire.threshold=60000
#Set the rate at which the server will check for misfires. Default is 60000ms. The value should be in milliseconds.
rundeck.scheduler.misfire.checkRate=60000
```

</div>
