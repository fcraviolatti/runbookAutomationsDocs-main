---
title: "Feature setup and compatibility"
source_url: https://docs.rundeck.com/docs/administration/runner/runner-setup.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Enterprise Runner - feature setup

## Pre-Requisites

The new architecture is available with v4.11+ of Runbook Automation. The new architecture is off by default and can be turned on with a system setting. The Runner authentication and communication architecture is the same between the two generations of Runners. The new Runners use new APIs, management UI, and have a new and more extensive set of plugins available.

## Setup steps

If the enterprise Runners are enabled you can skip setting the **`runner.enabled`** setting. If you have not enabled the Runner feature please do so by doing the following: Add the following property in rundeck-config.properties file and restart the Runbook Automation. This feature has been enabled on Docker installations since v4.5.0 and is also enabled by default for Runbook Automation:

**`rundeck.feature.runner.enabled`** and set it to **`true`**.

To use the latest features, be sure to add the following property in **System Configuration** as well:

**`rundeck.feature.distributedAutomation.enabled`** and set it to **`true`**.

## Upgrade Notes for customers previously using Runners before Runbook Automation version 4.11

This section applies only for installations that have deployed the previous generation architecture of Runbook Automation Runners (this does not apply to Automation Action Runners). You can disable the new architecture by changing the setting to false which will revert to the previous behaviors and UIs of the Runners. Toggling the feature on and off does NOT change Job or Runner data, but it does change how jobs use Runners and the Runbook Automation UI.

If you are using the previous generation of Runners before v4.11, and want to enable the new architecture please review how the new architecture behaves - [Overview](https://docs.rundeck.com/docs/administration/runner/), [Configuration](https://docs.rundeck.com/docs/administration/runner/runner-config.html) and [Usage](https://docs.rundeck.com/docs/administration/runner/using-runners/runner-using.html) of the new Runners before making changes. The new architecture uses Runner tags that are referenced in Jobs when selecting which Runners will carry out a task instead of relying on node filters hardcoded in the Runner configuration. Once reviewed, update the configuration of your Runners and the jobs using them with the following steps:

1.  Set **`rundeck.feature.distributedAutomation.enabled`** = true as described previously.
2.  Upgrade the Runners to the latest version.
