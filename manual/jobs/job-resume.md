---
title: "Job Resume Plugin (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-resume.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Job Resume Plugin (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

This plugin allows resuming a job if one or more steps fail.

When you enable this plugin for a Job, the plugin will record the internal *Workflow State* as the Execution progresses. When one or more steps fail, the Workflow State prior to executing the failed step(s) is recorded and stored.

You can then choose to "Resume" the execution, which will load the stored state and start a new execution, proceeding to execute the previously failed step(s) with the same inputs.

## Requirements

> **Warning**
>
> This plugin does not work for "Node First" Workflow Strategy.

> **BETA FEATURE**
>
> This plugin now works with "Parallel" and "Ruleset" Strategies.

1.  The Job cannot use the "Node FIrst" Workflow Strategy.
2.  The Job's workflow sequence should not be modified before resuming the execution. The plugin will store a "snapshot" of the workflow sequence within the resume state, allowing it to compare that to the workflow sequence used to resume it. If the Job workflow sequence has been modified, the plugin will fail to start. This means that you should not reorder, add/remove, or replace steps in the Workflow before resuming the execution. However, modifying existing steps should be possible.

## Caveats - Workflow Strategies

Does not work with "Node First" workflow strategy.

Only works with these workflow strategies:

- Sequential
- Parallel (**BETA** feature)
- Ruleset (**BETA** feature)

## Caveats - Secure Options

The runtime values for "Secure" or "Secure Remote Authentication" options **will not** be persisted with the Resumable workflow state.

This means that Secure Option values will only be available when Resuming a job in these cases:

- If a secure option defines a Storage Path, the Key Storage value will be loaded when the execution is Resumed.
- If "Other \> Retry" is configured for the Job, and "Resume On Retry" is checked, secure option values will be available when the execution is automatically retried.

In other words, manually-entered Secure Option values will not be available when a manual "Resume" action is performed.

## Usage

To use this plugin, edit or create a Job, and under the "Execution Plugins" tab, enable the checkbox next to the "Resumable" plugin.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/figure-job-resume-edit-job-execution-plugins.png" alt="Execution Plugins" />
<figcaption aria-hidden="true">Execution Plugins</figcaption>
</figure>

When an execution fails at some step, a new menu option is available under the "Run Againâ€¦" drop down.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/figure-job-resume-resume-execution-menuitem.png" alt="Resume Execution Menu Item" />
<figcaption aria-hidden="true">Resume Execution Menu Item</figcaption>
</figure>

You will see a confirmation page to begin the resumed execution.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/figure-job-resume-confirm-resume.png" alt="Confirm Resume Execution" />
<figcaption aria-hidden="true">Confirm Resume Execution</figcaption>
</figure>

After confirming, the new execution will begin at the step(s) that previously failed.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/figure-job-resume-resumed-execution.png" alt="Resumed Execution" />
<figcaption aria-hidden="true">Resumed Execution</figcaption>
</figure>

## Resume On Retry

When a Job uses the "Retry" feature, it normally will automatically start a fresh Execution when it fails, after an optional delay.

The Job Resume plugin can be configured to automatically use the Resume state when the execution is retried.

## Configuration

The configuration of this plugin is simple. Once added to a Job definition, it is enabled by default.

<div class="language-xml line-numbers-mode">

``` xml
<joblist>
  <job>
    <!-- ... -->
    <plugins>
      <ExecutionLifecycle type='resume'/>
    </plugins>
   </job>
</joblist>
```

</div>

If you also want to enable it for automatic Retries, set `onRetry` to `true`.

<div class="language-xml line-numbers-mode">

``` xml
<joblist>
  <job>
    <!-- ... -->
    <plugins>
      <ExecutionLifecycle type='resume'>
        <configuration data='true'>
          <map>
        <string key='onRetry'>true</string>
          </map>
        </configuration>
      </ExecutionLifecycle>
    </plugins>
   </job>
</joblist>
```

</div>

## Clustering

This plugin works with Clustering in Runbook Automation Self-Hosted. The serialized "Resume state" is stored alongside the execution log and execution state file in your configured [Log Storage](https://docs.rundeck.com/docs/administration/cluster/logstore/) system, with a file extension of `.resume.json`.

You can initiate the **Resume Execution** from any Cluster member if the Resume state file has been copied to the Log Storage system. Before the execution starts, the file will be loaded from the Log Storage system.

## Limitations

- Currently only the top level workflow steps will be tracked for resume. Referenced jobs will not resume at their internally failed step.
- If the Rundeck server is interrupted, such as an application or server crash, before the workflow state is serialized and stored the execution will not be able to resume from the failed step.
- Currently, if you kill manually a job during its execution, this job cannot be resumed. The plugin does not allow this action. Only a job can be resumed when this fails by itself.
