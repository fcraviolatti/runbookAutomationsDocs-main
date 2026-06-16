---
title: "Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

## Public Cloud Providers

For individuals responding to incidents in the public cloud, useful diagnostics can be retrieved from the public-cloud provider about the health of the platform services as well as from the infrastructure and applications running on the public cloud provider. This section outlines methods for retrieving diagnostics from the public cloud providersâ€™ platform services. If youâ€™re looking for details on retrieving diagnostics from the OS, applications and databases, refer to their respective sections.

### AWS

For AWS users, some examples of diagnostics would be:

- Check the health of all EC2 instances behind an Application Load Balancer (ALB) or Elastic Load Balancer (ELB).
- Retrieve reasons for stopped ECS tasks.
- Look in CloudWatch logs for operating-system and application errors.

There are multiple plugins that allow users to pull diagnostics from common AWS Services:

- [Query CloudWatch Logs](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-cloudwatch.html#amazon-cloudwatch-logs-workflow-step-plugins)![Query CloudWatch Logs](https://docs.rundeck.com/docs/assets/img/aws-cloudwatch-logs-query-string.png)
- [Query Athena tables](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/amazon-athena.html#amazon-athena-query-workflow-step)
- [Check ELB Targets Status](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-elb-workflow-plugin.html#target-group-instance-statuses)
- [Retrieve failed ECS container messages](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-ecs-fargate.html#stopped-ecs-tasks-error-messages)
- [Invoke script via Lambda](https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/aws-lambda.html#aws-lambda-workflow-steps)![Lambda Function Job Step](https://docs.rundeck.com/docs/assets/img/aws-custom-lambda-code.png)

In addition to using the AWS Plugins, it is also possible to harness the AWS CLI within your Automation Instance:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/aws-cli-job-step.png" alt="AWS CLI in a Job Step" />
<figcaption aria-hidden="true">AWS CLI in a Job Step</figcaption>
</figure>

If using Runbook Automation Self-Hosted, or a [**Runner**](https://docs.rundeck.com/administration/runner), then you can also execute scripts that leverage the AWS SDK, such as Boto3 for python.

These multiple methods of communication with AWS allow you to be flexible in your approach for retrieving Diagnostics or managing your AWS environments.

### Azure

For users of Azure, the most common method of retrieving diagnostics from the public cloud platform is by â€œwrapping aroundâ€? the Azure CLI using the Command Job Step plugin. As an example, you may want to retrieve the health of a Function App:

<div class="language-text line-numbers-mode">

``` text
az monitor metrics list --resource myresource --resource-group myresourcegroup --resource-type "Microsoft.Web/sites" --metric "HealthCheckStatus" --interval 5m
```

</div>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/azure-cli-health-function-app.png" alt="Azure CLI checks health of Function App" />
<figcaption aria-hidden="true">Azure CLI checks health of Function App</figcaption>
</figure>

Another example would be to check the health of an Azure container registry:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/azure-cli-container-registry-health.png" alt="Azure CLI checks errors in Container Registry" />
<figcaption aria-hidden="true">Azure CLI checks errors in Container Registry</figcaption>
</figure>

> **Point of Interest**
>
> Azure has a full article [here](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-check-health) dedicated to diagnosing Container Registry behavior.  
> A diagnostic runbook could incorporate the  
> **`az acr check-health`** command and translate the output using the error codes found in [this article](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-health-error-reference).

There are multiple plugins that allow users to pull diagnostics from Azure services:

- [**Azure Node Source**](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/azure.html#azure-node-source)
- [**Azure Node Health Checks**](https://docs.rundeck.com/docs/manual/healthcheckplugins/azure-healthcheck.html#azure-health-check-enterprise-only)

### Google Cloud Platform (GCP)

For users of Google Cloud Platform (GCP), the most common method of retrieving diagnostics from the public cloud platform is by â€œwrapping aroundâ€? the **gcloud CLI** using the **Command** Job Step plugin. As an example, you can retrieve the current health status of instances in a backend service:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/gcloud-check-instances-health.png" alt="Gcloud CLI checks backend instances health" />
<figcaption aria-hidden="true">Gcloud CLI checks backend instances health</figcaption>
</figure>

> **Point of Interest**
>
> This blog from Google Cloud on [**Debugging Health Checks in Load Balancing**](https://cloudplatform.googleblog.com/2015/07/Debugging-Health-Checks-in-Load-Balancing-on-Google-Compute-Engine.html) on Google Compute Engine outlines a number of steps for diagnosing Health Check failures.  
> These steps can be treated as a runbook and â€œtransposedâ€? into your Automation instance using the Remote Command

There are multiple plugins that allow users to pull diagnostics from GCP services:

- [**GCP Compute Engine - Node Source**](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/gcp.html)
- [**GCP Compute Engine - Health Check**](https://docs.rundeck.com/docs/manual/healthcheckplugins/gcp-compute-healthcheck.html)
