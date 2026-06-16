---
title: "Sensu Notifications (Enterprise Only)"
source_url: https://docs.rundeck.com/docs/manual/notifications/sensu.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Sensu Notifications (Enterprise Only)

> **Available in PagerDuty Runbook Automation Commercial products.**

Enterprise customers have access to this plugin, that allows users to create an event in Sensu based on the execution status of a job. For example, configure it to create an event if the job failed or if the job succeeded.

## Setup

Before using the Sensu plugins, add the API key and URL to the framework settings To do this, add the API key to Rundeck's key storage and specify the path and the URL value in the framework.

1.  In the top right-hand corner of Rundeck, click on the gear icon and select "Key Storage."
2.  Select "Add or Upload a Key."
3.  For key type, select "Password."
4.  Where it says enter text, copy and paste the API key.
5.  For storage path, this can be anything (REMEMBER THIS FOR LATER). E.g. keys/sensu/api
6.  This can be anything. For example, if api is the name, the new path would be keys/sensu/api.
7.  Now that the keys are created, specify them in the framework. Open the `etc/framework.properties` file and add the following lines:

<div class="language-bash line-numbers-mode">

``` bash
sensu.url=value
sensu.api_key_path=/keys/sensu/api
```

</div>

Where `path` is the path created above

## Send Event

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/sensu-notification1.png" alt="Sensu - Send Event Notification" />
<figcaption aria-hidden="true">Sensu - Send Event Notification</figcaption>
</figure>

- **Entity Namespace** : This is the namespace that the event should be organized in.

- **Check Name** : This is the check to add to the event.

- **Output** : This is the check output for the event.

- **State** : This is the check state for the event. Set the API URL and API key in the project/framework settings prior to creating the job, there will be a list of state values that are currently in Sensu to choose from.

- **Status** : This is the check status for the event. Set the API URL and API key in the project/framework settings prior to creating the job, there will be a list of status values that are currently in Sensu to choose from.

- **Check Handlers** : Select one of the check handlers and it will apply that handler to the new event. I.e. if "Slack Handler" is selected, a notification will be sent to slack.

- **Is Silence?** : If checked, the event will be silenced.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/sensu-notification2.png" alt="Sensu - Send Event Notification - continued" />
<figcaption aria-hidden="true">Sensu - Send Event Notification - continued</figcaption>
</figure>

- **Check Interval** : This is the interval to run the check on.

- **API URL** : This is the endpoint that needs to be hit in order to create an event for an account. For example, `http://sensu:8080/api/core/v2/namespaces/default`. If it is already specified it in project or framework settings, no need to add it again here.

- **API Key** : This is the API key for the account to create an event in. Choose the one created in the Setup section above. If it is already specified it in project or framework settings, no need to add it again here.
