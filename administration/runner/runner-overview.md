---
title: "Enterprise Runner"
source_url: https://docs.rundeck.com/docs/administration/runner/runner-overview.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Enterprise Runner

Building and orchestrating automation in complex multi-cloud and remote environments presents several challenges. The first challenge is that DevOps and Operations engineers need an alternative to run automation in secure application environments that mandate a zero trust architecture where accessing private networks through SSH is deprecated. Next, significant engineering effort is required to deploy and manage automation that performs well across many remote environments and geographical regions. Lastly, creating resilient automation runbooks is time consuming and prone to error when coordinating a variety of complex environments.

We are introducing a next generation architecture to address these challenges. With the new Runbook Automation architecture, DevOps and Operations engineers can easily manage automation in a central UI while delegating job execution within different private networks or multi-cloud environments without needing to open SSH ports for accessing those networks. The new architecture separates workflow orchestration from task execution. It offers next generation remote Runners that include common integration plugins like Ansible and Kubernetes that execute locally to the application environment.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/architecture-nextgen.png" alt="Next generation automation" />
<figcaption aria-hidden="true">Next generation automation</figcaption>
</figure>

The Runner, available for both Runbook Automation, securely opens up network/communication between data centers and the Automation Cluster. The Runner is a Remote Execution hub for Node Steps to run on specified endpoints, rather than from the Automation server itself.

## System Architecture

The Runner is a Java based program which uses a polling model to pick up work from the Automation Server. During each polling cycle (every 5 seconds) the Runner checks for executions that it is responsible for. Communication from the Runner to the Automation Server happens over https and is initiated from the Runner. This allows for enhanced firewall security as ports no longer need to be open for the Automation Server to talk to nodes over more sensitive ports. *(e.g. SSH/22)*![Runner Architecture](https://docs.rundeck.com/docs/assets/img/runner-arch-diagram.png)

## Example scenario using the runner architecture

With the next generation architecture, automation authors can select which Runners will carry out the tasks for a given job using Runner tags. Authors can also choose if tasks will execute on a Runner or if tasks will be dispatched to nodes through the selected Runner set. There are two types of Runners: Local and Remote. The Local Runner tasks execute from the Rundeck instance. The Remote Runner tasks execute from the Runners installed in the environment.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/runner-scenario.png" alt="Private networks scenario" />
<figcaption aria-hidden="true">Private networks scenario</figcaption>
</figure>

In the example below, we have a job that will span three different environments.

1.  The 1st step (Check Cloud Services Status) is a reference job that is configured with a Remote Runner which will execute a Kubernetes plugin as a workflow step.
2.  Steps 2, 3, and 4 are configured to run on the Local Runner.
3.  Step 5 (Check System Resources) is also a reference job similar to step 1, but executes an Ansible playbook through the Ansible plugin and targets nodes in the second environment through a separate Remote Runner.
4.  Step 7 (Run DB Lock Check) is also a reference job similar to step 1 and 5, but executes a Powershell command through the WinRM plugin and targets nodes in the third environment through a separate Remote Runner.

## Prerequisites

The new architecture is available with v4.11+ of Runook Automation. The new architecture is off by default and can be turned on with a system setting. The Runner authentication and communication architecture is the same between the two generations of Runners. The new Runners use new APIs, management UI, and have a new and more extensive set of plugins available.

## Setup steps

If the enterprise Runners are enabled you can skip setting the runner.enabled setting. If you have not enabled the Runner feature please do so by doing the following: Add the following property in rundeck-config.properties file and restart the Runbook Automation. This feature has been enabled on Docker installations since v4.5.0 and is also enabled by default for Runbook Automation:

`rundeck.feature.runner.enabled=true`

To enable the new architecture, a new configuration feature flag was added to enable/disable the new UI components for managing and running jobs with Runners. The feature flag will turn on all the new UI and APIs. The flag can be added through â€œAdd configâ€? n the System Configuration UI. Applying this setting does not require a restart of Runbook Automation.

`rundeck.feature.distributedAutomation.enabled = true`

## Upgrade Notes for customers previously using Runners before Runbook Automation version 4.11

This section applies only for installations that have deployed the previous generation architecture of Runbook Automation Runners (this does not apply to Automation Action Runners). You can disable the new architecture by changing the setting to false which will revert to the previous behaviors and UIs of the Runners. Toggling the feature on and off does NOT change Job or Runner data, but it does change how jobs use Runners and the Runbook Automation UI.

If you are using the previous generation of Runners before v4.11, and want to enable the latest Runner features:

1.  Set **`rundeck.feature.distributedAutomation.enabled`** = **`true`** as described previously.
2.  Upgrade the Runners to the latest version.
