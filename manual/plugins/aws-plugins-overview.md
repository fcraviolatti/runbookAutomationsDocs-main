---
title: "AWS Plugins"
source_url: https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS Plugins

## Overview

Runbook Automation integrates with Amazon Web Services (AWS) through a variety of plugins listed below. By integrating Runbook Automation with AWS, users can provide a centralized, self-service interface for both simple and complex tasks spanning multiple cloud environments.

*Click to expand to see the full list of Runbook Automation plugins for AWS:*

| AWS Service Type          | Plugin                                                                                                                                                   | Plugin Type   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| **Athena**                | [Query Athena Table](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/amazon-athena.html)                                            | Job Step      |
| **CloudWatch**            | [Query CloudWatch logs On Demand](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch.html)                              | Job Step      |
| **CloudWatch**            | [Execute Saved CloudWatch Logs Query](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch.html)                          | Job Step      |
| **CloudWatch**            | [Create CloudWatch Log Stream](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws.html)                                            | Job Step      |
| **EC2**                   | [Start EC2](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws.html)                                                               | Job Step      |
| **EC2**                   | [Restart EC2](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/aws.html)                                                                 | Job Step      |
| **EC2**                   | [Delete EC2](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/aws.html)                                                                  | Job Step      |
| **EC2**                   | [Create EC2 from Snapshot](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws.html)                                                | Job Step      |
| **EC2**                   | [Update EC2 Autoscale Groups](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws.html)                                             | Job Step      |
| **EC2**                   | [EC2 Node Source](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/aws.html)                                                         | Node Source   |
| **ECS**                   | [ECS & Fargate Node Source](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/ecs-fargate.html)                                       | Node Source   |
| **ECS**                   | [ECS & Fargate Node Executor](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ecs.html)                                                 | Node Executor |
| **ECS**                   | [Execute Command](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-ecs-fargate.html)                                             | Job Step      |
| **ECS**                   | [Stopped Task Errors](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-ecs-fargate.html)                                         | Job Step      |
| **ECS**                   | [Stop Task](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-ecs-fargate.html)                                                   | Job Step      |
| **ELB**                   | [Unhealthy Target Group Instances](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-elb-workflow-plugin.html)                    | Job Step      |
| **Lambda**                | [Execute Lambda Function](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-lambda.html#execute-lambda-function)                  | Job Step      |
| **Lambda**                | [Execute Custom-Code Lambda Function](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-lambda.html#lambda-custom-code-execution) | Job Step      |
| **RDS**                   | [Check Instance Status](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-rds.html)                                               | Job Step      |
| **S3**                    | [Copy Files from Local to S3 or S3 to local](https://github.com/rundeck-plugins/aws-s3-steps.md)                                                         | Job Step      |
| **S3**                    | [List S3 objects](https://github.com/rundeck-plugins/aws-s3-steps.md)                                                                                    | Job Step      |
| **S3**                    | [Create an S3 Bucket](https://github.com/rundeck-plugins/aws-s3-steps.md)                                                                                | Job Step      |
| **S3**                    | [Move Files from Local to S3 or S3 to local](https://github.com/rundeck-plugins/aws-s3-steps.md)                                                         | Job Step      |
| **S3**                    | [Delete an S3 Bucket](https://github.com/rundeck-plugins/aws-s3-steps.md)                                                                                | Job Step      |
| **S3**                    | [Sync Directories and S3 Prefixes](https://github.com/rundeck-plugins/aws-s3-steps.md)                                                                   | Job Step      |
| **S3**                    | [S3 Log Storage](https://docs.rundeck.com/docs/administration/cluster/logstore/s3.html)                                                                  | Log Storage   |
| **Secrets Manager**       | [AWS Secrets Manager](https://docs.rundeck.com/docs/manual/key-storage/storage-plugins/aws-secrets-manager.html)                                         | Key Storage   |
| **Systems Manager (SSM)** | [SSM Node Executor](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ssm.html)                                                           | Node Executor |
| **Systems Manager (SSM)** | [SSM File Copier & Scripts](https://docs.rundeck.com/docs/manual/projects/node-execution/aws-ssm.html)                                                   | File Copier   |
| **VPC**                   | [Configure Flow Logs](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws.html)                                                     | Job Step      |
| **VPC**                   | [Enable Network Peering](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws.html)                                                  | Job Step      |

## Setup

The steps for integrating with AWS will vary depending on the product you are using:

[**Runbook Automation**](#aws-integration-for-runbook-automation) - Integration steps for Runbook Automation (Cloud) product.

[**Runbook Automation on EC2**](#aws-integration-for-process-automation-hosted-on-ec2) - For Runbook Automation hosted on EC2  
[**Runbook Automation on ECS**](#process-automation-hosted-on-ecs) - For Runbook Automation hosted on ECS  

[**Access Key & Secret Key**](#alternative-aws-authentication-access-key-secret-key) - For Runbook Automation when Access Keys are permitted.

> **Warning**
>
> Using the **Access Key and Secret Key** method is the ***least*** recommended approach for integrating with AWS and is the ***least secure***. The other methods of integration are highly recommended in place of using Access Key and Secret Key.

### AWS Integration for Runbook Automation

Runbook Automation can be integrated with one or more AWS Accounts using an IAM role with a **`Trust Relationship`**. More details on this authentication mechanism can be found in [this AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html). Here is a diagram that outlines this setup process:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/aws-iam-auth-diagram.png" alt="RBA Authentication Process with AWS" />
<figcaption aria-hidden="true">RBA Authentication Process with AWS</figcaption>
</figure>

Steps for setting up the integration for the entire Runbook Automation instance or for individual projects are outlined below:

**Part 1: In Runbook Automation:**  
To configure the AWS integration for the whole Runbook Automation instance:

1.  Click on the **System Menu** (gear icon) in the upper right.
2.  Click on **System Configuration**.
3.  Navigate to the **AWS** section and click on the **Pencil Icon** in the upper right.
4.  In the **IAM Role Delegation** section, copy the **Account ID** and **External ID** so that they may be used in subsequent steps: ![IAM AWS Auth](https://docs.rundeck.com/docs/assets/img/aws-iam-auth-rba-highlights.png)  
5.  Leave open this page so that the **`Role ARN`** can be filled in later.

To configure the AWS integration for an individual project:

1.  Navigate to **Project Configuration** within the specific project.
2.  Click on **Edit Configuration** then click on **Plugins**.
3.  Click on **+ Plugin Config** and select **AWS**
4.  In the **IAM Role Delegation** section, copy the **Account ID** and **External ID** so that they may be used in subsequent steps. ![IAM AWS Auth](https://docs.rundeck.com/docs/assets/img/aws-iam-auth-rba-highlights.png)  
5.  Leave open this page so that the **`Role ARN`** can be filled in later.

**Part 2: In AWS Console:**  

1.  Go to the AWS Management Console and open the **IAM** console at <https://console.aws.amazon.com/iam/>.

2.  In the navigation pane of the console, click **Roles** and then click **Create New Role**.

3.  For the **Trusted Entity Type** select **AWS Account** and then select **Another AWS Account**. ![Another AWS Account](https://docs.rundeck.com/docs/assets/img/another-aws-account.png)

4.  Paste in the AWS Account ID that was copied from **Step 4** in the prior section into the **Account ID** field.

5.  Click on **Require External ID**.

6.  Paste in the **External ID** that was copied from **Step 4** in the prior section into the **External ID** field.

7.  Click **Next**

8.  Select the ***Permissions Policies*** to attach to the role.

    > **Policy Selection**
    >
    > The selection should align with the specific automation use-case tasks for Runbook Automation. For example, if Runbook Automation will be used to retrieve and push data to S3, then be sure to include a policy that include the `s3:GetObject` and `s3:PutObject` permissions.

9.  Assign the **Role Name** and optionally add a description. Do **not** modify the `Select trusted entities` section.

10. Click **Create Role**.

11. In the IAM Roles list, find and select the newly created IAM Role.

12. Copy the **`ARN`** to be used in subsequent steps: ![IAM ARN](https://docs.rundeck.com/docs/assets/img/aws-copy-iam-arn.png)

**Part 3: In Runbook Automation:**  

1.  Paste the **`ARN`** copied from the prior section into the **`Role ARN`** field.
2.  Click **Save** to add this plugin configuration.
3.  Click **Save** to commit the configuration changes to the proejct.

The AWS authentication can be tested using the **Validate Credentials** Job step plugin. Otherwise, being using the rest of the AWS plugins that align with the permissions allocated to the IAM Role.

### AWS Integration for Runbook Automation hosted on EC2

When self-hosting Runbook Automation on EC2, the recommended method for integrating with AWS is to assign an IAM role to the EC2 virtual-machines:

1.  Go to the AWS Management Console and open the **IAM** console at <https://console.aws.amazon.com/iam/>.
2.  In the navigation pane of the console, click **Roles** and then click **Create New Role**.
3.  For the **Trusted Entity Type** select **AWS service**.
4.  Under **Common use cases** select **EC2** then click **Next**. ![Select Entity Type](https://docs.rundeck.com/docs/assets/img/aws-iam-select-entity-type.png)
5.  In the **Permissions policies**, select the permission-sets based on the plugins you intend to use.
    - For example, all of the [CloudWatch Logs Plugins](https://docs.rundeck.com/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch) require **`logs:StartQuery`** and **`logs:GetQueryResults`** while the [Execute Saved Query](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch.html#execute-saved-cloudwatch-logs-query) *also* requires **`logs:DescribeQueryDefinitions`**.  
      Then click **Next**.
6.  Specify a **Role Name** and a **Description**. Do not change the **Select trusted entities**.
7.  Click **Create Role**.
8.  Navigate to the **EC2** console and click on **Instances**.
9.  Click on the EC2 (or multiple instances if running a clustered setup) and click on **Actions** -\> **Security** -\> **Modify IAM Role**: ![Modify IAM Role](https://docs.rundeck.com/docs/assets/img/aws-modify-iam-role.png)
10. Click on **Choose IAM Role** and find the IAM Role you created in **Step 6** then click **Update IAM Role**: ![Update IAM Role](https://docs.rundeck.com/docs/assets/img/aws-update-ec2-iam-role.png)

Now that the IAM Role is attached to the EC2, use the following steps to define this authentication method in Runbook Automation:

**System Level**

1.  Click on the **System Menu** (gear icon) in the upper right.
2.  Click on **System Configuration**.
3.  Navigate to the **AWS** section and click on the **Pencil Icon** in the upper right.
4.  (Optional) Set a default **Region** to be used for all plugins.
5.  From the **Credential Provider** field dropdown, select **EC2**.
6.  Click **Save** in the lower right: ![EC2 Credential Provider - System Level](https://docs.rundeck.com/docs/assets/img/aws-iam-ec2-system-level.png)

**Project Level**

1.  In the specific project, click on **Project Settings** in the lower left.
2.  Click on **Edit Configuration** then click on **Plugins**.
3.  Click on **+PluginGroup**.
4.  Select **AWS** from the list: ![AWS Select PluginGroup Project Level](https://docs.rundeck.com/docs/assets/img/aws-select-plugingroup-project-level.png)
5.  (Optional) Select the default **Region** to be used for all plugins within this project.
6.  From the **Credential Provider** field dropdown, select **EC2**.
7.  Click **Save** in the lower right.

### Runbook Automation hosted on ECS

When self-hosting Runbook Automation on ECS, the recommended method for integrating with AWS is to assign an IAM role to the ECS Task Role:

1.  Go to the AWS Management Console and open the **IAM** console at <https://console.aws.amazon.com/iam/>.
2.  In the navigation pane of the console, click **Roles** and then click **Create New Role**.
3.  For the **Trusted Entity Type** select **AWS service**.
4.  Under **Common use cases** find **Elastic Container Task** in the dropdown under **User cases for other AWS services**: ![ECS IAM Role](https://docs.rundeck.com/docs/assets/img/aws-ecs-iam-select-use-case.png)
5.  In the **Permissions policies**, select the permission-sets based on the plugins you intend to use.
    - For example, all of the [CloudWatch Logs Plugins](https://docs.rundeck.com/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch) require **`logs:StartQuery`** and **`logs:GetQueryResults`** while the [Execute Saved Query](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch.html#execute-saved-cloudwatch-logs-query) *also* requires **`logs:DescribeQueryDefinitions`**.  
      Then click **Next**.
6.  Specify a **Role Name** and a **Description**. Do not change the **Select trusted entities**.
7.  Click **Create Role**.
8.  Navigate to the **ECS** console and click on **Task Definitions**.
9.  Select the Task Definition used for Runbook Automation and **Create new revision**.
10. Scroll down to the **Environment** section and select the role you created for the **Task Role** field: ![Assign IAM Role](https://docs.rundeck.com/docs/assets/img/aws-ecs-assign-task-role.png)

Now that the IAM Role is attached to the ECS Task, use the following steps to define this authentication method in Runbook Automation:

**System Level**

1.  Click on the **System Menu** (gear icon) in the upper right.
2.  Click on **System Configuration**.
3.  Navigate to the **AWS** section and click on the **Pencil Icon** in the upper right.
4.  (Optional) Set a default **Region** to be used for all plugins.
5.  From the **Credential Provider** field dropdown, select **ECS**.
6.  Click **Save** in the lower right: ![EC2 Credential Provider - System Level](https://docs.rundeck.com/docs/assets/img/aws-iam-ec2-system-level.png)

**Project Level**

1.  In the specific project, click on **Project Settings** in the lower left.
2.  Click on **Edit Configuration** then click on **Plugins**.
3.  Click on **+PluginGroup**.
4.  Select **AWS** from the list: ![AWS Select PluginGroup Project Level](https://docs.rundeck.com/docs/assets/img/aws-select-plugingroup-project-level.png)
5.  (Optional) Select the default **Region** to be used for all plugins within this project.
6.  From the **Credential Provider** field dropdown, select **ECS**.
7.  Click **Save** in the lower right.

### Alternative AWS Authentication: Access Key & Secret Key

1.  Create an AWS Access Key and Secret Key that is associated with an IAM Role, follow [these instructions](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

2.  Once the keys have been downloaded, add the Secret Key into Project or System Key Storage using the Password key type, following [these instructions](https://docs.rundeck.com/docs/manual/system-configs.html#key-storage).

    > **Tip**
    >
    > If using a third party credential-store, such as [Hashicorp Vault](https://docs.rundeck.com/learning/howto/vault-integration), then skip step 2.

Now that the AWS Secret Key has been added to Key Storage, use the following steps to configure authentication for either the entire system or for a specific project:

**System Level**

1.  Click on the **System Menu** (gear icon) in the upper right.
2.  Click on **System Configuration**.
3.  Navigate to the **AWS** section and click on the **Pencil Icon** in the upper right.
4.  Click the **Select** button next to **Key Storage Password** and find the AWS Secret that was saved in step 2 above.
5.  Place your AWS Access Key into the **Access Key ID** field.
6.  (Optional) Set a default **Region** to be used for all plugins ![AWS Secrets Config System Level](https://docs.rundeck.com/docs/assets/img/aws-secret-system-level.png)
7.  Click **Save** in the lower right.

**Project Level**

1.  In the specific project, click on **Project Settings** in the lower left.
2.  Click on **Edit Configuration** then click on **Plugins**.
3.  Click on **+PluginGroup**.
4.  Select **AWS** from the list: ![AWS Select PluginGroup Project Level](https://docs.rundeck.com/docs/assets/img/aws-select-plugingroup-project-level.png)
5.  Click the **Select** button next to **Key Storage Password** and find the AWS Secret that was saved in step 2 above.
6.  Place your AWS Access Key into the **Access Key ID** field.
7.  (Optional) Select the default **Region** to be used for all plugins within this project.
8.  Click **Save** in the lower right.
