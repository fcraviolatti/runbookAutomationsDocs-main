---
title: "Runner"
source_url: https://docs.rundeck.com/docs/administration/runner/pre-4-11-runners.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Runner

> **Available in PagerDuty Runbook Automation Commercial products.**

The Runner, available for both Runbook Automation securely opens up network/communication between data centers and the Automation Cluster. The Runner is a Remote Execution hub for Node Steps to run on specified endpoints, rather than from the Automation server itself.

## Architecture

The Runner is a Java based program which uses a polling model to pick up work from the Automation Server. During each polling cycle (every 5 seconds) the Runner checks for executions that it is responsible for. Communication from the Runner to the Automation Server happens over https and is initiated from the Runner. This allows for enhanced firewall security as ports no longer need to be open for the Automation Server to talk to nodes over more sensitive ports. *(e.g. SSH/22)*

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/runner-arch-diagram.png" alt="Runner Architecture" />
<figcaption aria-hidden="true">Runner Architecture</figcaption>
</figure>

## Installation

Follow these steps to install a Runner:

Creating and configuring a Runner

Installing a Runner

Creating and configuring a Runner

1.  Under the *System Menu* (gear icon upper-right) choose **Runner Management**
2.  Choose **Create Runner**.
3.  Type in a unique *Name* and relevant *Description* for this Runner and Click **Add Runner**.
4.  Click **Next** to go to *Project Assignment*
5.  \[This step is optional\] On this page choose which project(s) the Runner is active for. The Assigned toggle will enable the Runner for *All Nodes* (`.*`) in that project. After the Runner is created you can edit the Runner assignment and adjust the node filter to target a subset of nodes. Click **Next**.
6.  On the **Confirmation** step, click on **Download** and save the Runner JAR binary file. Note that the JAR file must be used only for the environment that it is configured for. Click **Finish**.

Installing a Runner

Pre-Requisites:

- Same [OS requirements as Rundeck](https://docs.rundeck.com/docs/administration/install/system-requirements.html)
- Java 11 is required to run the Runner JAR file.

1.  Copy the Runner JAR file that was saved when the Runner was created to the server and directory where it will run.
2.  Execute `java -jar runner_filename.jar` to start the service.

Connection can be confirmed on the Runner Management page on the *Last Checkin* line. If there are errors in the output resolve those using troubleshooting steps below.

> **Tips**
>
> To enable the Runner features you have to add the following property in `rundeck-config.properties` file and restart the Runbook Automation cluster or instance. This feature has been enabled on Docker installations since v4.5.0 and is also enabled by default for Runbook Automation.
>
> <div class="language-text line-numbers-mode">
>
> ``` text
> rundeck.feature.runner.enabled=true
> ```
>
> </div>

## Runner Management

### Assigning Projects/Nodes to a Runner

Runners will execute Node Steps on Nodes within a project based on a Node Filter assigned to the Runner. To assign Projects and specific nodes to a Runner follow these steps:

1.  In the Runner Management screen click on the name of the Runner instance to be edited.
2.  If the project is not listed already choose **Add Projects**
3.  Toggle the Projects that should be added.
4.  The Node Filter section is used to identify Nodes that this runner is responsible for. By default `.*` will apply it to all nodes in the project.
5.  Click **Add** and the projects are now listed under the Runner configuration.

It is possible to edit each project Node Filter individually if needed. Use the *Actions* menu to *Edit* the project entry's Node Filter.

### Troubleshooting

Runner Logs are located in the `./runner/logs` folder under the folder where the jar was executed from. The `runner.log` file contains operational and important messages about the runner. `operations.log` tracks an operation starts and if it succeeds or fails. [Read more about logging and setting up custom logging](https://docs.rundeck.com/docs/administration/runner/runner-management/runner-logging.html).

### Proxying Runner connections

Runners can be configured to connect through a HTTP/HTTPS proxy. Proxies are commonly used to centralize and secure outbound traffic from the datacenter to internet services. The proxy configuration is optional and is added as java command line arguments when the runner process is started.

#### Proxy configuration without proxy authentication

The following example will allow the runner to connect through the secure company proxy with address wp.acme.corp.

<div class="language-text line-numbers-mode">

``` text
java -Dmicronaut.http.client.proxy-type=http -Dmicronaut.http.client.proxy-address=wp.acme.corp:443 -jar pdrunner.jar
```

</div>

1.  `-Dmicronaut.http.client.proxy-type` is set to `http`
2.  `-Dmicronaut.http.client.proxy-address` is set to the secure proxy company address.

#### Proxy configuration with proxy authentication

The following example adds basic auth proxy configuration to the runner. The proxy-type and proxy-address settings are the same as the unauthenticated access example.

<div class="language-text line-numbers-mode">

``` text
java -Dmicronaut.http.client.proxy-type=http -Dmicronaut.http.client.proxy-address=wp.acme.corp:443 -Dmicronaut.http.client.proxy-username=proxyUsernameString -Dmicronaut.http.client.proxy-password=proxyPassString -jar pdrunner.jar
```

</div>

1.  `-Dmicronaut.http.client.proxy-username` is set to the user that is allowed to connect through the secure proxy.
2.  `-Dmicronaut.http.client.proxy-password` is set to the secure proxy user password.

### Runner on Windows OS

The â€œRunner Managementâ€? menu will appear on under the â€œSystemâ€? settings:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/runner-management.png" alt="Runner Architecture" />
<figcaption aria-hidden="true">Runner Architecture</figcaption>
</figure>

If you are installing a Runner on a Windows OS as localhost node, you have to specify the â€œOS Familyâ€? setting as â€œwindowsâ€?.

- Choose related to the project.
- Go to the left side bar menu and choose "EDIT NODES".
- Click on "Resources" tab.
- Click on "Edit" on the local node.
- On the field "OS Family" set "windows".

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/runner-edit-nodes.png" alt="Runner Architecture" />
<figcaption aria-hidden="true">Runner Architecture</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/runner-resource-tab.png" alt="Runner Architecture" />
<figcaption aria-hidden="true">Runner Architecture</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/runner-edit-local.png" alt="Runner Architecture" />
<figcaption aria-hidden="true">Runner Architecture</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/runner-os-family.png" alt="Runner Architecture" />
<figcaption aria-hidden="true">Runner Architecture</figcaption>
</figure>

Powershell script steps are fully supported on the Runner. Commands that run through the cmd.exe shell are not supported at the moment.

## FAQ

**Does this replace Clustering?**

This feature is intended to be used in situations where execution of Node Steps is needed in a network segment or security zone that is different from the Cluster feature(s). An Automation Server Cluster still provides high-availability and fault tolerance for the User Interface, Job Management/Execution and system management tasks.

**Does this work for all communication into the remote data center?**

At this time, the Runner will execute Node Executor and File Copier steps. This includes node steps such as Remote Command, Inline Script, Script File, and Copy File, as well as commands executed from the Commands tab. Node Sources, Health Checks, and other communication are not included in this version of the Runner.

**Do Runners participate in node discovery?**

Not at this time. To dynamically update nodes use custom scripting and the [APIs](https://docs.rundeck.com/docs/api/#updating-and-listing-resources-for-a-project) to update the node lists remotely.

**Can multiple Runners run in parallel?**

Yes, multiple runners can be configured for the same project. If multiple runners have the same node scope, they race to retrieve the relevant task list. Multiple runners can be used to increase scale or add more redundancy in the automation architecture.
