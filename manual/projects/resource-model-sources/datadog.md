---
title: "Datadog Node Source"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/datadog.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Datadog Node Source

> **Available in PagerDuty Runbook Automation Commercial products.**

Runbook Automation users have the ability to use this plugin to import their host list in Datadog by creating nodes matching all the hosts. This makes it easy to import nodes from Datadog.

## Connection

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/resource-connect.png" alt="Datadog Resource Model - Connection" />
<figcaption aria-hidden="true">Datadog Resource Model - Connection</figcaption>
</figure>

Follow the instructions outlined in the [**Datadog Integration Overview**](https://docs.rundeck.com/manual/plugins/datadog-plugins-overview) to set up authentication with Datadog.

## Configuration

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/resource-config.png" alt="Datadog Resource Model - Configuration" />
<figcaption aria-hidden="true">Datadog Resource Model - Configuration</figcaption>
</figure>

- **Attribute Prefix** : This creates an attribute prefix for all the attributes for that host. For example, on attribute is "isMuted" which is a boolean to determine if the host is muted. Instead, it would appear as dd.isMuted is you put "dd" here.

- **Tag Prefix** : This create a prefix for all the tags for that host. So instead of just the tag, it will now be dd.tag. This helps to organize the different nodes in Rundeck.
