---
title: "Node Dispatch"
source_url: https://docs.rundeck.com/docs/administration/runner/runner-management/node-dispatch.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Node Dispatch

> **System Configuration Required**
>
> To use this feature, **`rundeck.feature.distributedAutomation.enabled`** must be set to **`true`** in **System Configuration**.

The Node Dispatch settings of a Runner defines which nodes are assigned to a Runner for the dispatch of automation tasks.

**Note:** *Node Dispatch* settings for Runners is only available for projects that use **Automatic** for ***Runner Selection for Job Execution***. This can be toggled through the [Project Dispatch Configuration](https://docs.rundeck.com/docs/administration/runner/runner-management/project-dispatch-configuration.html) and is the default for all new projects.

## Runner as a Node

Enabling the ***Runner as a Node*** adds the Runner as a node to the node inventory. When this node is targeted with a node-step within a Job or with a command from the Commands page, the Runner will execute the step locally. This is useful for running automation tasks that require the Runner to execute a command or script on the local host.

> **Runners with Multiple Replicas**
>
> When a Runner has multiple Replicas, only a single node is created for the Runner in the node inventory. This is because any Replica can pick up the tasks assigned to a Runner, including local-execution tasks. Therefore, when a command or a script is dispatched to the Runner node, any Replica of the Runner can pick up the task and execute it locally.

> **Runner Version Requirement**
>
> To use the Runner as a Node feature and target the Runner's host with command and script steps, the Runner must be at version 5.5.0 or later.

Nodes that represent Runners are designated with a Runner icon in the node inventory and do not require configuring a node source for the Runner's to be added to the inventory.

![Runner as a Node](https://docs.rundeck.com/docs/assets/img/runners-as-nodes-inventory.png)  

When a Runner is created, it is automatically added as a node to the node inventory. This can be disabled by unchecking the ***Enable Runner as a Node*** setting:

1.  Navigate to the **Runner Management** page within the Project.
2.  Select the Runner by clicking on the Runner's name.
3.  Click on the **Node Dispatch** tab.
4.  Uncheck the ***Enable Runner as a Node*** setting: ![Enable Runner as a Node](https://docs.rundeck.com/docs/assets/img/enable-runner-as-node.png)  
      

> **Local Node Source Requirement**
>
> Nodes that represent Runners are dependent on the **Local** Node Source to be configured. Removing the Local Node Source will result in the removal of the Runner nodes from the inventory.
>
> ![Local node source](https://docs.rundeck.com/docs/assets/img/local-node-source.png)  
>
> To still use the Local Node Source, but prevent the execution of commands and scripts on the Runbook Automation cluster members, set the JVM system property **`rundeck.localExecutor.disabled=true`** or **`DISABLED_LOCAL_EXECUTOR=true`** for Docker installations.

## Remote Node Dispatch

Enabling the ***Remote Node Dispatch*** setting allows the Runner to dispatch commands, scripts and API calls to *remote* nodes using protocols such as SSH, WinRM and HTTP/S. This is necessary for securely dispatching to nodes from Runbook Automation Cloud or to nodes that are not directly accessible from the self-hosted cluster.

The mapping of which nodes a given Runner is responsible for is defined using a [**Node Filter**](https://docs.rundeck.com/docs/manual/11-node-filters.html). When the Node Filter is defined for a Runner, then Job steps that target the nodes that match the filter will be dispatched *through* the Runner for execution.

To define the Node Filter for a Runner:

1.  Navigate to the **Runner Management** page within the Project.
2.  Select the Runner by clicking on the Runner's name.
3.  Click on the **Node Dispatch** tab.
4.  Enable the ***Remote Node Dispatch*** setting. ![](https://docs.rundeck.com/docs/assets/img/runner-node-dispatch.png)
5.  Define the Node Filter using the **Node Filter** field.
6.  Click **Save Configuration**.

![Remote Node Dispatch](https://docs.rundeck.com/docs/assets/img/runner-node-filter.png)*Runners are dynamically chosen for Job execution based on the Runner's Node Filter*

> **Nodes Without a Runner Association**
>
> Nodes that do not match the Node Filter of any Runner will be dispatched to using the Runbook Automation cluster (self-hosted). When using Runbook Automation Cloud, commands and scripts can be dispatched to these nodes using the [AWS Systems Manager](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ssm.html) Node Executor. Node Step plugins that target public endpoints - such as AWS or Datadog node step plugins - can also be used through Runbook Automation Cloud when no Runner is assigned to those nodes.
>
> This ensures that all nodes are dispatched for execution, even if they do not match the Node Filter of a Runner.

> **Example**
>
> ## Remote Dispatch Node Filter Example
>
> A common use-case for defining a Node Filter for a Runner is to declare a given region or data-center that a Runner is responsible for.
>
> For example, a Runner that is responsible for nodes in the **`us-west-1`** region could have a Node Filter defined as:  
> `region: "us-west-1"`
>
> ![Remote Node Dispatch](https://docs.rundeck.com/docs/assets/img/remote-node-dispatch-example.png)  
>
> Taking this a step further, a Runner could be responsible for only ***Windows*** nodes in `us-west-1`, in which case the Node Filter would be:  
> `region: "us-west-1" osFamily: "windows"`
>
> ![Remote node dispatch windows example](https://docs.rundeck.com/docs/assets/img/remote-node-dispatch-windows-example.png)  
>
> For more information on defining Node Filters, see the [Node Filters](https://docs.rundeck.com/docs/manual/11-node-filters.html) documentation.

## Overlapping Node Filters

When defining Node Filters for Runners, it is possible to have filters on multiple Runners that overlap their assignments of the node inventory. In other words, a given node may be mapped to more than one Runner.

For example, one Runner may have the node filter `region: "us-west-1"` and another Runner may have the node filter `region: "us-west-1" osFamily: "windows"`. In this case, Jobs steps that target *Windows* nodes in the *US-WEST-1* region could be dispatched through ***either*** Runner.

It is recommended to **avoid overlapping Node Filters for Runners**, as this can lead to confusion and unexpected behavior. Instead, it is recommended to use Replicas to scale the Runner's capacity and provide redundancy.
