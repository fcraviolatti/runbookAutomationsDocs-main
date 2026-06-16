---
title: "AWS - Identify Unused Lambda Functions"
source_url: https://docs.rundeck.com/docs/learning/solutions/cost-management/aws-list-unused-lambda.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AWS - Identify Unused Lambda Functions

## Description

This automation job generates a listing of AWS Lambda functions and highlights any that may be eligible for deletion based on modification and execution dates provided as job inputs. It provides a detailed report of Lambda functions, including their last modified and last execution dates, and recommends whether to keep or delete each function.

## Prerequisites

- Turn on "[Runner as Node](https://docs.rundeck.com/administration/runner/runner-management/node-dispatch.html#runner-as-a-node)" setting on your Runner.
  - This requires version 5.8.0 or higher. Adjustments to Node tab may be required for earlier versions.
- AWS CLI installed on the runner node
- jq tool for JSON parsing installed on the runner node
- Proper AWS credentials configured on the runner node

## AWS IAM Permissions

The AWS IAM role or user associated with this job requires the following permissions:

- `lambda:ListFunctions`
- `logs:DescribeLogGroups`
- `logs:DescribeLogStreams`

These permissions should be applied to all resources (`"Resource": "*"`).

<div class="language-json line-numbers-mode">

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lambda:ListFunctions",
                "logs:DescribeLogGroups",
                "logs:DescribeLogStreams"
            ],
            "Resource": "*"
        }
    ]
}
```

</div>

## Job Options

| Option Name      | Description                                              | Default Value |
|------------------|----------------------------------------------------------|---------------|
| `Region`         | AWS region to query for Lambda functions                 | N/A           |
| `Execution Date` | List functions that have not been called since this date | N/A           |
| `Modified Date`  | List functions older than this date                      | N/A           |

## Job Workflow

1.  The job runs on a node with the tag "RUNNER"
2.  It uses the AWS CLI to list all Lambda functions in the specified region
3.  For each function, it retrieves:
    - The last modified date
    - The last execution date (from CloudWatch Logs)
4.  It compares these dates against the provided execution and modification thresholds
5.  The job generates a report for each function, including:
    - Function name
    - Last modified date
    - Last execution date
    - Recommendation to keep or delete the function

## Output

The job produces a detailed report with the following information for each Lambda function:

- Function name
- Last modified date
- Last execution date
- Recommendation: "Delete" or "Keep"

The recommendation output is color-coded for easy reading:

- Red background: Functions recommended for deletion
- Green background: Functions recommended to keep

## Script Details

The job uses a Bash script to perform the following tasks:

1.  Set up variables for the AWS region and date thresholds
2.  Convert input dates to Unix timestamps and ISO 8601 format
3.  List all Lambda functions in the specified region
4.  For each function:
    - Retrieve the last modified date
    - Check for associated CloudWatch Logs
    - Retrieve the last execution date from logs (if available)
    - Compare dates against thresholds
    - Generate a recommendation

## Notes

- The job does not actually delete any functions; it only provides recommendations
- Functions are recommended for deletion if both the last modified date and the last execution date are earlier than the provided thresholds
- If a function has no associated CloudWatch Logs, its last execution date will be shown as "No logs found"
- If a function has logs but no executions, its last execution date will be shown as "No execution found"
- The script is designed to work on both Linux and macOS systems

## Troubleshooting

If you encounter issues running this job:

1.  Ensure that the AWS CLI and jq are properly installed on the runner node
2.  Verify that the AWS credentials on the runner node have the necessary permissions
