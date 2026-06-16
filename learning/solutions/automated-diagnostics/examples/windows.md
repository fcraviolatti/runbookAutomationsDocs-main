---
title: "Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/windows.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

## Windows OS & Applications

When responding to incidents related to Windows servers, there are many sorts of diagnostics that can be run. Unlike some cloud diagnostics, connecting to servers will involve using [node executors](https://docs.rundeck.com/docs/manual/projects/node-execution/builtin.html) to connect. Node executors will be utilized by [Runners](https://docs.rundeck.com/administration/runner/#runner-on-windows-os) with Runbook Automation or directly by servers with Runbook Automation Self-Hosted. Node executors are configured as part of node definitions at the project level or per-node and then used as needed at job run-time by the Runner or server.

Often, Windows diagnostics are jobs composed of one or more [command](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#command-step) or [script](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#script-step) steps that gather data from the node about resources or services on that node.

### Examples:

- Check the health of a Windows service such as a web server or database using PowerShell
- Parse server logs for common error messages
- Check health of components of a custom application across one or more servers
- Collect resource diagnostics from the server, such as memory utilization, cpu resources or available disk space

### Node executors commonly used in connecting with Windows nodes:

- [PowerShell](https://docs.rundeck.com/docs/manual/projects/node-execution/powershell.html)
- [WinRM](https://docs.rundeck.com/docs/learning/howto/configuring-windows-nodes.html#running-jobs-on-windows-nodes)
- [SSH](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html)
- [OpenSSH](https://docs.rundeck.com/docs/manual/projects/node-execution/openssh.html)
- [SSM on AWS](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ssm.html)
- [ECS container nodes](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ecs.html)
- [OpenSSH using Bastion Hosts](https://docs.rundeck.com/docs/manual/projects/node-execution/bastionssh.html)
