---
title: "Google Cloud Platform - Compute VM Node Source"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/gcp.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Google Cloud Platform - Compute VM Node Source

[Google Cloud Platform](https://cloud.google.com) (GCP) is a cloud service in wide use for dynamic infrastructure; it is easy to start up and shut down Node "Instances" in the cloud.

## Configuring the Node Source

### Authentication & Configuration

Follow the steps outlined in the [**Google Cloud Integration Overview**](https://docs.rundeck.com/manual/plugins/gcp-plugins-overview) doc to configure credentials for the GCP plugins. Credentials can be configured on a per Project basis or for the entire Runbook Automation system.

**Project ID**  
Specify your GCP Project ID.

**Zone**  
Specify your GCP Secret Key. If using the GCP Node Source it's possible to use `${node.zone}` and the Zone will be dynamically populated with the region for that node.

**Access Key Path**  
Path to Key Storage entry containing the Access Key.

> Note: This node source does not support pulling these settings from the System Configuration.

## Filtering Nodes

**Just running instances**  
Will return only running instances to populate the Node listing.
