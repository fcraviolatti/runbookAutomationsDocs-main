---
title: "Azure Log Storage Plugin"
source_url: https://docs.rundeck.com/docs/administration/cluster/logstore/azure.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Azure Log Storage Plugin

The Azure Storage plugin uses Azure Storage to store execution log files, for backup or for a cluster environment behavior.

The source code lives at <https://github.com/rundeck-plugins/rundeck-azure-plugin>.

### Enable the plugin

Enable the ExecutionFileStorage provider named azure-storage in your `rundeck-config.properties` file:

`rundeck.execution.logs.fileStoragePlugin=azure-storage`

### Configuration

To configure the Azure Storage Account credentials you can set these property values:

- **storageAccount**: Azure Storage Account

- **accessKey**: Azure Storage Access Key

- **path**: The path in the bucket to store a log file.

  You can use these expansion variables:

  - `${job.execid}` = execution ID
  - `${job.project}` = project name
  - `${job.id}` = job UUID (or blank).
  - `${job.group}` = job group (or blank).
  - `${job.name}` = job name (or blank)

You can define the configuration values in `framework.properties` by prefixing the property name with the stem: `framework.plugin.ExecutionFileStorage.azure-storage`. Or in a project's `project.properties` file with the stem `project.plugin.ExecutionFileStorage.azure-storage`.

For example:

<div class="language-properties line-numbers-mode">

``` properties
#storage.storageAccount and storage.accessKey
framework.plugin.ExecutionFileStorage.azure-storage.storageAccount=<ACCOUNT-NAME>
framework.plugin.ExecutionFileStorage.azure-storage.accessKey=<ACCESS-KEY>
framework.plugin.ExecutionFileStorage.azure-storage.defaultEndpointProtocol=https

#path to store the logs
framework.plugin.ExecutionFileStorage.azure-storage.path=logs/${job.project}/${job.execid}.log
```

</div>

> **Warning**
>
> This will work only if the generated paths follow the [naming conventions for Azure Storage services](https://docs.microsoft.com/en-us/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).

#### (Enterprise Version only):

The Azure Storage Enterprise Version includes the [checkpoint property](https://docs.rundeck.com/docs/administration/configuration/plugins/configuring.html#logging-checkpoints) which enables an incremental update to the execution log across the members of the cluster. To use the pro version of this plugin (3.4.4+), please use the following on the rundeck-config.properties:

<div class="language-properties line-numbers-mode">

``` properties
rundeck.execution.logs.fileStoragePlugin=rundeckpro.azure-storage
```

</div>

And on the framework.properties:

<div class="language-properties line-numbers-mode">

``` properties
framework.plugin.ExecutionFileStorage.rundeckpro.azure-storage.storageAccount=<STORAGE_ACCOUNT_NAME>
framework.plugin.ExecutionFileStorage.rundeckpro.azure-storage.accessKey=<STORAGE_ACCESS_KEY>
framework.plugin.ExecutionFileStorage.rundeckpro.azure-storage.containerName=logs
framework.plugin.ExecutionFileStorage.rundeckpro.azure-storage.path=${job.project}/${job.execid}
framework.plugin.ExecutionFileStorage.rundeckpro.azure-storage.defaultEndpointProtocol=https
```

</div>

And on the framework.properties to delete executions in your logstorage:

<div class="language-properties line-numbers-mode">

``` properties
framework.plugin.ExecutionFileStorage.rundeckpro.azure-storage.allowDeleteFiles=true
```

</div>
