---
title: "Google Cloud Compute Health Check"
source_url: https://docs.rundeck.com/docs/manual/healthcheckplugins/gcp-compute-healthcheck.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Google Cloud Compute Health Check

The Google Cloud Platform(GCP) Compute Health Check can provide health status updates based on whether the Google Compute instance is running or not.

### Authentication & Configuration

Follow the steps outlined in the [**Google Cloud Integration Overview**](https://docs.rundeck.com/manual/plugins/gcp-plugins-overview) doc to configure credentials for the GCP plugins. Credentials can be configured on a per Project basis or for the entire Runbook Automation system.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/healthcheck-gcp-compute.png" alt="GCP Compute Health Check" />
<figcaption aria-hidden="true">GCP Compute Health Check</figcaption>
</figure>

- **Node Filter:** This is the node filter that determines which nodes to run this health Check against. The default is `tags: GCPCOMPUTE`. A `GCPCOMPUTE` tag is applied automatically by the Node Source.

  > If the Project is using more than one EC2 Node Source for multiple regions it would be important to add the region to the Node Filter to the region this Node Filter is targeting.

- **Label**: A user friendly label for the Health Check

- **Project ID**: GCP Project ID where the Compute Instances are running.

- **Service Account Key Path**: Path in the Key Storage where the Access Key JSON is stored.

- **Zone**: The GCP Zone where these nodes are running.
