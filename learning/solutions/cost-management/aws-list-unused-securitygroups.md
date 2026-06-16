---
title: "AWS - Identify Unused Security Groups"
source_url: https://docs.rundeck.com/docs/learning/solutions/cost-management/aws-list-unused-securitygroups.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS - Identify Unused Security Groups

## Description

This automation job generates a listing of AWS security groups that are not associated with any network interfaces and are therefore eligible for deletion. It checks various AWS services to ensure comprehensive coverage.

## Prerequisites

- Turn on "[Runner as Node](https://docs.rundeck.com/administration/runner/runner-management/node-dispatch.html#runner-as-a-node)" setting on your Runner.
  - This requires version 5.8.0 or higher. Adjustments to Node tab may be required for earlier versions.
- AWS CLI installed on the runner node.
- Proper AWS credentials configured on the runner node.

## AWS IAM Permissions

The AWS IAM role or user associated with this job requires the following permissions:

- `ec2:DescribeSecurityGroups`
- `ec2:DescribeNetworkInterfaces`
- `elb:DescribeLoadBalancers`
- `elbv2:DescribeLoadBalancers`
- `rds:DescribeDBInstances`
- `elasticache:DescribeCacheClusters`
- `redshift:DescribeClusters`

These permissions should be applied to all resources in the specified region.

<div class="language-json line-numbers-mode">

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeNetworkInterfaces",
                "elb:DescribeLoadBalancers",
                "elbv2:DescribeLoadBalancers",
                "rds:DescribeDBInstances",
                "elasticache:DescribeCacheClusters",
                "redshift:DescribeClusters"
            ],
            "Resource": "*"
        }
    ]
}
```

</div>

## Job Options

| Option Name           | Description                                                           | Default Value |
|-----------------------|-----------------------------------------------------------------------|---------------|
| `region`              | AWS region to query for security groups                               | N/A           |
| `always-show-results` | Show results even when checking AWS services results in Access Errors | false         |

## Job Workflow

1.  It uses the AWS CLI to list all security groups in the specified region.
2.  The script then checks for security groups associated with:
    - Network interfaces
    - Classic load balancers
    - Application/Network load balancers
    - RDS instances
    - ElastiCache clusters
    - Redshift clusters
3.  It compares the list of all security groups against those associated with the above services.
4.  The job generates a report of security groups that are not associated with any of these services and are eligible for deletion.

## Output

The job produces a detailed report with the following information:

- List of all security groups in the region
- List of security groups associated with various AWS services
- Security groups that can be safely deleted (not associated with any service)
- Warnings for default security groups (which cannot be deleted)

## Script Details

The job uses a Bash script to perform the following tasks:

1.  Fetch all security groups in the specified region
2.  Retrieve security groups associated with various AWS services
3.  Compare the lists to identify unused security groups
4.  Generate a report of security groups eligible for deletion

## Notes

- The job does not actually delete any security groups; it only provides recommendations.
- Default security groups are excluded from the deletion recommendations.
- The script includes error handling and can optionally show the recommendation results even if some AWS API calls result in errors.

## Troubleshooting

If you encounter issues running this job:

1.  Ensure that the AWS CLI is properly installed on the runner node
2.  Verify that the AWS credentials on the runner node have the necessary permissions
3.  Check the `always-show-results` option if you want to see partial results in case of API errors
