---
title: "Cluster Overview"
source_url: https://docs.rundeck.com/docs/administration/cluster/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Cluster Overview

> **Available in PagerDuty Runbook Automation Commercial products.**

## Runbook Automation Self-Hosted Architecture

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/SingleCluster.png" alt="Runbook Automation Self-Hosted architecture" />
<figcaption aria-hidden="true">Runbook Automation Self-Hosted architecture</figcaption>
</figure>

## Installation

To install a new Runbook Automation instance, download the latest version from [here](https://www.rundeck.com/downloads), and review requirements and deployment steps in the Deployment Guide.

![](data:image/svg+xml;base64,PHN2Zz48cGF0aCAvPjwvc3ZnPg==)

## Requirements

The Runbook Automation environment needs the following shared resources:

### Database

- All the cluster instances must share the same DB:

  See: [Database Backends](https://docs.rundeck.com/docs/administration/configuration/database/).

- The keys and project data must be stored in the DB (enabled by default since 2.4.x):

  See: [Storage Facility](https://docs.rundeck.com/docs/administration/configuration/storage-facility.html)

### Load Balancer

A load balancer allows you to achieve high availability in your Runbook Automation installation by routing http traffic across several redundant Runbook Automation instances.

- Set the `grails.serverURL` parameter of all cluster members (`rundeck-config.properties`) with the LB URL.

- Use Sticky session

See: [Loadbalancer](https://docs.rundeck.com/docs/administration/cluster/loadbalancer/)

### Log Storage

All Cluster instances must share the same storage location for execution logs.

See: [Logstore](https://docs.rundeck.com/docs/administration/cluster/logstore/)

**Note**: If you use the [S3 Log Storage Plugin](https://docs.rundeck.com/docs/administration/cluster/logstore/s3.html) Be sure to use `com.rundeck.rundeckpro.amazon-s3` in place of `org.rundeck.amazon-s3`. It adds the additional feature:

- *Checkpoint log storage*: This enables viewing the execution logs while the execution is running.

### Authentication

The cluster environment needs a common authentication method. All the instances must have access to the same list of users/groups

See: [Authenticating Users](https://docs.rundeck.com/docs/administration/security/authentication.html)

### Resource Model

Projects need a common resource model that can be accessed from all cluster members. These are some of the alternatives to achieve this:

- A shared file system
- A script
- A REST endpoint

See: [Node Model Sources](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/)

## Features:

### Autotakeover

Scheduled jobs are owned by the last cluster member who modified them. Jobs can also be controlled using Cluster Manager. If a cluster member goes down, all scheduled jobs on that cluster member must be moved to another cluster node. This process can be performed automatically using the heartbeat and Autotakeover features in Runbook Automation version 2.1.0 and later releases.

See: [Autotakeover](https://docs.rundeck.com/docs/administration/cluster/autotakeover/)

### Cluster Remote Execution Policy

This feature allows Runbook Automation cluster members to forward job executions to other cluster members based on a policy configuration.

See: [Remote Job Execution](https://docs.rundeck.com/docs/administration/configuration/remote-job-execution.html)

### Runbook Automation Replication

This plugin is used for an active/passive configuration. Each cluster member can have its own database.

See [Runbook Automation Replication](https://docs.rundeck.com/docs/administration/cluster/replication/)
