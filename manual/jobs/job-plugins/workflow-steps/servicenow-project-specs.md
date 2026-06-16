---
title: "Establishing A ServiceNow\u00c2\u00ae Connection at the Project Level"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/servicenow-project-specs.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Establishing A ServiceNowÂ® Connection at the Project Level

> **Head Up!**
>
> There is an easier way to configure ServiceNow plugins at the Project Level. See [ServiceNow Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/servicenow-plugins-overview.html) for instructions.

For all the different ServiceNowÂ® job steps, the connection can also be established at the project level. In order to do so, add the following to your project configuration file, depending on which job step you are utilizing:

## ServiceNow / Incident / Update State

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Incident-Change-State.url=https://server.service-now.com
project.plugin.WorkflowStep.Service-Now-Incident-Change-State.login=user
project.plugin.WorkflowStep.Service-Now-Incident-Change-State.password-key-storage-path=keys/servicenow/pass
```

</div>

## ServiceNow / Incident / Check Assigned

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Incident-Check-Assigned.login=user
project.plugin.WorkflowStep.Service-Now-Incident-Check-Assigned.password-key-storage-path=keys/servicenow/pass
project.plugin.WorkflowStep.Service-Now-Incident-Check-Assigned.url=https://server.service-now.com
```

</div>

## ServiceNow / Incident / Check State

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Incident-Check-State.login=user
project.plugin.WorkflowStep.Service-Now-Incident-Check-State.password-key-storage-path=keys/servicenow/pass
project.plugin.WorkflowStep.Service-Now-Incident-Check-State.url=https://server.service-now.com
```

</div>

## ServiceNow / Incident / Comment

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Comment.login=user
project.plugin.WorkflowStep.Service-Now-Comment.password-key-storage-path=keys/servicenow/pass
project.plugin.WorkflowStep.Service-Now-Comment.url=https://server.service-now.com
```

</div>

## ServiceNow / Incident / Create

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Incident-Create.login=user
project.plugin.WorkflowStep.Service-Now-Incident-Create.password-key-storage-path=keys/servicenow/pass
project.plugin.WorkflowStep.Service-Now-Incident-Create.url=https://server.service-now.com
```

</div>

## ServiceNow / Incident / Edit

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Incident-Edit.login=admin
project.plugin.WorkflowStep.Service-Now-Incident-Edit.password-key-storage-path=keys/servicenow/pass
project.plugin.WorkflowStep.Service-Now-Incident-Edit.url=https\://dev63229.service-now.com
```

</div>

## ServiceNow / Incident / View

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Incident-View.login=admin
project.plugin.WorkflowStep.Service-Now-Incident-View.password=keys/servicenow/pass
project.plugin.WorkflowStep.Service-Now-Incident-View.url=https\://dev63229.service-now.com
```

</div>

## ServiceNow / Change / Check State

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Change-Check-State.url=https://server.service-now.com
project.plugin.WorkflowStep.Service-Now-Change-Check-State.login=user
project.plugin.WorkflowStep.Service-Now-Change-Check-State.password-key-storage-path=keys/servicenow/pass
```

</div>

## ServiceNow / Change / Update State

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Change-Update-State.url=https://server.service-now.com
project.plugin.WorkflowStep.Service-Now-Change-Update-State.login=user
project.plugin.WorkflowStep.Service-Now-Change-Update-State.password-key-storage-path=keys/servicenow/pass
```

</div>

## ServiceNow / Change / Create

<div class="language-text line-numbers-mode">

``` text
project.plugin.WorkflowStep.Service-Now-Change-Create.url=https://server.service-now.com
project.plugin.WorkflowStep.Service-Now-Change-Create.login=user
project.plugin.WorkflowStep.Service-Now-Change-Create.password-key-storage-path=keys/servicenow/pass
```

</div>
