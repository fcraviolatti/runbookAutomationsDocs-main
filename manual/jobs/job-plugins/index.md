---
title: "Job Step Plugins"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Job Step Plugins

Jobs are composed of *steps* that define the actions to be taken against target nodes, tools or data.

## Understanding Step Types

There are two fundamental types of steps in Runbook Automation Jobs, and understanding the distinction is critical for building effective workflows:

### Node Steps

**Node Steps** are designed to iterate across one or more target endpoints and execute once for each matched node.

**Characteristics:**

- Execute on each node that matches the Job's node filter
- Run in a **Node Context** with access to node-specific variables (`node.hostname`, `node.name`, etc.)
- Capture data in **Node Scope**, meaning each node can have different values for the same variable
- Examples: Commands, scripts, file operations, node-specific API calls

**Common Node Steps:**

- Execute a command on multiple servers
- Run a script against a database cluster
- Copy files to remote nodes
- Query node-specific metrics

**Variable Scoping:** When a Node Step captures data (via log filters), that data is stored in the Node's scope. To reference data from a specific node, use: `${data.variable@nodename}`. To collect values from all nodes, use: `${data.variable*}`.

See [Job Variables Reference - Node Scope](https://docs.rundeck.com/docs/manual/jobs/job-variables.html#node-scope) for more details.

### Workflow Steps

**Workflow Steps** execute exactly once per Job invocation and do not operate in a node context.

**Characteristics:**

- Execute only once, regardless of how many nodes are targeted
- Run on the Rundeck server (not dispatched to remote nodes)
- Run in a **Global Context** without access to node-specific variables
- Can access data from Node Steps, but must specify which node's data to use
- Examples: Orchestration logic, global state changes, API integrations

**Common Workflow Steps:**

- Update a load balancer configuration
- Send notifications
- Refresh the project's node cache
- Export captured data from multiple nodes
- Make decisions based on aggregate node results

**Variable Scoping:** Workflow Steps capture data in Global Scope, making it available to all subsequent steps. To access Node Scope data from a Workflow Step, you must explicitly reference it: `${data.variable@nodename}` or collect all values: `${data.variable*}`.

See [Job Variables Reference - Global Scope](https://docs.rundeck.com/docs/manual/jobs/job-variables.html#global-scope) for more details.

### Execution Order

The order in which steps execute is determined by the [Workflow Strategy](https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/):

- **Node-First Strategy** (default): Each node runs all steps before moving to the next node
- **Sequential Strategy**: Each step runs on all nodes before moving to the next step
- **Parallel Strategy**: Steps run simultaneously across nodes

When mixing Node Steps and Workflow Steps (which is common):

- Node Steps may execute multiple times (once per node)
- Workflow Steps execute only once
- The execution order follows the workflow strategy
- Workflow Steps can access aggregated data from all Node Steps that executed before them

**Example Workflow:**

<div class="language-text line-numbers-mode">

``` text
Step 1: Node Step - Check disk space on all web servers
Step 2: Workflow Step - Determine which server has the most free space
Step 3: Node Step - Deploy application to the server with most space
Step 4: Workflow Step - Update load balancer to include new deployment
```

</div>

For more information on building workflows, see [Job Workflows](https://docs.rundeck.com/docs/manual/jobs/job-workflows.html).

## Node Steps

- [AWS Node Steps](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/aws.html)
- [Azure Node Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/azure.html)
- [Google Cloud Platform Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/gcp.html)
- [Oracle Cloud Node Steps plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/oracle.html)
- [Datadog Node Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/datadog.html)
- [Jira Node Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/jira.html)
- [Sensu Node Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/sensu.html)
- [SQL Runner (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/sqlrunner.html)
- [VMWare Operations Node Step Plugin (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/vmware.html)
- [Command step](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#command-step)
- [Script step](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#script-step)
- [Script file](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#script-file-step)
- [Script URL](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#script-url-step)
- [Job reference](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#job-reference-step)
- [Copy file](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#copy-file-step)
- [Local command](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#local-command-step)
- [Data node](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#data-node-step)
- [HTTP Request](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#http-node-step)
- [Loop Script Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/loop-plugins.html)

## Workflow Steps

- **Amazon Web Services (Enterprise Only)**
  - [Athena Query](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/amazon-athena.html)
  - [CloudWatch Logs](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch.html)
  - [ECS & Fargate](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-ecs-fargate.html)
  - [Elastic Cloud Compute (EC2)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws.html)
  - [Elastic Load Balancer (ELB)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-elb-workflow-plugin.html)
  - [Lambda](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-lambda.html)
  - [RDS](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-rds.html)

<!-- -->

- [Azure Job Steps (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/azure.html)
- [Google Cloud Platform (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/gcp.html)
- [Oracle Cloud Infrastructure(Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/oracle.html)
- [Datadog Workflow Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/datadog.html)
- [File Transfer (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/file-transfer.html)
- [Github (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/github.html)
- [Jira Workflow Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/jira.html)
- [PagerDuty (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/pagerduty.html#pager-duty-job-steps-enterprise)
- [Progress Badge (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/progress-badge.html#progress-badge-workflow-step-plugin)
- [Sensu Workflow Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/sensu.html)
- [ServiceNow (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/servicenow.html)
- [VMWare Step Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/vmware.html)
- [Ansible module](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#ansible-module)
- [Ansible playbook inline](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#ansible-playbook-inline)
- [Ansible playbook](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#ansible-playbook)
- [Global variable](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#global-variable)
- [Flow control](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#flow-control)
- [Job state conditional](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#job-state-conditional)
- [Log data step](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#log-data-step)
- [Refresh project nodes](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#refresh-project-nodes)
- [Data step](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/builtin.html#data-step)
- [Sumo Logic (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/sumo-logic.html)
- [Loop Script Plugins (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/loop-plugins.html)
- [RSS Feed Plugin (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/rss-feed-plugin.html)
- [MongoDB Command Runner](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/mongodb.html)

## Notifications

Notification plugins allow Rundeck to communicate changes in job execution state and notify other users of successful or failed runs. For a general explanation on how job notifications work, see [Job Notifications](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html#job-notifications).

- [Jira Notification Plugins (Commercial)](https://docs.rundeck.com/docs/manual/notifications/jira.html)
- [Datadog Notification Plugin (Commercial)](https://docs.rundeck.com/docs/manual/notifications/datadog.html)
- [PagerDuty Notification Plugin (Commercial)](https://docs.rundeck.com/docs/manual/notifications/pagerduty.html)
- [ServiceNow Notification Plugin (Commercial)](https://docs.rundeck.com/docs/manual/notifications/servicenow.html)
- [Slack Notification Plugin (Commercial)](https://docs.rundeck.com/docs/manual/notifications/slack.html)
- [Email](https://docs.rundeck.com/docs/manual/notifications/email.html)
- [Webhooks](https://docs.rundeck.com/docs/manual/notifications/webhooks.html)

For directions on how to use the Notification interface, see [here](https://docs.rundeck.com/docs/manual/notifications/interface-instructions.html).

## Option Plugins

Option Plugins provide dynamic Allowed Value lists to help choose the proper inputs for your jobs. For general overview of how Options work see [Job Options](https://docs.rundeck.com/docs/manual/jobs/job-options.html)

- [Jira Option Plugins](https://docs.rundeck.com/docs/manual/option-plugins/jira.html)

## Workflow Strategy

The Workflow Strategy determines how the steps are processed within a Job's Workflow.

- [Ruleset (Commercial)](https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/ruleset.html)

## Node Orchestrator

Typically, Rundeck processes nodes in the exact order that they are specified within a Job definition. An *Orchestrator Plugin* allows this run order to be modified by selecting a subset of nodes. This would be useful in order to limit concurrent executions during a deployment or gradually role out a new job to allow for testing.

The Bundled plugins support random selection, ordering by ranked tier, or specifying a percentage of nodes to target. If more logic or specificity is required, the Enterprise edition supports the selection of a single node based upon the value of an attribute.

- [Highest/Lowest Attribute Value (Commercial)](https://docs.rundeck.com/docs/manual/orchestrator-plugins/highest-lowest.html)
- [Bundled Orchestrator Plugins](https://docs.rundeck.com/docs/manual/orchestrator-plugins/bundled.html)

## Log Filters

Log Filters can transform or aggregate output from one or more Workflow states.

- [Mask Passwords](https://docs.rundeck.com/docs/manual/log-filters/mask-passwords.html)
- [Render Formatted Data](https://docs.rundeck.com/docs/manual/log-filters/render-formatted-data.html)
- [Key Value Data](https://docs.rundeck.com/docs/manual/log-filters/key-value-data.html)
- [Quiet Output](https://docs.rundeck.com/docs/manual/log-filters/quiet-output.html)
- [Highlight Output](https://docs.rundeck.com/docs/manual/log-filters/highlight-output.html)
- [Progress Badge](https://docs.rundeck.com/docs/manual/log-filters/progress-badge.html)
- [Store and Validate JSON (Commercial)](https://docs.rundeck.com/docs/manual/log-filters/loop-plugins.html)

## Content Converters

Content Converters are not added directly to Jobs, but can be used by Log Filters and Step plugins to render log output as HTML or Markdown within the Rundeck User Interface.

See [Content Converter Plugins](https://docs.rundeck.com/docs/manual/content-converters/).

## Execution Lifecycle

See [Execution Lifecycle Plugins](https://docs.rundeck.com/docs/manual/execution-lifecycle/).
