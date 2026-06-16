---
title: "AWS Elastic Container Service (ECS) Workflow Steps"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-ecs-fargate.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS Elastic Container Service (ECS) Workflow Steps

> **Available in PagerDuty Runbook Automation Commercial products.**

Amazon ECS is a fully managed container orchestration service that makes it easy for you to deploy, manage, and scale containerized applications.

The following plugins are available for PagerDuty Runbook Automation:

- [AWS Elastic Container Service (ECS) Workflow Steps](#aws-elastic-container-service-ecs-workflow-steps)
  - [Authentication](#authentication)
  - [Send Commands to ECS Containers](#send-commands-to-ecs-containers)
    - [Prerequisites](#prerequisites)
    - [Configuration](#configuration)
    - [Executing Job Step](#executing-job-step)
  - [Stopped ECS Tasks Error Messages](#stopped-ecs-tasks-error-messages)
  - [Stop an ECS Task](#stop-an-ecs-task)
    - [Assume Role ARN](#assume-role-arn)

### Authentication

Follow the instructions outlined in the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html) for Runbook Automation to authenticate with AWS.

When defining the IAM Role for Runbook Automation, be sure to include the permissions required by the specific plugins in the Policy associated with the role:

- **Run Command**:

  - `ssmmessages:CreateControlChannel`
  - `ssmmessages:CreateDataChannel`
  - `ssmmessages:OpenControlChannel`
  - `ssmmessages:OpenDataChannel`

- **Stopped Task Details**:

  - `ecs:ListTasks`
  - `ecs:DescribeTasks`

- **Stop ECS Task**:

  - `ecs:StopTask`

### Send Commands to ECS Containers

The **AWS / ECS / Run Command** plugin sends commands to specified ECS containers:

![ECS Command Example](https://docs.rundeck.com/docs/assets/img/aws-ecs-command-example.png)  
  

Sending commands to ECS containers makes it easier to collect diagnostic information and quickly troubleshoot errors. For example, in development, this allows you to easily interact with various processes in your containers and troubleshoot your applications. In production scenarios, this enables you to gain break-glass access to your containers to debug issues.

#### Prerequisites

1.  This feature requires a Task IAM role to grant containers the permissions needed for communication between the managed SSM agent (execute-command agent) and the SSM service. Use the following policy and attach it to your task definition as explained [here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html).
    <div class="language-text line-numbers-mode">

    ``` text
    {
       "Version": "2012-10-17",
       "Statement": [
           {
           "Effect": "Allow",
           "Action": [
                "ssmmessages:CreateControlChannel",
                "ssmmessages:CreateDataChannel",
                "ssmmessages:OpenControlChannel",
                "ssmmessages:OpenDataChannel"
           ],
          "Resource": "*"
          }
       ]
    }
    ```

    </div>
2.  Enable remote commands by adding the **`--enable-execute-command`** flag to one of the following AWS CLI Commands: `create-service`, `update-service`, `start-task`, or `run-task`. For example, with an existing Service:
    <div class="language-text line-numbers-mode">

    ``` text
     aws ecs create-service \
      --cluster cluster-name \
      --task-definition task-definition-name \
      --enable-execute-command \
      --service-name service-name \
      --desired-count 1
    ```

    </div>
3.  **\[Optional\]** If you set the task definition parameter `initProcessEnabled` to **`true`**, this starts the init process inside the container, which removes any zombie SSM agent child processes found. The following provides an example:
    <div class="language-text line-numbers-mode">

    ``` text
    {
        "taskRoleArn": "ecsTaskRole",
        "networkMode": "awsvpc",
        "requiresCompatibilities": [
            "EC2",
            "FARGATE"
        ],
        "executionRoleArn": "ecsTaskExecutionRole",
        "memory": ".5 gb",
        "cpu": ".25 vcpu",
        "containerDefinitions": [
            {
                "name": "amazon-linux",
                "image": "amazonlinux:latest",
                "essential": true,
                "command": ["sleep","3600"],
                "linuxParameters": {
                    "initProcessEnabled": true
                }
            }
        ],
        "family": "ecs-exec-task"
    }
    ```

    </div>

#### Configuration

The following fields are used for configuration the Workflow Step plugin to send commands to ECS containers:

- **Container Name**: The name of the ECS container to run the command on.
- **Cluster Name**: The name of the cluster where the container resides.
- **Task ID**: The ID the task associated with the specified container.
- **Command**: The shell command you wish to run on the specified container.
- **Container Region**: The region where the container's cluster is located.
- **Access Key ID**: AWS Access Key. This can be set in the Project configuration properties with `project.aws.access_key` or in [Configuration Management](https://docs.rundeck.com/docs/manual/configuration-mgmt/configmgmt.html).
- **Secret Key**: AWS Secret Key. Click the **Select** button to choose your AWS Secret from Key Storage. This can be set in the Project configuration properties with `project.aws.secret_key_path`.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/aws-ecs-command-example-config.png" alt="Example Configuration" />
<figcaption aria-hidden="true"><strong>Example Configuration</strong></figcaption>
</figure>

#### Executing Job Step

Once the Job step is configured, commands can be sent to the specified container. Start by hard-coding a specific command into the Job step as shown here:

![Hard Coded Command](https://docs.rundeck.com/docs/assets/img/aws-ecs-test-hard-coded-command.png)  

If this executes successfully, you would see the following output in the Job output logs:

![Command Output Logs](https://docs.rundeck.com/docs/assets/img/aws-ecs-command-log-output.png)  

To use this Job step as part of a larger workflow, or to create a ***"self service interface"***, you will likely want to use a Job Option (shown below) or a Data Variable as the input for the command. See here for more details on [Job Options](https://docs.rundeck.com/manual/job-options) and [Data Variables](https://docs.rundeck.com/docs/learning/howto/passing-variables.html):

![Using Job Options](https://docs.rundeck.com/docs/assets/img/aws-ecs-command-job-options.png)  
  

![Self Service](https://docs.rundeck.com/docs/assets/img/aws-ecs-command-self-service.png)  
  

### Stopped ECS Tasks Error Messages

The **AWS / ECS / Stopped Task Details** plugin checks a specified cluster for any **Stopped** ECS Tasks and provides their associated error messages:

![Stopped ECS Error](https://docs.rundeck.com/docs/assets/img/aws-ecs-stopped-task-errors.png)  

In order to use this plugin, you mused specify the **ECS Cluster Name**.

The IAM Policies required to use this plugin are:

- **`ecs:ListTasks`**
- **`ecs:DescribeTasks`**

See [here](https://docs.aws.amazon.com/AmazonECS/latest/userguide/stopped-task-error-codes.html) for more details on the Stopped ECS Tasks error message meanings.

### Stop an ECS Task

The **AWS / ECS / Stop** plugin *stops* a specific ECS Task. This can assist with auto-remediation of issues with ECS containers. There is both a **Workflow** *and* a **Node** step of this plugin.

In order to use the *Workflow* step plugin, you will need to specify the Cluster-ID (or ARN) *and* the Task-ID (or ARN):

![Stop ECS Task](https://docs.rundeck.com/docs/assets/img/aws-ecs-stop-task.png)  

The IAM Policies required to use this plugin are:

- **`ecs:StopTask`**

#### Assume Role ARN

There are cases when it is beneficial to use a different IAM Role than the one used for the [AWS PluginGroup](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html#setup) for the integration to retrieve the ECS Tasks and add them to the node inventory. For example, to target ECS Tasks from across multiple AWS Accounts, then a different IAM Role needs to be "assumed" in order to retrieve tasks from each AWS Account.

The **Assume Role ARN** field can be populated with an IAM Role ARN that Runbook Automation can assume *after* an authentication method has been provided through the PluginGroup.

By default, this plugin will use the `assume-role-arn` node-attribute from the ECS tasks added to the inventory through the [ECS Node Source](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/ecs-fargate.html). This can be overridden by placing an IAM role ARN into the field.
