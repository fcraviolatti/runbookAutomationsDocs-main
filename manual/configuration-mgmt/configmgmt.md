---
title: "System Configuration (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/configuration-mgmt/configmgmt.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# System Configuration (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

Runbook Automation includes a System Configuration module to set configuration settings via the GUI and store them in the Rundeck database. Database storage shares configuration options with all your cluster members and centralizes configuration. This can significantly streamline the configuration of new Rundeck servers. Most settings will be set and refreshed upon Saving. If a setting requires a restart there is a message to let users know.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/configmgmt-list.png" alt="System Configuration" />
<figcaption aria-hidden="true">System Configuration</figcaption>
</figure>

## Managing Configuration

Use the **+ Add Config** button to add new configuration entries.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/configmgmt-add-config.png" alt="Add Config Mgmt Entry" />
<figcaption aria-hidden="true">Add Config Mgmt Entry</figcaption>
</figure>

**Property Name**

Enter the property value here. A dynamic drop-down will pre-populate with some suggested settings, but the field will take any value.

**Property Value**

Enter the value for the setting here. Currently, the field only supports string values.

## Initial Boot Notes

On the initial Rundeck build/boot, all configuration items are still written to the traditional file-based configuration files. In order to use this feature configuration settings must be written in this System Configuration GUI, then removed from the file-based configurations. File-based configurations will take precedence over database configurations.
