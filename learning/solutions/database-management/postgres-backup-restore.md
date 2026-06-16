---
title: "Backup and Restore a PostgreSQL Database"
source_url: https://docs.rundeck.com/docs/learning/solutions/database-management/postgres-backup-restore.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Backup and Restore a PostgreSQL Database

Ad hoc database backups and restores in PostgreSQL are essential for various operational and strategic purposes. These on-demand processes provide flexibility in managing data, ensuring business continuity, and facilitating development and testing. Common reasons include migrating data between servers or environments, creating copies for testing major changes without affecting production, recovering from data corruption or accidental deletions, setting up development environments with real-world data, and complying with regulatory requirements for data preservation. Ad hoc backups also allow for point-in-time recovery, which is crucial when addressing critical errors or rolling back unintended changes. Additionally, they support performance tuning efforts by allowing administrators to experiment with different configurations on a copy of the database. Overall, the ability to perform ad hoc backups and restores is a vital tool in a database administrator's toolkit, enabling rapid response to various scenarios and maintaining the integrity and availability of data.

## Pre-requisites & Environment Setup

- Environment setup with active [Enterprise Runner](https://docs.rundeck.com/docs/administration/runner/).
- The Backup job requires that the `pg_dump` command to be installed on the same machine as the Enterprise Runner and be available in the default path.
- The Restore job requires the `psql` command to be installed on the same machine as the Enterprise Runner and be available in the default path.
- The Restore job will need to access the `.sql` file to import from the Enterprise Runner.
- The Enterprise Runner must have access to an existing PostgreSQL instance.
- Be sure to select a runner before starting the job. No Runners are selected by default.

## Backup Job

1.  The output will be written to a plain text SQL file.
2.  The SQL file will be read out using cat to the output log.
3.  The SQL file will then be optionally deleted as a cleanup step based on the input choice. If you plan to restore the file choose `No` for the delete option.

**Database Host Name**: The host name or IP address of the PostgreSQL server.

**Database Name**: The name of the database to backup.

**Database User Name**: The login name to authenticate to the PostgreSQL server.

**Login Password**: The password for the login name. \>(Note: The password can be provided directly as part of the input options. For production use we recommend using a Key Storage entry.)

**Delete the File?**: Should the job delete the SQL output file at the end of the job? Answer `Yes` to just view the SQL definition in the job log. Answer `No` if you plan to use the SQL file to restore a database.

![job-options](https://docs.rundeck.com/docs/assets/img/solutions-postgres-backup-options.png)  

### Successful Execution

![success-output](https://docs.rundeck.com/docs/assets/img/solutions-postgres-backup-success.png)  

## Restore Job

1.  The job will read the `.sql` file from the path provided and use `psql` to rebuild the database.

> The first four Job options are same as Backup job above

**SQL File Path**: This value needs to be a path to the `.sql` file with the database to import. Example: *./mytestdb.sql* to use a file from the default execution directory of the Enterprise Runner.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/solutions-postgres-restore-options.png" alt="job-options-restore" />
<figcaption aria-hidden="true">job-options-restore</figcaption>
</figure>

### Successful Execution

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/solutions-postgres-restore-output.png" alt="job-success-restore" />
<figcaption aria-hidden="true">job-success-restore</figcaption>
</figure>

> Note: The errors in the screenshot above are expected as the table was not deleted prior to executing.
