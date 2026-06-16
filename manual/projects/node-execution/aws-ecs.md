---
title: "AWS Elastic Container Service (ECS) Node Executor"
source_url: https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ecs.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS Elastic Container Service (ECS) Node Executor

> **Available in PagerDuty Runbook Automation Commercial products.**

## About Amazon ECS

**Amazon ECS** is a fully managed container orchestration service that makes it easy for users to deploy, manage, and scale containerized applications.

AWS **Fargate** is a serverless compute engine that is compatible with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS).

## About the ECS Node Executor

The **Amazon ECS Node Executor** provides the ability to send commands to one or multiple containers running on ECS.

Sending commands to ECS containers makes it easier to collect diagnostic information and quickly troubleshoot errors. In development, this allows users to easily interact with various processes in your containers and troubleshoot applications. In production scenarios, this enables break-glass access to containers to debug issues.

This plugin is designed to work in conjunction with the [ECS-Fargate Node Source](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/ecs-fargate.html).

## Configuration

### Configure ECS Task and Service Definitions

1.  Attach a **Task IAM Role** to the **Task Definition** that grants containers the permissions needed for communication between the managed SSM agent (`execute-command` agent) and the SSM service. Use the following policy and attach it to the task definition as explained [**here**](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html).
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
3.  **\[Optional\]** If the task definition parameter `initProcessEnabled` is set to **`true`**, this starts the init process inside the container, which removes any zombie SSM agent child processes found. The following provides an example:
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

### Configure IAM Policy for Runbook Automation

### Authentication

Follow the instructions outlined in the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html) for Runbook Automation to authenticate with AWS.

When defining the IAM Role for Runbook Automation or Runbook Automation, be sure to include the following permissions in the Policy associated with the role:

**`ecs:ExecuteCommand`**

This IAM policy condition key can be used in tandem with other IAM policy condition keys to limit the access that Runbook Automation has within ECS:

- **`aws:ResourceTag/clusterTagKey`**
- **`ecs:ResourceTag/clusterTagKey`**
- **`aws:ResourceTag/taskTagKey`**
- **`ecs:ResourceTag/taskTagKey`**
- **`ecs:container-name`**
- **`ecs:cluster`**
- **`ecs:task`**
- **`ecs:enable-execute-command`**

Examples of IAM policies that restrict the access by Runbook Automation can be found [here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-exec.html).

## Executing Commands

In order to send commands to ECS Containers, first configure the [ECS-Fargate Node Source](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/ecs-fargate.html). This retrieves the ECS containers and presents them as nodes in Runbook Automation:

![](https://docs.rundeck.com/docs/assets/img/aws-ecs-node-inventory.png)

Once the containers have been added as nodes, Runbook Automation can send commands to them. This can be done through the **Commands** tab, or using the **Remote Command** Job step:

#### Ad-hoc Commands through the Commands Tab

1.  Navigate to the **Commands** tab in the sidebar menu.  
      
2.  In the Node Filter field, type in a Node Filter to specify the containers that the command should execute on. For example, **`ECS:Container-Image: spring.*`** filters only the containers where the container image starts with `spring`: ![](https://docs.rundeck.com/docs/assets/img/aws-ecs-node-filter.png)  
      
3.  In the **Enter a command** field, provide the command to be executed on the filtered containers. Click on **Run on 1 Node**. ![](https://docs.rundeck.com/docs/assets/img/aws-ecs-node-executor-command.png)  

#### Remote Command Job Step

1.  In a new or existing Job, click on **Add a step**.  
      
2.  In the **Node Steps** tab, click on **Command**.  
      
3.  Provide the command to send to the container and click **Save** to save the Job step: ![](https://docs.rundeck.com/docs/assets/img/aws-ecs-remote-command-step.png)  
      
4.  Towards the top of the page, click on the **Nodes** tab to modify the target Nodes for the Job.  
      
5.  The toggle should be set to **Dispatch to Nodes**.  
      
6.  In the **Node Filter** field, provide a filter that selects the containers that the commands should be executed on. For example, **`ECS:Container-Image: spring.*`**: ![](https://docs.rundeck.com/docs/assets/img/aws-ecs-job-node-filter.png)  
      
7.  Click **Save** at the bottom of the page to save the Job configuration.

## Example Job: Java Thread Dump from ECS Container

A sample implementation of executing commands on ECS containers can be seen in our [**Automated Diagnostics Solution**](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/).
