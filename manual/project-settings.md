---
title: "Project Settings"
source_url: https://docs.rundeck.com/docs/manual/project-settings.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Project Settings

Each Rundeck Project has it's own unique Configuration Page which contains lets you view and manage project settings.

## Edit Configuration...

Use this section to edit Project Settings like the name, various defaults and enable job execution project wide.

### Details

Edit the Project Name and Description.

### Execution History Cleaner

Automatically removes old execution records based on configurable retention policies. The Execution History Cleaner is the recommended way to maintain a clean, performant execution history.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/execution-history-clean.png" alt="Execution History Clean" />
<figcaption aria-hidden="true">Execution History Clean</figcaption>
</figure>

For comprehensive documentation on how to configure and use the Execution History Cleaner, see [Execution History Cleaner](https://docs.rundeck.com/docs/manual/projects/execution-history-cleaner.html).

### Execution Mode

Used to manage job execution and schedule configuration at project level. If there is a need to disable all job executions for this project, or disabled all scheduled jobs (but still run manually) use the check boxes in this section.

### User Interface

Additional configuration for the user interface for this project that can show or hide helpful information for project users.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-settings-ui.png" alt="User Interface" />
<figcaption aria-hidden="true">User Interface</figcaption>
</figure>

### Default Node Executor Configuration

When Rundeck executes a command on a node, it does so via a "Node Executor". The most common built-in Node Executor is the "SSH" implementation, which uses SSH to connect to the remote node, however other implementations can be used.

Select the Default Node Executor you wish to use for all remote Nodes for the project:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0712.png" alt="Default Node Executor Choice" />
<figcaption aria-hidden="true">Default Node Executor Choice</figcaption>
</figure>

You can install more types of Node Executors as plugins, see [Node Execution Plugins](https://docs.rundeck.com/docs/manual/jobs/job-plugins/#node-execution).

> **Tips**
>
> When using SSH node executor and SCP file copier, the properties will be shared between the file copier and the node executor, so any change made for the node executor will affect the file copier and vice versa. If a more specific configuration is required, this can be done directly in the node definition.

### Default File Copier Configuration

When Rundeck executes a script on a node, it does so by first copying the script as a file to the node, via a "File Copier". (It then uses a "Node Executor" to execute the script like a command.)

The most common built-in File Copier is the "SCP" implementation, which uses SCP to copy the file to the remote node, however other implementations can be used.

Select the Default File Copier you wish to use for all remote Nodes for the project:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0713.png" alt="Default File Copier Choice" />
<figcaption aria-hidden="true">Default File Copier Choice</figcaption>
</figure>

You can install more types of File Copiers as plugins, see [Node Execution Plugins](https://docs.rundeck.com/docs/manual/jobs/job-plugins/#node-execution).

> **Tips**
>
> When using SCP file copier and SSH node executor, the properties will be shared between the file copier and the node executor, so any change made for the file copier will affect the node executor and vice versa. If a more specific configuration is required, this can be done directly in the node definition.

## Edit Nodes...

This section lets you add and modify Node Resource Model Sources for the project. These sources contain the node definitions for the project. A default source will be defined listing the Rundeck Host as a node as a result of the initial project creation. You can configure additional Node Sources to gather all the node information relevant to this project.

See [Node Sources](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/) for more details.

## Node Enhancers

Take advantage of the node enhancers that Rundeck offers by adding them to your nodes. See [Node Enhancers](https://docs.rundeck.com/docs/manual/node-enhancers.html) for more details.

## Access Control

Control access to the project with [ACL Policy GUI](https://docs.rundeck.com/docs/administration/security/acl-policy-editor.html) (Commercial) or [Access Control Policy](https://docs.rundeck.com/docs/administration/security/authorization.html) files.

## Edit Readme...

A project ReadMe can provide some important context for a Project. The content can be formatted using Markdown and can displayed on the Project's home page and as part of the Project Listing.

## Edit Message of the Day...

The Message of the Day is a way to communicate important messages to Project users. The message can be dismissed or hidden after reading using the \[x\] in the upper right corner.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/motd-example.png" alt="Message of the Day" />
<figcaption aria-hidden="true">Message of the Day</figcaption>
</figure>

More info in the [Projects Section](https://docs.rundeck.com/docs/manual/projects/project-motd.html)

## Setup SCM...

More info in the [Projects Section \> SCM](https://docs.rundeck.com/docs/manual/projects/scm/)

## Export Archive...

Use this to export the Project to an Archive file for backup or migration purposes.

More info in the [Projects Section](https://docs.rundeck.com/docs/manual/projects/project-archive.html#export-archive).

## Import Archive...

Use this to import a Project archive file.

More info in the [Projects Section](https://docs.rundeck.com/docs/manual/projects/project-archive.html#import-archive).

## Delete Project...

Use this to delete the project. Note it will delete all associated jobs, node sources, etc.

## Plugins Control

Plugins Control can be used to selectively enable/disable plugins available to this project.

More info in the [Projects Section](https://docs.rundeck.com/docs/manual/projects/plugin-control.html).
