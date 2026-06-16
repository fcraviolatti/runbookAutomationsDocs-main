---
title: "Log Rotation and Cleanup"
source_url: https://docs.rundeck.com/docs/learning/solutions/storage-management/storage-log-rotation.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Log Rotation and Cleanup

This documentation provides details on how to use a Rundeck job to manually rotate, compress, and clean up log files in a specified directory. This job is useful for managing log files to prevent them from consuming excessive disk space.

> **Note**
>
> This is just one example of how to implement a log rotation job. Other opportunities exist leveraging `logrotate` or other methods.

## Job Description

This job will:

- Rotate log files by renaming them with a timestamp.
- Compress the rotated log files to save disk space.
- Delete old log files that exceed a specified retention period.

### Assumptions

- The job assumes the node is a Linux endpoint with `bash` and `gzip` installed.
- The default log directory is `/var/log/myapp`, and should be customized.

### Notes

- No nodes are selected by default. Change Target Nodes and select the endpoint to run against. If multiple nodes are selected the same script will be run on each node.

## Configuration

### Job Options

- **Log Directory:** The path where the log files are located. The default is `/var/log/myapp`.
- **Retention Days:** The number of days to retain old log files. The default is `30` days.

![job-options](https://docs.rundeck.com/docs/assets/img/log-rotation-job-options.png)  

## Successful Execution

Upon successful execution, the job will:

- Rename current log files by appending a timestamp.
- Compress the renamed log files.
- Remove compressed log files older than the specified retention period.

![success-output](https://docs.rundeck.com/docs/assets/img/log-rotation-success-output.png)  

## Troubleshooting

- **Log Rotation Issues**: Ensure the log directory and file permissions are correctly set.
- **Compression Issues**: Verify that `gzip` is installed and accessible on the system.
- **Cleanup Issues**: Check the retention period and ensure the `find` command syntax is correct.

## Conclusion

This custom log rotation and cleanup job helps manage log files efficiently by rotating, compressing, and deleting old logs. Adjust the script and configuration parameters as needed to fit your specific requirements.
