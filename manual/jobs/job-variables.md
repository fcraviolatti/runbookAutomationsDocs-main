---
title: "Job Variables Reference"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-variables.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Job Variables Reference

## Overview

When a Job step is executed, it has access to a set of "context variables" that provide information about the Job, execution environment, nodes, and runtime data. These variables can be referenced in Job steps, scripts, commands, and configuration fields throughout Rundeck.

This page serves as a comprehensive reference for all variable types, their syntax, and usage patterns.

## Variable Categories

Variables in Rundeck are organized into several categories:

- **[Job Context Variables](#job-context-variables)** - Information about the current Job
- **[Node Context Variables](#node-context-variables)** - Information about the target node
- **[Option Context Variables](#option-context-variables)** - User-provided input values
- **[Step Execution Variables](#step-execution-context-variables)** - Information about step execution results
- **[Error Handler Variables](#error-handler-context-variables)** - Information about step failures
- **[Execution Context Variables](#execution-context-variables)** - Information about the execution (primarily for notifications)
- **[Data Variables](#data-variables)** - Captured data from log filters
- **[Webhook Variables](#webhook-context-variables)** - Data from webhook triggers
- **[Project Variables](#project-global-variables)** - Project-level global variables

## Variable Syntax

Variables can be referenced using different syntax depending on where they are used:

### Commands and Arguments

Use the `${variable.name}` syntax in:

- Command steps
- Script arguments
- Job reference arguments
- Configuration fields

<div class="language-bash line-numbers-mode">

``` bash
echo "Job name: ${job.name}"
echo "Node hostname: ${node.hostname}"
echo "Option value: ${option.myoption}"
```

</div>

### Inline Script Content

Use the `@variable.name@` syntax within inline script content:

<div class="language-bash line-numbers-mode">

``` bash
#!/bin/bash
echo "Running on @node.hostname@"
echo "Job ID: @job.id@"
```

</div>

> **Note**
>
> The `@variable.name@` expansion is **not** available for "Script File" steps. Script files are not rewritten when executed.

> **Tips**
>
> This can be disabled. See [Administrator Guide \> Configuration File Reference \> framework.properties](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#framework-properties).

### Environment Variables

All context variables are also exported as environment variables with the following transformation:

- All letters become uppercase
- Punctuation is replaced with underscore
- The name is prefixed with `RD_`

<div class="language-bash line-numbers-mode">

``` bash
# Using environment variable syntax
echo $RD_JOB_NAME
echo $RD_NODE_HOSTNAME
echo $RD_OPTION_MYOPTION
```

</div>

> **Note**
>
> See the chapter [Configuring Remote Machine for SSH](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html#configuring-remote-machine-for-ssh) for information about SSH server requirements.

## Context Variables Reference

### Job Context Variables

Job context variables provide information about the current Job and execution. These are **Global Scope** variables available to all workflow steps.

| Variable                | Description                                                                                                                              |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| `job.name`              | Name of the Job                                                                                                                          |
| `job.group`             | Group of the Job                                                                                                                         |
| `job.id`                | ID of the Job                                                                                                                            |
| `job.url`               | URL to the Job/execution data                                                                                                            |
| `job.execid`            | ID of the current Execution                                                                                                              |
| `job.outputfilepath`    | Path to the log file for the current execution (can be local or remote)                                                                  |
| `job.isRemoteFilePath`  | Flag (`"true"`, `"false"`) indicating if `outputfilepath` is remote or local                                                             |
| `job.execIdForLogStore` | Execution ID of the log file (may differ if execution was imported)                                                                      |
| `job.executionType`     | Execution type: `user`, `scheduled`, or `user-scheduled` (for Run Job Later)                                                             |
| `job.user.name`         | Username of the user executing the Job                                                                                                   |
| `job.user.email`        | Email address of the executing user from their [User profile](https://docs.rundeck.com/docs/manual/10-user.html)                         |
| `job.project`           | Project name                                                                                                                             |
| `job.loglevel`          | Logging level: `ERROR`, `WARN`, `INFO`, `VERBOSE`, or `DEBUG`                                                                            |
| `job.retryAttempt`      | Number indicating the retry attempt (see [Retry](https://docs.rundeck.com/docs/manual/jobs/job-workflows.html#retry))                    |
| `job.wasRetry`          | `true` if this execution is a retry, otherwise `false` (see [Retry](https://docs.rundeck.com/docs/manual/jobs/job-workflows.html#retry)) |
| `job.threadcount`       | Threadcount (number of nodes run at once)                                                                                                |
| `job.filter`            | The filter used to select nodes for this job                                                                                             |

**Example Usage:**

<div class="language-bash line-numbers-mode">

``` bash
# Command step
echo "Running ${job.name} in project ${job.project}"

# Environment variable
echo "Job ID: $RD_JOB_ID"
```

</div>

### Node Context Variables

Node context variables provide information about the target node. These are **Node Scope** variables, meaning each node has its own set of values.

| Variable           | Description                                    |
|--------------------|------------------------------------------------|
| `node.name`        | Name of the Node being executed on             |
| `node.hostname`    | Hostname of the Node                           |
| `node.username`    | Username of the remote user                    |
| `node.description` | Description of the node                        |
| `node.tags`        | Comma-separated list of tags                   |
| `node.os-name`     | Operating system name                          |
| `node.os-version`  | Operating system version                       |
| `node.os-arch`     | Operating system architecture                  |
| `node.os-family`   | Operating system family                        |
| `node.*`           | Any custom Node attributes defined on the Node |

**Example Usage:**

<div class="language-bash line-numbers-mode">

``` bash
# Command step
echo "Executing on ${node.hostname} (${node.os-family})"

# Inline script
@node.name@ - @node.description@
```

</div>

### Option Context Variables

Option context variables contain values provided by users when running a Job, either through the GUI, API, or webhook.

Options are referenced as `option.NAME` where `NAME` is the option name defined in the Job.

**Example Usage:**

<div class="language-bash line-numbers-mode">

``` bash
# Command step
echo "User provided: ${option.environment}"
echo "Server: ${option.server_name}"

# Inline script
#!/bin/bash
ENV="@option.environment@"
SERVER="@option.server_name@"
```

</div>

See [Job Options](https://docs.rundeck.com/docs/manual/jobs/job-options.html) for more information about defining and using options.

### Step Execution Context Variables

Step execution variables provide information about the exit code of previous steps. These are **Global Scope** variables.

**Syntax:** `#:exec.exitCode@<node>`

Where `#` is the step number.

**Examples:**

| Variable                      | Description                                         |
|-------------------------------|-----------------------------------------------------|
| `${2:exec.exitCode}`          | Exit code for step 2 on the current node            |
| `${2:exec.exitCode*}`         | Exit code for step 2 on all nodes (comma-separated) |
| `${2:exec.exitCode@nodename}` | Exit code for step 2 on a specific node             |

**Example Usage:**

<div class="language-bash line-numbers-mode">

``` bash
# Check if step 1 succeeded
if [ "${1:exec.exitCode}" -eq "0" ]; then
  echo "Step 1 succeeded"
fi
```

</div>

### Error Handler Context Variables

When an Error Handler step is executed, additional context variables are available to provide information about the failure. These are **Global Scope** variables.

| Variable             | Description                                                                |
|----------------------|----------------------------------------------------------------------------|
| `result.reason`      | A code indicating why the step failed                                      |
| `result.message`     | A string describing the failure                                            |
| `result.resultCode`  | Exit code from the execution (if available)                                |
| `result.failedNodes` | Comma-separated list of node names that failed (for `NodeDispatchFailure`) |

#### Common Reason Codes

**Node Execution Failures:**

- `NonZeroResultCode` - The execution returned a non-zero code
- `SSHProtocolFailure` - SSH protocol failure
- `HostNotFound` - Host not found
- `ConnectionTimeout` - Connection timeout
- `ConnectionFailure` - Connection failure (e.g. refused)
- `IOFailure` - IO error
- `AuthenticationFailure` - Authentication was refused or incorrect

**Job Reference Failures:**

- `JobFailed` - Referenced Job workflow failed
- `NotFound` - Referenced Job not found
- `Unauthorized` - Referenced Job not authorized
- `InvalidOptions` - Referenced Job input options invalid
- `NoMatchedNodes` - Referenced Job node dispatch filters had no match

**Node Step Failures (when handler is a Workflow Step):**

- `NodeDispatchFailure` - One or more nodes failed the step

**Example Usage:**

<div class="language-bash line-numbers-mode">

``` bash
# Error handler command
echo "Step failed with reason: ${result.reason}"
echo "Failed nodes: ${result.failedNodes}"
echo "Message: ${result.message}"
```

</div>

See the [Error Handlers](https://docs.rundeck.com/docs/manual/jobs/job-workflows.html#error-handlers) section for more information.

### Execution Context Variables

Execution context variables contain detailed information about the Job execution. These are **Global Scope** variables.

> **Important**
>
> The `execution.*` variables are only available in the [Notification context](https://docs.rundeck.com/docs/developer/notification-plugins.html#execution-data). They are **not** available while a Job is running or as part of Job Steps.

| Variable                        | Description                                                     |
|---------------------------------|-----------------------------------------------------------------|
| `execution.id`                  | ID of the execution                                             |
| `execution.href`                | URL to the execution output view                                |
| `execution.status`              | Execution state: `running`, `failed`, `aborted`, or `succeeded` |
| `execution.user`                | User who started the job                                        |
| `execution.dateStarted`         | Start time (java.util.Date)                                     |
| `execution.dateStartedUnixtime` | Start time as milliseconds since epoch (long)                   |
| `execution.dateStartedW3c`      | Start time as a W3C formatted String                            |
| `execution.description`         | Summary string for the execution                                |
| `execution.argstring`           | Argument string for any job options                             |
| `execution.project`             | Project name                                                    |
| `execution.loglevel`            | Loglevel string: `ERROR`, `WARN`, `INFO`, `VERBOSE`, or `DEBUG` |

**Available after job completion** (not available for `onstart` trigger):

| Variable                            | Description                                                       |
|-------------------------------------|-------------------------------------------------------------------|
| `execution.failedNodeListString`    | Comma-separated list of nodes that failed                         |
| `execution.failedNodeList`          | Java List of node names that failed                               |
| `execution.succeededNodeListString` | Comma-separated list of nodes that succeeded                      |
| `execution.succeededNodeList`       | Java List of node names that succeeded                            |
| `execution.nodestatus`              | Java Map with counts: `[succeeded: int, failed: int, total: int]` |
| `execution.dateEnded`               | End time (java.util.Date)                                         |
| `execution.dateEndedUnixtime`       | End time as milliseconds since epoch (long)                       |
| `execution.dateEndedW3c`            | End time as W3C formatted string                                  |
| `execution.abortedby`               | User who aborted the execution                                    |

### Data Variables

Data variables are captured during Job execution using [Log Filter Plugins](#data-capture-log-filter-plugins). They store values extracted from command or script output that can be used in subsequent steps.

Data variables are stored in groups (typically the `data` group) and are referenced as `data.NAME` where `NAME` is the key defined in the log filter.

**Example Usage:**

<div class="language-bash line-numbers-mode">

``` bash
# Step 1: Capture data using Key Value Data log filter
# Command outputs: RUNDECK:DATA:server_ip=192.168.1.100

# Step 2: Use the captured data
echo "Server IP: ${data.server_ip}"
ping -c 1 ${data.server_ip}
```

</div>

> **Tips**
>
> Data variables may be captured in either **Global Scope** or **Node Scope** depending on the step type. See [Variable Scopes](#variable-scopes) for details.

See [Data Capture Log Filter Plugins](#data-capture-log-filter-plugins) for more information.

### Webhook Context Variables

When a Job is triggered by a webhook, additional context variables are available:

| Variable            | Description                                        |
|---------------------|----------------------------------------------------|
| `webhook.id`        | Unique event ID                                    |
| `webhook.project`   | The project that owns the webhook                  |
| `webhook.sender`    | The IP address of the sending system               |
| `webhook.timestamp` | The epoch milliseconds when the event was received |

**Example Usage:**

<div class="language-bash line-numbers-mode">

``` bash
echo "Webhook triggered from ${webhook.sender} at ${webhook.timestamp}"
```

</div>

See [Webhooks](https://docs.rundeck.com/docs/manual/webhooks/run-job.html) for more information.

### Project Global Variables

Projects can define global variables in their configuration that are available to all Jobs in that project.

Project variables are defined in the project configuration file using the format:

<div class="language-text line-numbers-mode">

``` text
project.globals.VARIABLE_NAME=value
```

</div>

They are referenced in Jobs as `globals.VARIABLE_NAME`:

**Example:**

Project configuration:

<div class="language-properties line-numbers-mode">

``` properties
project.globals.apiEndpoint=https://api.example.com
project.globals.environment=production
```

</div>

Job usage:

<div class="language-bash line-numbers-mode">

``` bash
curl ${globals.apiEndpoint}/status
echo "Environment: ${globals.environment}"
```

</div>

## Variable Scopes

Understanding variable scopes is critical for correctly referencing data in your workflows.

### Global Scope

Variables in the **Global Scope** are available to all types of Workflow steps throughout the entire Job execution.

**Global Scope variables include:**

- `job.*` variables
- `execution.*` variables (notifications only)
- `option.*` variables
- `webhook.*` variables
- `globals.*` variables
- Variables added to Global Context by Workflow Steps

### Node Scope

Variables in a **Node Scope** are bound to a particular Node Name. There can be multiple Node Scopes within a single execution (one per node).

**Node Scope variables include:**

- `node.*` variables
- `data.*` variables captured by Node Steps

Variables captured within a Node Step are stored in that node's scope, allowing different nodes to have different values for the same variable name.

### Scope Resolution

When referencing a variable, Rundeck searches for it in the following order:

1.  **Current Scope** - If the reference is in a Node Step, it checks the Node Scope first
2.  **Widened Scope** - If not found, the scope is "widened" to search parent scopes
3.  **Global Scope** - Eventually reaching the Global Scope

This means you can always reference Global Scope variables using normal syntax, even from within Node Steps.

### Cross-Scope References

You can explicitly reference variables from different scopes using special syntax:

#### Reference a Specific Node

Use `@nodename` to reference a variable from a specific node's scope:

<div class="language-bash line-numbers-mode">

``` bash
${data.status@webserver01}
${data.disk_usage@database-primary}
```

</div>

#### Reference All Nodes

Use `*` to collect values from all Node Scopes:

<div class="language-bash line-numbers-mode">

``` bash
# Comma-separated values from all nodes
${data.status*}
# Example result: "running,running,stopped"
```

</div>

#### Custom Delimiter

Add a delimiter character after the `*`:

<div class="language-bash line-numbers-mode">

``` bash
# Semicolon-separated
${data.status*;}
# Result: "running;running;stopped"

# Newline-separated
${data.status*
}

# Dash-separated
${data.status*-}
# Result: "running-running-stopped"
```

</div>

### Scope Best Practices

> **Tips**
>
> If a variable reference does not produce the expected value, verify that:
>
> 1.  The variable's Scope matches the reference point's Scope
> 2.  For Node Scope variables, you're using the correct node reference syntax
> 3.  The variable has been set before it's being referenced
>
> Use the **Log Data** Workflow Step to visualize all available context variables at any point in your workflow.

> **Workflow Strategy Impact**
>
> The Workflow Strategy affects when steps execute and therefore which variables are available:
>
> - **Sequential Strategy**: Each step completes on all nodes before the next step begins. Step 2 can reference any value from Step 1, even from different nodes.
> - **Node-First Strategy**: The entire workflow runs on each node before moving to the next node.
> - **Parallel Strategy**: Steps may execute simultaneously, so timing affects availability.
> - **Ruleset Strategy**: Custom rules determine execution order.
>
> Depending on the strategy, some captured values may or may not be present when referenced.
>
> See [Workflow Strategies](https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/) for more information.

## Data Capture Log Filter Plugins

Rundeck provides Log Filter plugins that can capture data from step output and make it available as variables in subsequent steps.

### Key Value Data

The Key Value Data log filter captures key-value pairs from step output using regular expressions.

**Default pattern:** `^RUNDECK:DATA:(.+?)\s*=\s*(.+)$`

This allows commands to output data in a simple format:

<div class="language-bash line-numbers-mode">

``` bash
echo "RUNDECK:DATA:status=success"
echo "RUNDECK:DATA:record_count=42"
```

</div>

These become available as `${data.status}` and `${data.record_count}` in later steps.

For more information, see [Key Value Data](https://docs.rundeck.com/docs/manual/log-filters/key-value-data.html).

### Multiline Regex Data Capture

The Multiline Regex Capture log filter can capture multiple lines of output into a single variable.

For more information, see [Multiline Regex Capture](https://docs.rundeck.com/docs/manual/log-filters/multi-line-regex.html).

### JQ JSON Filter

The JQ log filter can parse JSON output and extract values into variables.

For more information about all available log filters, see [Log Filters](https://docs.rundeck.com/docs/manual/log-filters/).

## Exporting Variables

### Global Variable Workflow Step

The **Global Variable** workflow step allows you to export variables from Node Scope to Global Scope, making them available to subsequent Workflow Steps and to parent Jobs when using Job References.

This is particularly useful for:

- Making node-specific data available globally
- Passing data from a child Job to a parent Job
- Collecting values from multiple nodes into a single variable

**Key features:**

- Export to the `export` group for parent Jobs: `${export.myvar}`
- Export to the `data` group for current Job: `${data.myvar}`
- Collect values from all nodes: `${data.myvar*}`
- Collect from specific node: `${data.myvar@nodename}`

For detailed information and examples, see [Global Variable Workflow Step](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#global-variable).

### Result Data Plugins (Enterprise)

> **Available in PagerDuty Runbook Automation Commercial products.**

Result Data plugins allow Jobs to export structured JSON data as the result of an execution, which can be retrieved via the API and displayed in the GUI.

For more information, see [Result Data](https://docs.rundeck.com/docs/manual/jobs/result-data.html).

## Variable Expansion in Special Contexts

### Option Remote Values URLs

When defining Option values loaded from a remote URL, you can embed variables in the URL that will be expanded when the URL is called.

**Available variables for Remote Option URLs:**

| Variable                | Description                                                   |
|-------------------------|---------------------------------------------------------------|
| `${job.name}`           | Name of the Job                                               |
| `${job.group}`          | Group of the Job                                              |
| `${job.description}`    | Job description                                               |
| `${job.project}`        | Project name                                                  |
| `${job.user.name}`      | User executing the job                                        |
| `${rundeck.nodename}`   | Name of the Rundeck server node                               |
| `${rundeck.serverUUID}` | UUID of the Rundeck server (cluster mode)                     |
| `${rundeck.basedir}`    | File path of the Rundeck base directory (`file://` URLs only) |
| `${option.NAME}`        | Value of another option (for cascading options)               |

**Example:**

<div class="language-text line-numbers-mode">

``` text
https://api.example.com/servers?project=${job.project}&env=${option.environment}
```

</div>

See [Job Options - Variable Expansion](https://docs.rundeck.com/docs/manual/jobs/job-options.html#variable-expansion-in-remote-urls) for more details.

### Notification Context

Notifications have access to both `execution.*` and `job.*` variables, plus any configuration properties with embedded references.

See [Notification Plugins](https://docs.rundeck.com/docs/developer/notification-plugins.html#execution-data) for more information.

## Troubleshooting Variables

### Common Issues

**Problem: Variable shows as empty or undefined**

Possible causes:

1.  The variable hasn't been set yet (check execution order)
2.  Scope mismatch (Node Scope vs Global Scope)
3.  Typo in variable name
4.  Variable only available in certain contexts (e.g., `execution.*` in notifications only)

**Solution:** Use the **Log Data** workflow step to see all available variables at that point.

**Problem: Node Scope variable not accessible in Workflow Step**

**Solution:** Use the [Global Variable](#global-variable-workflow-step) workflow step to export the Node Scope data to Global Scope first.

**Problem: Variables from multiple nodes showing concatenated**

**Solution:** This is expected when using `${data.var*}` syntax. Use specific node syntax `${data.var@nodename}` or change your delimiter `${data.var*;}`.

### Debugging Variables

**Log Data Step**

Add a **Log Data** workflow step to output all available context variables:

1.  Add a Workflow Step
2.  Select "Log Data"
3.  Run the Job

This will show all variables and their values at that point in the workflow, helping you identify scope and availability issues.

**Echo in Steps**

Add debug commands to output variable values:

<div class="language-bash line-numbers-mode">

``` bash
echo "DEBUG: job.name = ${job.name}"
echo "DEBUG: data.myvar = ${data.myvar}"
echo "DEBUG: node.hostname = ${node.hostname}"
```

</div>

## Related Documentation

- [Job Workflows](https://docs.rundeck.com/docs/manual/jobs/job-workflows.html) - Overview of workflow execution
- [Job Options](https://docs.rundeck.com/docs/manual/jobs/job-options.html) - Defining and using input options
- [Log Filters](https://docs.rundeck.com/docs/manual/log-filters/) - All available log filter plugins
- [Key Value Data](https://docs.rundeck.com/docs/manual/log-filters/key-value-data.html) - Capturing data from output
- [Workflow Steps](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html) - Built-in workflow steps including Global Variable
- [Webhooks](https://docs.rundeck.com/docs/manual/webhooks/run-job.html) - Webhook variables and usage
- [Notification Plugins](https://docs.rundeck.com/docs/developer/notification-plugins.html) - Variables in notification context
- [Workflow Strategies](https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/) - How strategy affects variable availability

## Quick Reference

### Syntax Cheat Sheet

| Context              | Syntax               | Example                |
|----------------------|----------------------|------------------------|
| Command/Argument     | `${group.name}`      | `${job.name}`          |
| Inline Script        | `@group.name@`       | `@option.env@`         |
| Environment Variable | `$RD_GROUP_NAME`     | `$RD_JOB_NAME`         |
| Specific Node        | `${group.name@node}` | `${data.status@web01}` |
| All Nodes (comma)    | `${group.name*}`     | `${data.status*}`      |
| All Nodes (custom)   | `${group.name*X}`    | `${data.status*;}`     |

### Common Variable Groups

| Group         | Example               | Description                             |
|---------------|-----------------------|-----------------------------------------|
| `job.*`       | `${job.name}`         | Current Job information                 |
| `node.*`      | `${node.hostname}`    | Target node information                 |
| `option.*`    | `${option.env}`       | User input options                      |
| `data.*`      | `${data.result}`      | Captured data from log filters          |
| `export.*`    | `${export.value}`     | Exported global variables               |
| `globals.*`   | `${globals.apiUrl}`   | Project global variables                |
| `webhook.*`   | `${webhook.sender}`   | Webhook trigger information             |
| `execution.*` | `${execution.status}` | Execution details (notifications only)  |
| `result.*`    | `${result.reason}`    | Error information (error handlers only) |
