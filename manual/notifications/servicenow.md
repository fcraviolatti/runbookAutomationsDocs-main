---
title: "ServiceNow\u00c2\u00ae Notification Plugins"
source_url: https://docs.rundeck.com/docs/manual/notifications/servicenow.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# ServiceNowÂ® Notification Plugins

> **Available in PagerDuty Runbook Automation Commercial products.**

To configure authentication with ServiceNow for these notification plugins, follow the steps outlined in [ServiceNow Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/servicenow-plugins-overview.html) to set credentials at either a System or Project level.

## ServiceNow / Incident / Comment

Notification plugin to comment an incident.

### Usage

To use the plugin, configure this mandatory input:

- incident key: ServiceNow incident ID.
- Comment: Comment to add.

## ServiceNow / Incident / Create

Notification plugin that creates an incident.

### Usage

To use the plugin, configure this mandatory input:

- caller: the username of the assigned Caller field of the Incident.

These inputs are optional and if left empty the default value of Service now it's going to be used

- urgency: A number representing the urgency of the incident (usually being 1 the most urgent)
- impact: A number representing the impact of the incident (usually being 1 the higher urgent)
- priority: A number representing the priority of the incident (calculated from urgency and impact)
- Assignment Group: Assignment Group. If not set, no value will be sent
- Description: Description to be used

## ServiceNow / Change / Create

Notification plugin to create a ServiceNow Change.

### Usage

To use the plugin, configure this mandatory input:

- assignment group: ServiceNowÂ® incident ID.
- state: State code. If not set, the change will be in New status.
