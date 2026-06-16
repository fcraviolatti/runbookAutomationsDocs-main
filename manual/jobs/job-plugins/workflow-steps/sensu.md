---
title: "Sensu Workflow Steps (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/sensu.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Sensu Workflow Steps (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

## Authentication

To authenticate Runbook Automation with Sensu, follow instructions outlined in [this documentation](https://docs.rundeck.com/docs/manual/plugins/sensu-plugins-overview.html).

## Sensu / Check / Create

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/sensu-create-check.png" alt="Sensu - Create Check" />
<figcaption aria-hidden="true">Sensu - Create Check</figcaption>
</figure>

- **Check Name** : This is the name of the check to create.

- **Check NameSpace** :This is the namespace to add the check too.

- **Check command** : This is the command for the check to run.

- **Check Subscriptions** : These are the subscriptions that to be added to the check. Example: `system, entity:12345`

- **Check Handlers** : If one of the check handlers is selected, it will apply those handlers to the new event. I.e. if "Slack Handler" is selected, a notification will be sent to slack.

- **Check Type** : This is the type that the check being created should be. If the API URL and API key are set in the project/framework settings prior to creating the job, there will be a list of check types that are currently in Sensu to choose from.

- **Check Interval** : This is interval the check should be run on.

- **Check Cron** : Set the check cron here. Example: `* * * * *` , `TZ=America/Los_Angeles * * * * *`

## Sensu / Delete / Silence

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/sensuwf-delete-silence.png" alt="Sensu - Delete a Silence on a Check" />
<figcaption aria-hidden="true">Sensu - Delete a Silence on a Check</figcaption>
</figure>

- **Check Name** : This is the check the silenced entry should be deleted on. If the API URL and API key are set in the project/framework settings prior to creating the job, there will be a list of checks that are currently in Sensu to choose from

- **Subscriptions** : These are the subscriptions that the entry should match. I.e. system, entity:id123

## Sensu / Create / Silence Entry

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/sensu-create-silenced.png" alt="Sensu - Create Silenced Entry" />
<figcaption aria-hidden="true">Sensu - Create Silenced Entry</figcaption>
</figure>

- **Check Name** : This is the check to create a silenced entry for. If the API URL and API key are set in the project/framework settings prior to creating the job, there will be a list of checks that are currently in Sensu to choose from

- **Namespace** : This is the namespace the silenced entry should be in.

- **Subscriptions** : These are the subscriptions that the new entry should match. I.e. system, entity:id123

- **Silence Reason** : This is the reason for silencing. Can be anything.

- **Expired**

- This is when the silenced entry should expire. This should be in number of seconds.

- **Begin** : This is when the silenced entry should begin. Can specify seconds, minutes, hours. (I.e. 2s, 3m, 4h)

- **Expire on Resolve** : If this is checked, then if the check finished successfully then the silenced entry will be deleted.

- **API URL** : This is the endpoint that needs to be hit in order to get the checks for a specific account. For example, `http://sensu:8080/api/core/v2/namespaces/default`. If it is already specified it in project or framework settings, no need to add it again here.

- **API Key** : This is the API key for the account with the check to get information about. If it is already specified it in project or framework settings, no need to add it again here.
