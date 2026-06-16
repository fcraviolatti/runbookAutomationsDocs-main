---
title: "Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/linux.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

## Linux OS & Applications

When responding to incidents related to Linux servers, there are many sorts of diagnostics that can be run. Unlike some cloud diagnostics, connecting to Linux servers will involve using [node executors](https://docs.rundeck.com/docs/manual/projects/node-execution/builtin.html) to connect. Node executors will be utilized by [Runners](https://docs.rundeck.com/administration/runner/#installation) with Runbook Automation or directly by servers with Runbook Automation Self-Hosted.  
Node executors are configured as part of node definitions at the project level or per-node and then used as needed at job run-time by the Runner or server.

Often, Linux diagnostics are jobs composed of one or more [command](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#command-step) or [script](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#script-step) steps that gather data from the node about resources or services on that node.

### Examples:

The following examples are included in our **Automated Diagnostics Project**, which can be downloaded [**here**](https://github.com/rundeckpro/automated-diagnostics-project/releases/latest/download/automated-diagnostics.jar).

#### Check the health of a Linux service such as a web server or database

![](https://docs.rundeck.com/docs/assets/img/linux1.png)  

#### Parse server logs for common error messages

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/linux2.png" alt="Syslog Queries For Common Errors" />
<figcaption aria-hidden="true">Syslog Queries For Common Errors</figcaption>
</figure>

#### Collecting resource diagnostics from the server

![](https://docs.rundeck.com/docs/assets/img/linux3.png)  

## Node Executors for Linux:

**Runbook Automation** offer multiple methods of communicating with Linux servers through the multiple **Node Executors**, such as these:

- [SSH](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html)
- [OpenSSH](https://docs.rundeck.com/docs/manual/projects/node-execution/openssh.html)
- [Ansible inventory](https://docs.rundeck.com/docs/learning/howto/using-ansible.html#how-to-integrate-ansible-with-rundeck)
- [SSM on AWS](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ssm.html)
- [ECS container nodes](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ecs.html)
- [OpenSSH using Bastion Hosts](https://docs.rundeck.com/docs/manual/projects/node-execution/bastionssh.html)
