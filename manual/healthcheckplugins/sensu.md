---
title: "Sensu Health Check (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/healthcheckplugins/sensu.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Sensu Health Check (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

## Authentication

To authenticate Runbook Automation with Sensu, follow instructions outlined in [this documentation](https://docs.rundeck.com/docs/manual/plugins/sensu-plugins-overview.html).

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/sensu-health.png" alt="Sensu - Health Check" />
<figcaption aria-hidden="true">Sensu - Health Check</figcaption>
</figure>

- **Node Filter** : Specify a node filte here, and only the nodes matching the filter will use the health check.

- **Label** : The label for the health check being created. Can be anything.

- **API URL** : This is the endpoint that needs to be hit in order to use health check for an account. For example, `http://sensu:8080/api/core/v2/namespaces/default`. If it is already specified it in project or framework settings, there is no need to add it again here.

- **API Key** : This is the API key for the account to get node information from. If it is already specified it in project or framework settings, there is no need to add it again here.
