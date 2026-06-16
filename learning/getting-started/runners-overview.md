---
title: "Configuring Enterprise Runners to access remote Nodes"
source_url: https://docs.rundeck.com/docs/learning/getting-started/runners-overview.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Configuring Enterprise Runners to access remote Nodes

> **Available in PagerDuty Runbook Automation Commercial products.**

[Enterprise Runners](https://docs.rundeck.com/docs/administration/runner/pre-4-11-runners.html#runner) are a recent addition to the PagerDuty Runbook Automation architecture. They are primarily used as a method for orchestrating automation in secure, remote environments where direct access to infrastructure and services is restricted. This is accomplished by using a "reverse proxy" architecture: Runners regularly query (outbound only) the Runbook Automation Cluster (or Runbook Automation instance) for tasks. Runners are assigned to one or more Projects, and then [Jobs](https://docs.rundeck.com/docs/learning/getting-started/jobs/what-is-a-job.html) within those Projects can use the Runner to dispatch the Job steps to be executed through the Runner in the remote environment.  
![](https://docs.rundeck.com/docs/assets/img/runnerarch1.png)  
*Example showing Runner architecture (Each remote Runner could be a Runner set)*  
When Runners are enabled for a job, the execution of Job steps will be delegated to a specific Runner for management. This model offers resiliency as multiple Runners could be enabled for a particular Project so that each Job can be assigned to a specific Runner during high usage windows.  
To utilize Runners, there are a few steps to carry out:  

## System Configuration

1.  [Enable Runners at the system level](https://docs.rundeck.com/docs/administration/runner/runner-setup.html)  
    Though Runners will primarily be used and managed in the context of projects, a system admin does need to enable them initially.  
2.  [Create new Runners at the system level](https://docs.rundeck.com/docs/administration/runner/runner-config.html)  
    For each Runner, you will be prompted for three things:  
    \* A name  
    Using clear naming can help with Runner management as the number of Runners increases.  
    \* Define one or more tags  
    Tags determine which Runner set will execute which Jobs.  
    \* Associate Runners with Projects  
    Each Runner must be associated with at least one Project in order to be used.  

## Runner Installation

1.  [Install Runner software in remote networks for each Runner that has been created](https://docs.rundeck.com/docs/administration/runner/runner-installation/runner-install.html).  
    Though Runners have been defined by this point, it is still necessary to install software in each of the remote locations.  

## Configure Jobs for Runners

1.  [Add Runner tags to Jobs](https://docs.rundeck.com/docs/administration/runner/)  
    New jobs will prompt authors to choose tags which represent Runners or Runner sets by tags. It is important to review existing Jobs to ensure that they have appropriate tags selected as well. ![](https://docs.rundeck.com/docs/assets/img/runnerarch2.png)  
    *Jobs are assigned to remote Runners based on tags. Jobs on nodes in the clusterâ€™s local network can be handled through the Local Runner.*  

# Resources

[Advanced Runner Setup Options](https://docs.rundeck.com/administration/runner/)  
[Runner Custom Logging](https://docs.rundeck.com/docs/administration/runner/runner-management/runner-logging.html)
