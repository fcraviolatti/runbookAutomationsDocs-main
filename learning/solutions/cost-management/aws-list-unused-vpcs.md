---
title: "AWS - Identify Unused VPCs"
source_url: https://docs.rundeck.com/docs/learning/solutions/cost-management/aws-list-unused-vpcs.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS - Identify Unused VPCs

## Description

This automation job generates a listing of AWS Virtual Private Clouds (VPCs) that are not associated with any resources and are therefore eligible for deletion. It checks various AWS services to ensure comprehensive coverage.

## Prerequisites

- Turn on "[Runner as Node](https://docs.rundeck.com/administration/runner/runner-management/node-dispatch.html#runner-as-a-node)" setting on your Runner.
  - This requires version 5.8.0 or higher. Adjustments to Node tab may be required for earlier versions.
- AWS CLI installed on the runner node.
- Proper AWS credentials configured on the runner node.

## AWS IAM Permissions

The AWS IAM role or user associated with this job requires the following permissions:

- `ec2:DescribeVpcs`
- `ec2:DescribeInstances`
- `rds:DescribeDBInstances`
- `elb:DescribeLoadBalancers`
- `elbv2:DescribeLoadBalancers`
- `ec2:DescribeNatGateways`
- `ec2:DescribeVpnConnections`
- `ec2:DescribeTransitGatewayVpcAttachments`

<div class="language-json line-numbers-mode">

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeVpcs",
                "ec2:DescribeInstances",
                "rds:DescribeDBInstances",
                "elb:DescribeLoadBalancers",
                "elbv2:DescribeLoadBalancers",
                "ec2:DescribeNatGateways",
                "ec2:DescribeVpnConnections",
                "ec2:DescribeTransitGatewayVpcAttachments"
            ],
            "Resource": "*"
        }
    ]
}
```

</div>

These permissions should be applied to all resources in the specified region.

## Job Options

| Option Name           | Description                                                           | Default Value |
|-----------------------|-----------------------------------------------------------------------|---------------|
| `region`              | AWS region to query for VPCs                                          | N/A           |
| `always-show-results` | Show results even when checking AWS services results in Access Errors | false         |

## Job Workflow

1.  It uses the AWS CLI to list all VPCs in the specified region.
2.  The script then checks for VPCs associated with:
    - EC2 instances
    - RDS instances
    - Classic load balancers
    - Application/Network load balancers
    - NAT Gateways
    - VPN Connections
    - Transit Gateway attachments
3.  It compares the list of all VPCs against those associated with the above services.
4.  The job generates a report of VPCs that are not associated with any of these services and are eligible for deletion.

## Output

The job produces a detailed report with the following information:

- List of all VPCs in the region
- List of VPCs associated with various AWS services
- VPCs that can be safely deleted (not associated with any service)
- Warnings for default VPCs (which cannot be deleted)

## Script Details

The job uses a Bash script to perform the following tasks:

1.  Fetch all VPCs in the specified region
2.  Retrieve VPCs associated with various AWS services
3.  Compare the lists to identify unused VPCs
4.  Generate a report of VPCs eligible for deletion

## Notes

- The job does not actually delete any VPCs; it only provides recommendations.
- Default VPCs are excluded from the deletion recommendations.
- The script includes error handling and can optionally show the recommendation results even if some AWS API calls result in errors.

## Troubleshooting

If you encounter issues running this job:

1.  Ensure that the AWS CLI is properly installed on the runner node
2.  Verify that the AWS credentials on the runner node have the necessary permissions
3.  Check the `always-show-results` option if you want to see partial results in case of API errors
