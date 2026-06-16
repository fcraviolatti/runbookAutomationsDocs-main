---
title: "Cluster Resource Model Source"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/cluster.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Cluster Resource Model Source

> **Available in PagerDuty Runbook Automation Commercial products.**

The **Cluster Resource Model Source** plugin exposes Rundeck cluster members as nodes in the node inventory. This enables administrators to execute jobs and commands directly on cluster members for maintenance, monitoring, and cluster management tasks.

## Setup

To add the Cluster Resource Model Source to a project:

1.  Navigate to **Project Settings** -\> **Edit Nodes** -\> **Sources**
2.  Click **Add a New Node Source**
3.  Select **Cluster Resource Model Source** from the list

> **Cluster Configuration**
>
> This node source requires a Rundeck cluster environment. See the [Cluster Overview](https://docs.rundeck.com/docs/administration/cluster/) for information on setting up a cluster.

## Configuration

The following configuration option is available:

- **Show Dead Nodes**: Include cluster members that are no longer active or have stopped responding. When enabled, inactive cluster members will appear in the node inventory. Default: `false` (only active cluster members are shown).

## SSH Connection Configuration

The Cluster Resource Model Source uses the `framework.server.name` property as the SSH connection hostname for each cluster member. By default, this may contain internal or container hostnames that are not DNS-resolvable from other cluster members.

### Configuring Resolvable Hostnames

To enable SSH connections to cluster member nodes, configure the following properties in the `framework.properties` file on each cluster member:

**Required Properties:**

- **framework.server.name**: Set to a DNS-resolvable hostname or IP address that other cluster members can reach
- **framework.server.hostname**: The hostname of the Rundeck server node (can match framework.server.name)
- **framework.ssh.user**: Default SSH username for connections to cluster members
- **framework.ssh.keypath**: Path to the SSH private key file used for authentication

**Example Configuration:**

<div class="language-properties line-numbers-mode">

``` properties
framework.server.name=rundeck-node-1.example.com
framework.server.hostname=rundeck-node-1.example.com
framework.ssh.user=rundeck
framework.ssh.keypath=/var/lib/rundeck/.ssh/id_rsa
```

</div>

> **SSH Authentication**
>
> SSH authentication settings can be overridden using node attributes such as `ssh-key-storage-path` or `username`. See [SSH Node Execution](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html) for configuration options and precedence.

See [Configuration File Reference](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#frameworkproperties) for more details on framework properties.

## Node Attributes

The following attributes are automatically populated for each cluster member node:

- **serverUUID**: Unique identifier for the cluster member
- **rundeckVersion**: Rundeck version running on the cluster member
- **cpuLoadPct**: CPU load percentage
- **heapusagePct**: JVM heap memory usage percentage
- **memoryAllocatedPct**: Total memory allocation percentage
- **schedulerRunningCount**: Number of currently running scheduled jobs
- **osName**: Operating system name
- **osArch**: Operating system architecture
- **osVersion**: Operating system version

These attributes can be used for node filtering, job targeting, and monitoring cluster health.
