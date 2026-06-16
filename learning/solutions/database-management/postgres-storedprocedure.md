---
title: "Executing PostgreSQL Stored Procedures"
source_url: https://docs.rundeck.com/docs/learning/solutions/database-management/postgres-storedprocedure.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Executing PostgreSQL Stored Procedures

Executing stored procedures in PostgreSQL allows you to run predefined database functions with parameters. This is useful for encapsulating business logic, maintaining consistent data operations, and improving database performance. The Execute PostgreSQL Stored Procedure job provides a secure and automated way to call stored procedures with parameters through the Enterprise Runner.

## Pre-requisites & Environment Setup

- Environment setup with active [Enterprise Runner](https://docs.rundeck.com/docs/administration/runner/).
- The `psql` command must be installed on the same machine as the Enterprise Runner and available in the default path.
- The Enterprise Runner must have access to an existing PostgreSQL instance.
- The stored procedure must exist in the target database
- The specified database user must have EXECUTE permissions on the stored procedure

## Example Stored Procedure Setup

Before using the job, ensure your stored procedure exists in the target database. Here's an example of creating a simple addition procedure:

<div class="language-sql line-numbers-mode">

``` sql
-- Create the stored procedure
CREATE OR REPLACE FUNCTION add_numbers(num1 integer, num2 integer)
RETURNS integer
LANGUAGE plpgsql
AS $$
BEGIN
    RETURN num1 + num2;
END;
$$;
```

</div>

## Configuration

**Database Host Name**: The host name or IP address of the PostgreSQL server.

**Database Name**: The name of the database.

**Database User Name**: The login name to authenticate to the PostgreSQL server.

**Login Password**: The password for the login name. \>(Note: The password can be provided directly as part of the input options. For production use we recommend using a Key Storage entry.)

**Stored Procedure Name**: The name of the stored procedure to execute (e.g., 'add_numbers').

**Stored Procedure Arguments**: Comma-separated list of arguments for the stored procedure (e.g., '5,3').

![job-options](https://docs.rundeck.com/docs/assets/img/solution-postgres-storedproc-joboptions.png)  

## Example Usage

To execute the add_numbers stored procedure:

Configure the database connection details

1.  Set the Stored Procedure Name to `add_numbers`
2.  Set the Stored Procedure Arguments to `5,3`
3.  The job will execute the procedure and return the result (8 in this example).

## Successful Execution

Successful Execution A successful execution will show the result returned by the stored procedure. For the add_numbers example:

<div class="language-text line-numbers-mode">

``` text
 add_numbers
-------------
           8
(1 row)
```

</div>

## Troubleshooting

Common issues and solutions:

- Error: function does not exist: Verify the stored procedure name and that it exists in the specified database
- Permission denied: Ensure the database user has EXECUTE permission on the stored procedure
- Wrong number of arguments: Verify the number and types of arguments match the stored procedure definition
