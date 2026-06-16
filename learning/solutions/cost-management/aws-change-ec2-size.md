---
title: "AWS - Change EC2 Instance Size"
source_url: https://docs.rundeck.com/docs/learning/solutions/cost-management/aws-change-ec2-size.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS - Change EC2 Instance Size

## Description

This automation job allows you to safely modify the instance type of an EC2 instance. The job handles the complete workflow including stopping the instance, changing its size, and optionally restarting it.

## Prerequisites

- Turn on "[Runner as Node](https://docs.rundeck.com/administration/runner/runner-management/node-dispatch.html#runner-as-a-node)" setting on your Runner.
  - This requires version 5.8.0 or higher. Adjustments to Node tab may be required for earlier versions.
- AWS CLI installed on your runner.
- AWS EC2 Node Source configured with "Show only Running instances" set to "No". (Details below)
- Sufficient AWS IAM permissions to modify EC2 instances

## AWS IAM Permissions

The AWS IAM role or user associated with this job requires the following permissions:

- `ec2:StopInstances`
- `ec2:StartInstances`
- `ec2:ModifyInstanceAttribute`
- `ec2:DescribeInstances`
- `ec2:DescribeInstanceTypeOfferings`

<div class="language-json line-numbers-mode">

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:StopInstances",
                "ec2:StartInstances",
                "ec2:ModifyInstanceAttribute",
                "ec2:DescribeInstances",
                "ec2:DescribeInstanceTypeOfferings"
            ],
            "Resource": "*"
        }
    ]
}
```

</div>

## Important Node Source Configuration

When using this job with EC2 instances, a specific Node Source configuration is required:

**Why**: EC2 instances must be in a stopped state before their instance type can be modified. Therefore, the Node Source must be able to discover both running AND stopped instances.

**Required Setting**:

- In your EC2 Node Source configuration
- Set "Show only Running Instances" to "No"

If this setting remains set to "Yes", stopped instances will not be visible to Rundeck and the job will fail to locate the target instance.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/solutions-aws-change-ec2-nodesource.png" />
</figure>

## Job Options

| Option Name         | Description                                         | Required | Default |
|---------------------|-----------------------------------------------------|----------|---------|
| `new-instance-type` | The target EC2 instance type                        | Yes      | N/A     |
| `start-instance`    | Whether to restart the instance after changing size | Yes      | Yes     |

Available instance types include various sizes across these families:

- General Purpose: t3, m5
- Compute Optimized: c5
- Memory Optimized: r5
- Storage Optimized: i3
- Accelerated Computing: p3, g4dn

## Job Workflow

The job executes the following steps in sequence:

1.  Stops the target EC2 instance
2.  Verifies instance state and performs validation:
    - Confirms instance has reached 'stopped' state
    - Validates new instance type is supported in the region
3.  Changes the instance type
4.  Optionally restarts the instance (based on `start-instance` option)

## Script Details

The job uses a combination of AWS CLI commands and a Bash script to:

1.  Stop the instance safely
2.  Wait up to 30 seconds for instance to reach stopped state
3.  Verify the new instance type is supported in the region
4.  Modify the instance attribute to change the instance type
5.  Start the instance if requested

## Error Handling

The script includes several error checks:

- Verifies instance reaches stopped state before proceeding
- Validates instance type compatibility in the region
- Confirms successful instance type modification
- Exits with appropriate error codes and messages on failures

## Notes

- The job will not proceed with the instance type change if the instance fails to stop
- If the change step fails, the instance will remain in a stopped state
- The job supports cross-family instance type changes (e.g., t3 to m5)
- Default node filtering is configured to target EC2 instances using the tag 'ec2', but you must pick the nodes at the time of execution.

## Troubleshooting

If you encounter issues:

1.  Verify the target instance is accessible and in a valid state
2.  Ensure the new instance type is supported in your region
3.  Check AWS credentials and permissions
4.  Review job logs for specific error messages
