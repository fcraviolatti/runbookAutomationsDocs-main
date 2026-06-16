---
title: "Node Execution"
source_url: https://docs.rundeck.com/docs/manual/projects/node-execution/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Node Execution

## Overview

Node Execution (also called Node Executors) defines **how Rundeck connects to and executes commands on your nodes**. Each node executor plugin provides a different method for remote execution, from traditional SSH to cloud-native services like AWS SSM or container orchestration platforms.

When Rundeck needs to execute a command or script on a remote node, it uses the configured node executor to:

1.  Establish a connection to the node
2.  Execute the command or script
3.  Capture and return the output
4.  Report success or failure

## Configuration

Node executors are configured at the **project level** as the default execution method, but can be overridden per-node using node attributes. The default node executor is used when a node doesn't specify its own executor.

**Configure the default in:** Project Settings \> Edit Configuration \> Default Node Executor

## Available Node Executors

Rundeck supports multiple node executor plugins to accommodate different infrastructure and security requirements:

### Traditional Remote Execution

**[SSH (Recommended)](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html)**

- Uses SSH protocol for secure remote command execution
- Supports public/private key and password authentication
- Default for most Rundeck installations
- Includes multiple SSH implementations (SSH-J, OpenSSH, Bastionssh)

**[OpenSSH](https://docs.rundeck.com/docs/manual/projects/node-execution/openssh.html)**

- Uses the native OpenSSH client on the Rundeck server
- Leverages system SSH configuration and known_hosts
- Good for environments with existing SSH infrastructure

**[Bastionssh](https://docs.rundeck.com/docs/manual/projects/node-execution/bastionssh.html)**

- SSH connections through a bastion/jump host
- Enhanced security for nodes in private networks
- Supports chained authentication

### Windows Execution

**[PowerShell](https://docs.rundeck.com/docs/manual/projects/node-execution/powershell.html)**

- Execute commands on Windows nodes using WinRM
- Native PowerShell script execution
- Supports Windows authentication methods

### Cloud Provider Execution

**[AWS SSM](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ssm.html)**

- Execute commands on EC2 instances using AWS Systems Manager
- No SSH key management required
- Leverages AWS IAM for authentication and authorization
- Works with instances in private subnets

**[AWS ECS](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ecs.html)**

- Execute commands in ECS containers
- Direct container execution without SSH
- Supports both EC2 and Fargate launch types

### Container and Script Execution

**[Script](https://docs.rundeck.com/docs/manual/projects/node-execution/script.html)**

- Execute commands using custom scripts
- Wrap existing automation tools
- Flexible integration with any execution method

**[Local (Built-in)](https://docs.rundeck.com/docs/manual/projects/node-execution/builtin.html)**

- Execute commands directly on the Rundeck server
- Used for the local node
- No remote connection required

## Choosing a Node Executor

Consider these factors when selecting a node executor:

**Security Requirements:**

- SSH with keys - Most secure for Linux/Unix
- AWS SSM - Eliminates key management, uses IAM
- Bastionssh - Additional security layer via jump host

**Infrastructure Type:**

- **Traditional VMs** - SSH (Linux/Unix) or PowerShell (Windows)
- **AWS EC2** - SSH or AWS SSM
- **Containers (ECS)** - AWS ECS executor
- **Private Networks** - Bastionssh through bastion host
- **Rundeck Server** - Local/Built-in

**Operational Preferences:**

- **Standardized** - SSH (works everywhere)
- **Cloud-native** - AWS SSM, AWS ECS
- **No key management** - AWS SSM, PowerShell with AD
- **Existing automation** - Script executor wrapper

## Related Configuration

Node executors work together with other node-related features:

- **[Node Sources](https://docs.rundeck.com/manual/projects/resource-model-sources/)** - Where nodes come from (discovery)
- **[File Copiers](https://docs.rundeck.com/docs/manual/projects/node-execution/builtin.html#file-copiers)** - How files are transferred to nodes
- **[Node Enhancers](https://docs.rundeck.com/docs/manual/node-enhancers.html)** - Enhance node data with additional attributes
- **[Node Filters](https://docs.rundeck.com/docs/manual/11-node-filters.html)** - Select which nodes to execute on

## How Node Execution Works

When you execute a job or command in Rundeck:

1.  **Node Selection** - Rundeck identifies target nodes based on filters
2.  **Executor Selection** - Determines which node executor to use (per-node or default)
3.  **Connection** - Node executor establishes connection to the node
4.  **Execution** - Command or script is executed on the node
5.  **Output Capture** - Results are captured and streamed to Rundeck
6.  **Reporting** - Success/failure status is reported

For script steps, an additional **File Copier** step occurs before execution to transfer the script file to the target node.

## Troubleshooting

Common node execution issues:

**Connection Failures:**

- Verify network connectivity to nodes
- Check firewall rules (SSH: port 22, WinRM: ports 5985/5986)
- Confirm authentication credentials (keys, passwords)
- Review node attributes (hostname, username)

**Permission Errors:**

- Verify user has execute permissions on target nodes
- Check sudo/privilege escalation configuration
- Confirm AWS IAM roles (for AWS SSM/ECS)

**Performance Issues:**

- Increase timeout values in executor configuration
- Check network latency to nodes
- Review concurrent execution limits

For detailed troubleshooting, see the individual executor documentation pages.

## Advanced Configuration

### Per-Node Executor Override

Set node-specific executors using node attributes:

<div class="language-yaml line-numbers-mode">

``` yaml
nodename: mynode
hostname: 192.168.1.100
username: rundeckuser
node-executor: aws-ssm  # Override default executor
```

</div>

### Custom Node Executors

You can develop custom node executor plugins to integrate with proprietary systems or specialized infrastructure. See [Node Executor Plugin Development](https://docs.rundeck.com/docs/developer/node-executor-plugins.html) for details.

## Related Documentation

- [SSH Node Execution](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html) - Detailed SSH configuration
- [Node Sources](https://docs.rundeck.com/manual/projects/resource-model-sources/) - Node discovery and inventory
- [Commands](https://docs.rundeck.com/docs/manual/06-commands.html) - Executing ad-hoc commands
- [Jobs](https://docs.rundeck.com/manual/jobs/) - Creating automated workflows
- [Node Executor Plugins (Development)](https://docs.rundeck.com/docs/developer/node-executor-plugins.html) - Creating custom executors
