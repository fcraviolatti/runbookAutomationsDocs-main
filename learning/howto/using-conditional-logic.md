---
title: "Using Conditional Logic in a Job"
source_url: https://docs.rundeck.com/docs/learning/howto/using-conditional-logic.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Using Conditional Logic in a Job

**Early Access Feature** - Available in Runbook Automation 5.20.0+

## Overview

Conditional Logic steps enable workflows to make decisions during execution based on runtime conditions. Instead of creating multiple jobs for different scenarios or writing complex scripts with if/then logic, you can use Conditional Logic steps to branch your workflow based on:

- Job options (environment, configuration values)
- Node attributes (OS family, hostname, tags)
- Job context (project name, job name, execution user)
- Data captured from previous steps

This guide provides hands-on examples to help you understand how to use conditional logic effectively.

## Prerequisites

1.  **Runbook Automation 5.20.0+** with the conditional logic feature enabled
2.  **Feature flag enabled** in `rundeck-config.properties`:
    <div class="language-properties line-numbers-mode">

    ``` properties
    rundeck.feature.earlyAccessJobConditional.enabled=true
    ```

    </div>
3.  **Basic understanding** of job workflows and job options
4.  **Workflow strategy** set to Sequential or Parallel (not Node First or Ruleset)

> **New to Rundeck?**
>
> If you're new to Rundeck, we recommend completing the [Getting Started Tutorial](https://docs.rundeck.com/docs/learning/tutorial/) first. This guide assumes familiarity with creating jobs, adding steps, and using job options.

## Understanding Conditional Logic

Conditional Logic steps come in two types:

- **Node Conditional Logic**: Evaluates conditions independently on each node based on node attributes
- **Workflow Conditional Logic**: Evaluates conditions once per job execution in a global context

Both types support:

- Multiple conditions with AND logic (all must be true)
- Multiple condition sets with OR logic (any set can be true)
- Various operators: equals, not equals, contains, matches (regex), greater than, less than

## Hands-On Examples

The following examples demonstrate conditional logic in action. Import these jobs to see how conditions work, then run them with different option values to observe the behavior.

Simple Conditional Example

Complex Conditional Example

Simple Conditional Example

This example demonstrates a basic conditional step that executes only when a specific version is selected.

**Use Case:** Run deployment steps only for version 5.20

**What This Job Does:**

1.  Accepts a `version` option as input
2.  Uses a Node Conditional Logic step to check if version equals "5.20"
3.  If the condition is true, executes an echo command
4.  If the condition is false, skips the substep

**Condition Structure:**

- **Field:** `${option.version}`
- **Operator:** `equals`
- **Value:** `5.20`

**Job Definition (JSON):**

<div class="language-json line-numbers-mode">

``` json
[ {
  "defaultTab" : "nodes",
  "description" : "Simple example showing a single condition checking a job option value.",
  "executionEnabled" : true,
  "loglevel" : "INFO",
  "name" : "Simple Conditional Example",
  "nodeFilterEditable" : false,
  "nodefilters" : {
    "dispatch" : {
      "excludePrecedence" : true,
      "keepgoing" : false,
      "rankOrder" : "ascending",
      "successOnEmptyNodeFilter" : false,
      "threadcount" : "1"
    },
    "filter" : ".*"
  },
  "nodesSelectedByDefault" : true,
  "options" : [ {
    "name" : "version",
    "label" : "Version",
    "description" : "Enter a version number (try 5.20 or 5.19)",
    "type" : "text",
    "required" : true
  } ],
  "scheduleEnabled" : true,
  "schedules" : [ ],
  "sequence" : {
    "commands" : [ {
      "conditionGroups" : [ [ {
        "key" : "${option.version}",
        "operator" : "==",
        "value" : "5.20"
      } ] ],
      "description" : "Check if version is 5.20",
      "nodeStep" : true,
      "subSteps" : [ {
        "exec" : "echo 'Running deployment for version 5.20'"
      } ],
      "type" : "conditional"
    } ],
    "keepgoing" : false,
    "strategy" : "sequential"
  }
} ]
```

</div>

**How to Use This Example:**

1.  Copy the JSON above and save it as `simple-conditional-example.json`
2.  Import the job into your Rundeck project:
    - Navigate to the Jobs page
    - Click the gear icon and select "Import Job"
    - Upload the JSON file
3.  Run the job and enter `5.20` for the version option
    - The conditional step will evaluate to true
    - The echo command will execute
4.  Run the job again and enter `5.19` for the version option
    - The conditional step will evaluate to false
    - The substep will be skipped
    - Check the execution log to see the skip message

**What to Observe:**

- In the Job Editor, expand the conditional step to see the condition configuration
- In execution logs when condition is **true**: You'll see the echo output
- In execution logs when condition is **false**: You'll see a message like "Conditional step skipped"
- Enable Debug logging to see detailed condition evaluation

**Key Takeaways:**

- Fields must use `${}` syntax to reference variables
- The operator `==` is equivalent to "equals"
- Substeps only execute when the condition evaluates to true
- Simple conditionals are perfect for single-criteria decisions

Complex Conditional Example

This example demonstrates advanced conditional logic using multiple condition sets with OR logic and multiple conditions per set with AND logic.

**Use Case:** Run deployment steps in specific scenarios:

- Always run in Dev environment, OR
- Run on Windows servers (but skip version 5.20), OR
- Run on Linux servers (but skip version 5.19)

**What This Job Does:**

1.  Accepts three options: `environment`, `os`, and `version`
2.  Uses a Node Conditional Logic step with three condition sets (OR logic)
3.  Each condition set can have multiple conditions (AND logic)
4.  Executes substeps when ANY condition set evaluates to true

**Condition Structure:**

**Condition Set 1:** Dev environment

- Field: `${option.environment}` Operator: `equals` Value: `Dev`

**OR**

**Condition Set 2:** Windows + not version 5.20

- Field: `${option.os}` Operator: `equals` Value: `Windows`
- **AND** Field: `${option.version}` Operator: `not equals` Value: `5.20`

**OR**

**Condition Set 3:** Linux + not version 5.19

- Field: `${option.os}` Operator: `equals` Value: `Linux`
- **AND** Field: `${option.version}` Operator: `not equals` Value: `5.19`

**Job Definition (JSON):**

<div class="language-json line-numbers-mode">

``` json
[ {
  "defaultTab" : "nodes",
  "description" : "Complex example showing multiple condition sets with OR logic and multiple conditions per set with AND logic.",
  "executionEnabled" : true,
  "loglevel" : "INFO",
  "name" : "Complex Conditionals",
  "nodeFilterEditable" : false,
  "nodefilters" : {
    "dispatch" : {
      "excludePrecedence" : true,
      "keepgoing" : false,
      "rankOrder" : "ascending",
      "successOnEmptyNodeFilter" : false,
      "threadcount" : "1"
    },
    "filter" : ".*"
  },
  "nodesSelectedByDefault" : true,
  "options" : [ {
    "label" : "Version",
    "name" : "version",
    "description" : "Application version",
    "type" : "text",
    "required" : true
  }, {
    "enforced" : true,
    "label" : "Environment",
    "name" : "environment",
    "required" : true,
    "type" : "text",
    "values" : [ "Prod", "Dev" ],
    "valuesListDelimiter" : ","
  }, {
    "enforced" : true,
    "label" : "Operating System",
    "name" : "os",
    "required" : true,
    "type" : "text",
    "values" : [ "Linux", "Windows" ],
    "valuesListDelimiter" : ","
  } ],
  "scheduleEnabled" : true,
  "schedules" : [ ],
  "sequence" : {
    "commands" : [ {
      "conditionGroups" : [ [ {
        "key" : "${option.environment}",
        "operator" : "==",
        "value" : "Dev"
      } ], [ {
        "key" : "${option.os}",
        "operator" : "==",
        "value" : "Windows"
      }, {
        "key" : "${option.version}",
        "operator" : "!=",
        "value" : "5.20"
      } ], [ {
        "key" : "${option.os}",
        "operator" : "==",
        "value" : "Linux"
      }, {
        "key" : "${option.version}",
        "operator" : "!=",
        "value" : "5.19"
      } ] ],
      "description" : "Check deployment conditions",
      "nodeStep" : true,
      "subSteps" : [ {
        "description" : "Output Variables",
        "exec" : "echo 'Deploying on ${option.os} version ${option.version} in ${option.environment}'"
      } ],
      "type" : "conditional"
    } ],
    "keepgoing" : false,
    "strategy" : "sequential"
  }
} ]
```

</div>

**How to Use This Example:**

1.  Copy the JSON above and save it as `complex-conditionals-example.json`
2.  Import the job into your Rundeck project
3.  Run the job with different option combinations to see how conditions evaluate

**Test Scenarios:**

Try these combinations to understand the OR/AND logic:

| Environment | OS      | Version | Will Execute? | Why?                                                                                    |
|-------------|---------|---------|---------------|-----------------------------------------------------------------------------------------|
| Dev         | Linux   | 5.20    | âœ… Yes       | Matches Set 1 (Dev environment)                                                         |
| Dev         | Windows | 5.19    | âœ… Yes       | Matches Set 1 (Dev environment)                                                         |
| Prod        | Windows | 5.19    | âœ… Yes       | Matches Set 2 (Windows AND not 5.20)                                                    |
| Prod        | Windows | 5.20    | â?Œ No        | Set 1 fails (Prod enviroment), Set 2 fails (version IS 5.20), Set 3 fails (not Linux)   |
| Prod        | Linux   | 5.20    | âœ… Yes       | Matches Set 3 (Linux AND not 5.19)                                                      |
| Prod        | Linux   | 5.19    | â?Œ No        | Set 1 fails (Prod enviroment), Set 2 fails (not Windows), Set 3 fails (version IS 5.19) |

**What to Observe:**

1.  **In the Job Editor:**

    - Expand the conditional step to see all three condition sets
    - Notice the OR separator between condition sets
    - Notice the AND logic within each set (multiple conditions in Set 2 and Set 3)

2.  **In Execution Logs:**

    - When conditions are met: You'll see the echo output with the selected values
    - When conditions are not met: You'll see "Conditional step skipped"
    - Enable Debug logging to see detailed evaluation of each condition and condition set

3.  **Debug Mode Output:**

    - Shows each condition being evaluated
    - Shows resolved variable values
    - Shows pass/fail for each condition
    - Shows which condition set (if any) matched

**Key Takeaways:**

- OR logic lets you define multiple scenarios where the step should execute
- AND logic within a set requires ALL conditions to be true
- Complex conditionals can handle sophisticated business logic without external scripts
- You can combine up to 5 conditions per set and up to 5 condition sets per step

## Real-World Use Cases

### Environment-Based Workflows

Use conditionals to run different steps based on environment:

<div class="language-text line-numbers-mode">

``` text
Workflow Conditional Logic: ${option.environment} equals "production"
ââ Substep: Send approval notification
ââ Substep: Backup database
ââ Substep: Enable maintenance mode
```

</div>

### OS-Specific Commands

Target specific operating systems without changing node filters:

<div class="language-text line-numbers-mode">

``` text
Node Conditional Logic: ${node.osFamily} equals "unix"
ââ Substep: Run Linux-specific commands

Node Conditional Logic: ${node.osFamily} equals "windows"
ââ Substep: Run Windows-specific commands
```

</div>

### Version-Aware Deployments

Skip or include steps based on application versions:

<div class="language-text line-numbers-mode">

``` text
Workflow Conditional Logic: ${option.version} greater than "5.0"
ââ Substep: Use new API endpoints
```

</div>

### Tag-Based Node Targeting

Execute steps only on nodes with specific tags:

<div class="language-text line-numbers-mode">

``` text
Node Conditional Logic: ${node.tags} contains "database"
ââ Substep: Database maintenance commands
```

</div>

## Building Your Own Conditional Jobs

### Step-by-Step Guide

1.  **Plan Your Conditions**

    - Identify what should trigger different behavior
    - Determine if you need Node or Workflow conditional logic
    - Map out your AND/OR logic requirements

2.  **Create Job Options**

    - Add options for values you'll check in conditions
    - Use enforced values for dropdown choices
    - Make options required if conditions depend on them

3.  **Add Conditional Step**

    - In the Job Editor, click "Add a step"
    - Select Node Conditional Logic or Workflow Conditional Logic
    - Give the step a descriptive name

4.  **Configure Conditions**

    - Add your first condition (Field, Operator, Value)
    - Click "Add" to add more conditions to the same set (AND logic)
    - Click "Add Condition Set" to create alternate conditions (OR logic)

5.  **Add Substeps**

    - Click "+ Add Condition Step"
    - Select and configure steps that run when conditions are met
    - Add multiple substeps as needed

6.  **Test Thoroughly**

    - Run with different option values
    - Enable Debug logging to see condition evaluation
    - Verify substeps execute only when expected

## Tips for Effective Conditionals

### Condition Design

- **Keep it simple**: Prefer multiple simple conditions over complex regex
- **Use descriptive names**: Help others understand what the conditional does
- **Test with debug mode**: Always verify conditions evaluate as expected
- **Document your logic**: Add notes in the job description

### Common Patterns

**Multiple Environments:**

<div class="language-text line-numbers-mode">

``` text
Set 1: ${option.environment} equals "dev"
OR
Set 2: ${option.environment} equals "staging"
```

</div>

**OS + Tag Combination:**

<div class="language-text line-numbers-mode">

``` text
Set 1: ${node.osFamily} equals "unix" AND ${node.tags} contains "web"
OR
Set 2: ${node.osFamily} equals "windows" AND ${node.tags} contains "iis"
```

</div>

**Exclude Specific Cases:**

<div class="language-text line-numbers-mode">

``` text
${option.environment} not equals "production"
```

</div>

### Troubleshooting

**Conditions not evaluating correctly?**

- Enable Debug logging when running the job
- Verify option names match exactly (case-sensitive)
- Ensure Fields use `${}` syntax: `${option.name}` not `option.name`
- Check that node attributes exist on target nodes

**Substeps not appearing?**

- Verify substeps match parent type (Node substeps for Node Conditional, Workflow substeps for Workflow Conditional)
- Check that at least one condition is defined
- Ensure all required fields are filled

**Cannot import job?**

- Conditional Logic requires JSON or YAML format (XML is not supported)
- Verify the feature flag is enabled before importing

## Advanced Scenarios

### Using Data from Previous Steps

Conditional Logic can evaluate data captured from previous steps using log filters:

1.  Add a step with a Log Filter (e.g., Key Value Data) to capture output
2.  In a later conditional step, reference the captured data: `${data.variableName}`

Example:

<div class="language-text line-numbers-mode">

``` text
Step 1: Command with Key Value Data log filter capturing "status"
Step 2: Workflow Conditional Logic: ${data.status} equals "ready"
  ââ Substep: Proceed with deployment
```

</div>

### Multi-Level Conditional Logic

Since nested conditionals are not supported, use Job Reference steps:

1.  Create Job B with its own conditional logic
2.  In Job A, add a conditional step
3.  Add a Job Reference substep pointing to Job B
4.  When Job A's condition is met, it calls Job B, which evaluates its own conditions

This pattern enables sophisticated multi-level conditional workflows.

### Combining with Workflow Strategies

Conditional Logic respects your job's workflow strategy:

- **Sequential Strategy**: Evaluates conditionals for all nodes before moving to the next step
- **Parallel Strategy**: Evaluates conditionals concurrently across nodes

## Related Documentation

- [Conditional Logic Steps Reference](https://docs.rundeck.com/docs/manual/jobs/conditional-logic.html) - Complete feature documentation
- [Job Options](https://docs.rundeck.com/docs/manual/jobs/job-options.html) - Creating and using job options
- [Job Variables](https://docs.rundeck.com/docs/manual/jobs/job-variables.html) - Complete variable reference
- [Workflow Strategies](https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/) - Understanding workflow execution
- [Log Filters](https://docs.rundeck.com/docs/manual/log-filters/) - Capturing data for use in conditions
- [Pass Data Between Steps](https://docs.rundeck.com/docs/learning/howto/passing-variables.html) - Working with variables and log filters

## Next Steps

Now that you understand conditional logic basics:

1.  **Experiment** with the example jobs - modify conditions and observe behavior
2.  **Combine** conditionals with other features like log filters and job references
3.  **Build** your own conditional workflows for your specific use cases
4.  **Share feedback** with Rundeck support - this is an Early Access feature under active development
