---
title: "Datadog Health Check (Enterprise Only)"
source_url: https://docs.rundeck.com/docs/manual/healthcheckplugins/datadog.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Datadog Health Check (Enterprise Only)

> **Available in PagerDuty Runbook Automation Commercial products.**

## Overview

The DataDog Health Check plugin allow Rundeck to check status of DataDog hosts to determine if they are healthy. The plugin checks if the host is up according to the DataDog system and returns "healthy/unhealthy". Optionally, the plugin can check the status of the DataDog Agent process.

## Preparation

Gather the API Key and APP Key from your DataDog portal. [Click here for more information from DataDog documentation](https://docs.datadoghq.com/account_management/api-app-keys/).

Follow the instructions outlined in the [**Datadog Integration Overview**](https://docs.rundeck.com/manual/plugins/datadog-plugins-overview) to set up authentication with Datadog.

## Configuration

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/healthcheck-datadog-config.png" alt="DataDog HealthCheck Config" />
<figcaption aria-hidden="true">DataDog HealthCheck Config</figcaption>
</figure>

**Node Filter**: This is the Node Filter used to determine which nodes the HealthCheck is run against.

**Label**: Name to reference this instance of the HealthCheck

**API Key**: The DataDog API Key used to authenticate.

**APP Key**: The DataDog APP Key used to authenticate.

**Health Check Agent**: Check the status of the DataDog Agent on these nodes. If the agent is not running it will return an "unhealthy" status.
