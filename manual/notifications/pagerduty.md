---
title: "PagerDuty Notifications Plugins (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/notifications/pagerduty.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# PagerDuty Notifications Plugins (Commercial)

PagerDuty notification plugins can be added to jobs within Rundeck so alerts go to PagerDuty. When one of the following conditions is met, it will create an event in PagerDuty:

- **On Start**: the job was started
- **On Success**: the job completed successfully
- **On Failure**: the job failed or was aborted
- **On Avg. Duration**: the execution exceeded the average duration of the job
- **On Retryable Failure**: the job failed but will be retried

## Send Event Notification

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/pagerduty_notification.png" alt="PagerDuty - Notification Plugin" />
<figcaption aria-hidden="true">PagerDuty - Notification Plugin</figcaption>
</figure>

The example photo above is for a notification following a job completing successfully. Select the PagerDuty plugin in a different section to have a different condition trigger the notification.

- **Dedupe Key**: This is the incident key
- **Integration Key**: In order to generate a new integration key, you need to add a new Rundeck integration into the service you wish to get notifications for
- **Action**: The action can be trigger, acknowledge or resolve based on the status of the event
- **Payload Severity**: Specify the severity
- **Images**: Provide the list of image URLs to include, separated by a comma

## Escalate Incident Notification

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/pd_escalate_notification.png" alt="PagerDuty - Escalate Incident Notification Plugin" />
<figcaption aria-hidden="true">PagerDuty - Escalate Incident Notification Plugin</figcaption>
</figure>

- **API Key**: The API key for the account containing the incident.
- **Email**: A valid email associated with the account containing the incident.
- **Incident ID**: The ID of the incident you want to escalate
- **Escalation Level**: The level of the escalation policy to move the incident to.

## Run Response Play Notification

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/notification_runresponse.png" alt="PagerDuty - Run Response Play Notification Plugin" />
<figcaption aria-hidden="true">PagerDuty - Run Response Play Notification Plugin</figcaption>
</figure>

- **Incident ID**: The ID of the incident to run a response play on.
- **Response Play ID**: The ID of the response play you would like to be run on the incident.
- **Email**: A valid email address associated with the account the incident is in.
- **API Key**: The API key for the account containing the incident.

## Add Incident Note Notification

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/notification_incidentnote.png" alt="PagerDuty - Inident Note Notification Plugin" />
<figcaption aria-hidden="true">PagerDuty - Inident Note Notification Plugin</figcaption>
</figure>

- **API Key**: The API key for the account containing the incident.
- **Email**: A valid email address associated with the account the incident is in.
- **Incident ID**: The ID of the incident to add the note to.
- **Note**: The note to add to the PagerDuty incident.

*Automated Diagnostics Example Note:*

Beginning Automated Diagnostics job "\${job.project}/\${job.group}/\${job.name}" for incident "\${option.pd_incident_id}". See the full Rundeck log at: \${job.url}
