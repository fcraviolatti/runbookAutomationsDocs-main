---
title: "Amazon Athena Query Workflow Step"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/amazon-athena.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Amazon Athena Query Workflow Step

> **Available in PagerDuty Runbook Automation Commercial products.**

## About Amazon Athena

Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL.

Athena is out-of-the-box integrated with AWS Glue Data Catalog, allowing users to create a unified metadata repository across various services, crawl data sources to discover schemas and populate their Catalog with new and modified table and partition definitions, and maintain schema versioning.

To learn more about Amazon Athena, click [here](https://aws.amazon.com/athena).

## About the Amazon Athena Query Workflow Step Plugin

The Athena Query Workflow Step plugin allows users to make queries through Athena to their S3 data as part of their automated-runbook workflows: ![](https://docs.rundeck.com/docs/assets/img/aws-athena-job-step-config.png)  

## Configuration

Before queries can be made through Athena, data must be made available in S3. For documentation on connecting to data sources, click [here](https://docs.aws.amazon.com/athena/latest/ug/work-with-data-stores.html)

Once Athena has been connected with a data source, it is recommended by AWS to start with the **AWS Managed Policies** for Athena. These can be found [here](https://docs.aws.amazon.com/athena/latest/ug/managed-policies.html). Permissions can then be modified to suit the specific use-case for Runbook Automation.

### Authentication

Follow the instructions outlined in the [AWS Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/aws-plugins-overview.html) for Runbook Automation to authenticate with AWS.

When defining the IAM Role for Runbook Automation, be sure to include the following permissions in the Policy associated with the role:

- **`athena:StartQueryExecution`**
- **`athena:getQueryExecution`**
- **`athena:getQueryResults`**

### Job Step Configuration

1.  In a new or existing Job, click on **Add a step**.  
      
2.  In the **Workflow Steps** tab, search for and select **AWS / Athena / Query**.  
      
3.  Insert the SQL Query for Athena into the **Query** field.  
      
4.  Provide the Athena database into the **Database Field**.  
      
5.  Provide the S3 Bucket for the results of the SQL query into the **Bucket** field.  
      
6.  Select the **Region** where the Athena client and database resides.  
      
7.  Optionally provide the **Access Key ID** and **Secret Key** to set the AWS credential on a per Job basis - rather than at the Project or System levels.  
      
    ![](https://docs.rundeck.com/docs/assets/img/aws-athena-job-step-config.png)  

## Viewing Query Results

When a query to Athena is made through Runbook Automation, the **first 50 rows** of results from that query are visible in the Log Output of the Job execution: ![](https://docs.rundeck.com/docs/assets/img/aws-athena-output.png)  

To view the full log output of the Athena query, navigate to the link provided in the log-output.
