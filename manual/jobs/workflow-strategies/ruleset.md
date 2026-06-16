---
title: "Ruleset Workflow Strategy Plugin"
source_url: https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/ruleset.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Ruleset Workflow Strategy Plugin

> **Available in PagerDuty Runbook Automation Commercial products.**

The Ruleset Workflow Strategy allows Enterprise users to provide more complex logic around job step execution. To use the Ruleset Strategy choose *Ruleset* on the Workflow tab when editing a Job.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/relnotes-344-rulesetdesigner.gif" alt="Ruleset Strategy" />
<figcaption aria-hidden="true">Ruleset Strategy</figcaption>
</figure>

> **Warning**
>
> When the Workflow graph contains a large number of jobs, the job edit page may experience performance issues. Use the following setting to disable the graph renderization: `rundeck.gui.workflowGraph` set to `false`. This can be configured without restarting the system, via [Configuration Manager](https://docs.rundeck.com/docs/manual/configuration-mgmt/configmgmt.html).
>
> Read more about [the setting](https://docs.rundeck.com/docs/administration/configuration/gui-customization.html)

## Writing Rules

### Syntax

Rules define how each step should run. You can add one rule per-line. Rules are additive, and you can define multiple rules for each step. Rules are in the form:

<div class="language-text line-numbers-mode">

``` text
STEP [directive] [conditions...]
```

</div>

This indicates which step or steps the rule applies to, and any directives or conditions for the step. The rule must have a directive or condition, or both.

### Step

Specifies the step, or steps that the rule applies to. You must include the \[ and \] characters:

- `[X]`: Applies to a single step, the named or numbered step X. You can use the step number, e.g. `[1]` or the label, e.g. `[Deploy QA]` (case sensitive).
- `[X,Y,Z...]`: Applies to multiple steps. Separate multiple steps with a comma, e.g. `[1,2,3]`
- `[1-3]`: Applies to steps 1 through 3
- `[1-3,5-7]`: Applies to steps 1 through 3 and 5 through 7
- `[*]`: Applies to all steps

### Directive

Directives optionally define when a step should start. You can define a directive rule for all steps `[*]` using run-at-start or run-in-sequence.

- `run-at-start`: Run at workflow start time. The indicated steps will start immediately when the workflow starts.
- `run-in-sequence`: Run after the previous step in sequence is run or is skipped.
- `run-after:X[,Y[,Z..]]`: Run after one or more steps run or are skipped.

> **Warning**
>
> Step Numbers and Names can be used on run-after:\[\], but in the case that the Step Name includes spaces, this condition must be encapsulated in double quotes, e.g. `[Step Two] "run-after:Step One"`

### Conditions

Conditions can define additional checks that must pass before a step can run, or determine when a step can be skipped. For example:

- `if:expression`
- `unless:expression`

`expression` defines a comparison or match that will be checked. Valid expressions are:

- `key.name==string`: a context variable such as option.myoption has a certain value
- `key.name!=string`: not-equal check
- `key.name=~pattern`: regular expression match
- `key.name!~pattern`: negative regular expression match
- `!key.name` context: variable is unset
- `key.name>=number`: greater than or equal to check
- `key.name<=number`: less than or equal to check
- `key.name>number`: greater than check
- `key.name<number`: less than check

> Note: Curly braces are not needed to reference context variable key names. Option, Global, and Workflow Step variables are accessible by the Ruleset Strategy. *Node Context* variables are not available to Ruleset Conditions.

### How to achieve an OR condition

To achieve an OR condition you can evaluate two times the options than should be satisfied to allow the steps to be executed, as shown on the following example code this double evaluation must be done in two separate lines.

<div class="language-text line-numbers-mode">

``` text
[1] run-at-start
[2] run-after:1
[3,4,5] if:option.1>0
[3,4,5] if:option.2==true
```

</div>

In this case steps 3,4,5 will be executed if one or both conditions are satisfied.

### How to achieve an AND condition

To achieve an AND condition you can apply two or more evaluations on the same line, if all conditions are satisfied the steps will be executed.

<div class="language-text line-numbers-mode">

``` text
[1] run-at-start
[2] run-after:1
[3,4,5] if:option.1>0 if:option.1<100 if:option.2==true
```

</div>

In this case steps 3,4,5 will be executed if all the three conditions are satisfied.

## Examples

Run steps 2 and 5 only after step 1 is done:

<div class="language-text line-numbers-mode">

``` text
[2,5] run-after:1
```

</div>

Choose between 5 and 6 based on an option value:

<div class="language-text line-numbers-mode">

``` text
[*] run-in-sequence
[5] if:option.env==QA
[6] unless:option.env==PRODUCTION
```

</div>

Run step 1, then steps 2 and 3 in parallel, then step 4:

<div class="language-text line-numbers-mode">

``` text
[2] run-after:1
[3] run-after:1
[4] run-after:2,3
```

</div>

Run steps only if two different conditions are met:

<div class="language-text line-numbers-mode">

``` text
[1] run-in-sequence
[2] if:option.1==yes if:option.2==yes
[3] if:option.1==yes if:option.2==no
[4] if:option.1==no if:option.2==yes
[5] if:option.1==no if:option.2==no
```

</div>

Based on the ruleset defined above, if option 1 is "yes" and option 2 is "no" then job step 3 would run after 1. If option 1 is "no" and option 2 is "yes" then job step 4 would run after 1.
