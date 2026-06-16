---
title: "Health Checks (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/healthchecks.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Health Checks (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

## Overview

Health Checks allow the ability to check the *Health Status* of Nodes periodically and on-demand. It can show the heatlh status visually in the GUI, and use the status to filter out unhealthy nodes when running Jobs.

> **Health Checks with Enterprise Runners**
>
> Health Checks are fully compatible with Enterprise Runners as of version 5.18.0. Health Checks will continue to work correctly when Runners are enabled and assigned to projects.

![Health Checks](https://docs.rundeck.com/docs/assets/img/healthchecks-health-status-ui.png)  

Configure how to determine the Health Statuses of Nodes in Rundeck, using a Command or Script.

Capture output of the command or script to add as attributes to the nodes in Rundeck.

Expose the status as Node Attributes using the Health Status Node Enhancer, and use the health check attributes inside node filters.

Use the secondary node filter feature of Jobs to pre-filter out unhealthy nodes, and see which nodes will be targetted and which will be filtered out before running a Job.

## Health Checks System

The Health Checks System operates across several parts of the Rundeck System:

- **Project Nodes** - as determined by the account's Nodes configuration.
- **Health Checks configuration** - the definition of which checks to run in the project configuration.
- **Node Execution** - Command and Script execution use the configured Node Executor for the nodes
- **ACL Policies** - Access control definition used by the Health Checks when performing Node Execution
- **Health Checks System** - periodically and asychronously performs the Health Checks
  - **Health Checks Cache** - a cache of the results of the health checks
- **Node Enhancer** - the "Health Status" Node enhancer layers additional attributes onto the Project Nodes by reading data from the Health Checks Cache

## Usage

Enable Health Checks in the Project configuration.

Configure multiple Health Check Plugins for each project, and each Health Check can apply to all nodes (default) or a select set of nodes using a Node Filter.

Each Health Check can have a "label", which identifies it within the generated Node Attributes.

### Running Health Checks

Health Checks will be run *on-demand* asynchronously and the results will be cached for a period of time. The *on-demand* aspect is triggered when Health Status information is *requested* of the Health Checks System. The request can be triggered by accessing the Nodes page of Rundeck, or otherwise reading the Nodes data, such as preparing to run a Job. Initially, each node would be given an "Unknown" status, until the Health Checks are completed.

After a period of time, the Health Checks results will *expire*, and another request for Nodes data would trigger a *refresh* of the data.

It is also possible to *Refresh* the results in the GUI directly, which will cause the checks to be run again for the nodes.

## Status Results

Each Health Check will result in a Health Status:

- **Healthy** - the check reported Healthy results
- **Unhealthy** - the check reported Unhealthy results
- **Error** - a problem creating or executing the Health Check
- **Skipped** - the check was not applied to the node (e.g. it did not match the filter)
- **Unknown** - the check could not run or was not conclusive

## Setup

1.  Visit the "Project Settings... \> Edit Nodes" page. Under the Configuration tab, check the "Health Checks Enabled" checkbox:

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-enabled.png" alt="Health Checks Enabled" />
    <figcaption aria-hidden="true">Health Checks Enabled</figcaption>
    </figure>

    Alternately, in the project configuration properties file, add the configuration:

    <div class="language-properties line-numbers-mode">

    ``` properties
    project.healthcheck.enabled=true
    ```

    </div>

    The health check uses a cache to store the statuses and improve performance when requesting them. To automatically refresh the Health Checks, enable the "Refresh health status cache" and set the update period in the "Cache refresh period" field whose default value is 30 seconds.

2.  Visit the sidebar link "Health Checks"

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-sidebar-link.png" alt="Sidebar - Health Checks Link" />
    <figcaption aria-hidden="true">Sidebar - Health Checks Link</figcaption>
    </figure>

3.  Click on the "Configure" Tab, and add a Health Check Plugin. Here we add the simple Command Health Check plugin, and leave the default command of `uname`. Click "Save" and "Save" again.

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-add-healthcheck-plugin.png" alt="Configure - Add Health Check Plugin" />
    <figcaption aria-hidden="true">Configure - Add Health Check Plugin</figcaption>
    </figure>

4.  Return to the Nodes Tab to see a list of nodes.

    There may be a message saying "Unauthorized: cannot execute on node". If so, add an ACL Policy to allow the Health Check System to run commands and scripts on the target nodes. See [Access Control](#access-control).

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-unauthorized.png" alt="Health Checks - Unauthorized Warning" />
    <figcaption aria-hidden="true">Health Checks - Unauthorized Warning</figcaption>
    </figure>

5.  Once Access Control is configured, the checks should be showing up and healthy:

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-healthy-checks.png" alt="Health Checks - Healthy checks" />
    <figcaption aria-hidden="true">Health Checks - Healthy checks</figcaption>
    </figure>

6.  Return to the "Project Settings... \> Edit Nodes" page. Under "Enhancers" click "Add a new Node Enhancer" and choose "Health Status".

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-add-node-enhancer.png" alt="Health Checks - Add Node Enhancer" />
    <figcaption aria-hidden="true">Health Checks - Add Node Enhancer</figcaption>
    </figure>

    Option to modify the settings, or keep the defaults. Make sure "UI Status Attributes" is added, to add UI indicators. Then click "Save" and "Save" again.

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-add-health-status-enhancer.png" alt="Health Checks - Add Health Status Enhancer" />
    <figcaption aria-hidden="true">Health Checks - Add Health Status Enhancer</figcaption>
    </figure>

7.  Visit the "Nodes" link in the Sidebar. There will be healthy status indicators for the nodes:

    <figure>
    <img src="https://docs.rundeck.com/docs/assets/img/healthchecks-health-status-ui.png" alt="Health Checks - Node Health Status UI" />
    <figcaption aria-hidden="true">Health Checks - Node Health Status UI</figcaption>
    </figure>

> **Tips**
>
> In order to avoid "TaskRejectedException" when having health check enabled with a large number of nodes (over 525). It is recommended to increase the health check queue and pool size to at least match the node list size. You can add the following properties to the rundeck-config.properties file and change their default values.
>
> <div class="language-properties line-numbers-mode">
>
> ``` properties
> # Default values
> rundeckpro.healthcheck.statusService.queueCapacity=500
> rundeckpro.healthcheck.statusService.maxPoolSize=25
> ```
>
> </div>
>
> <div class="language-properties line-numbers-mode">
>
> ``` properties
> # Example values for 836 nodes
> rundeckpro.healthcheck.statusService.queueCapacity=800
> rundeckpro.healthcheck.statusService.maxPoolSize=36
> ```
>
> </div>

## Job Filter

Use the "Exclude Filter" in Job definitions to filter out unhealthy nodes, while still indicating in the UI those nodes will be excluded. Make sure to set "Show Excluded Nodes" to "Yes". If some nodes are unhealthy it will show the node but it will be crossed out:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/healthchecks-job-edit-exclude-filter.png" alt="Health Checks - Job Definition - Exclude Unhealthy Nodes" />
<figcaption aria-hidden="true">Health Checks - Job Definition - Exclude Unhealthy Nodes</figcaption>
</figure>

When a Job is run, the excluded nodes will be indicated and automatically deselected. Note: if "Show Excluded Nodes" is set to "No", the excluded nodes will not be shown at all.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/healthchecks-run-job-excluded-filter.png" alt="Health Checks - Run Job - Exclude Unhealthy Nodes" />
<figcaption aria-hidden="true">Health Checks - Run Job - Exclude Unhealthy Nodes</figcaption>
</figure>

## Refresh Cache Before Execution

Enable the "Refresh HealthChecker Cache" plugin to force healthcheck cache to refresh before job execution starts.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/refresh_healthcheck_cache_exec_lifecycle_plugin.png" alt="Refresh HealthChecker cache" />
<figcaption aria-hidden="true">Refresh HealthChecker cache</figcaption>
</figure>

## Access Control

To execute commands and scripts on Nodes, the Health Checks System adopts a username/role of "system/system".

Control what nodes are allowed to be executed on by adding an appropriate ACL Policy.

Here is an example ACL Policy to allow access to all nodes within a project.

<div class="language-yaml line-numbers-mode">

``` yaml
by:
  group: system
for:
  node:
    - allow: run
description: Allow run on all nodes for system Health Checks
```

</div>

Change the Username and Role adopted by the Health Checks System with the following configuration in `rundeck-config.properties`:

<div class="language-properties line-numbers-mode">

``` properties
rundeck.healthcheck.access.username=system
rundeck.healthcheck.access.role=system
```

</div>

## Health Status Node Attributes

When the "Health Status" Node Enhancer is applied, it will add Node Attributes to each node checked.

The attributes it adds contains the summary Health Status, as well as individual health check statuses. It can also add UI status attributes, and cache information.

By default the prefix for all healthcheck attributes is `healthcheck:` but this can be modified.

- `healthcheck:status` the overall health status. One of `HEALTHY`,`UNHEALTHY`,`UNKNOWN`,`ERROR` or `SKIPPED`

Cache information:

- `healthcheck:duration` the total time for performing healthchecks, in milliseconds, e.g. `950`
- `healthcheck:lastCheckTime` the last check time timestamp, e.g. `Tue Nov 26 09:54:18 PST 2019`

Individual Health Check results. If a "label" is defined on the health check plugin configuration, the attribute will use the label in the prefix. Otherwise, the attribute will use the health check number in the prefix. E.g. `healthcheck:mycheck:` or `healthcheck:1:`.

- `healthcheck:label:status` plugin status result
- `healthcheck:label:type` plugin type
- `healthcheck:label:message` any message from the plugin
- `healthcheck:label:$ATTR` any attributes captured by the plugin
