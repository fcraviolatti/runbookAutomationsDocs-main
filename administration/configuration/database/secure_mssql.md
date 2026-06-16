---
title: "Security mode for Microsoft\u00c2\u00ae SQL Server"
source_url: https://docs.rundeck.com/docs/administration/configuration/database/secure_mssql.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Security mode for MicrosoftÂ® SQL Server

Tested version

- Currently Supported Rundeck version and related system requirements.

To enable security mode with SQL Server when executing rundeck.

Copy the "sqljdbc_auth.dll" file to correct folder

32 Bit: `\JDBC_SQL_Server\sqljdbc_4.1\enu\auth\x86\sqljdbc_auth.dll`

64 Bit: `\JDBC_SQL_Server\sqljdbc_4.1\enu\auth\x64\sqljdbc_auth.dll`

If is java 32 bits, the dll ( 32 bits ) should be copied to `c:\windows\`

If is java 64 bits, the dll ( 64 bits ) should be copied to `c:\windows\system32`

Some common errors may occur like the following

1.- Library not found

<div class="language-log line-numbers-mode">

``` log
com.microsoft.sqlserver.jdbc.SQLServerException: This driver is not configured for integrated authentication. ClientConnectionId:9dee6baf-4f79-4b42-984b-7f623e310e1d
```

</div>

2.- If Rundeck was started from a different domain than the database server this error may occurs.

<div class="language-log line-numbers-mode">

``` log
com.microsoft.sqlserver.jdbc.SQLServerException: Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication. ClientConnectionId:933d902b-1a74-429c-974c-5c20d9a588d0
        at com.microsoft.sqlserver.jdbc.SQLServerException.makeFromDatabaseError(SQLServerException.java:259)
```

</div>

One solution is to use "localhost" in the jdbc connection

3.- Different architecture error

<div class="language-log line-numbers-mode">

``` log
Configuring Spring Security Core ...
... finished configuring Spring Security Core

2018-10-12 23:54:37.224  WARN --- [           main] c.m.s.jdbc.internals.AuthenticationJNI   : Failed to load the sqljdbc_auth.dll cause : C:\Windows\sqljd
bc_auth.dll: Can't load AMD 64-bit .dll on a IA 32-bit platform
2018-10-12 23:54:51.724 ERROR --- [           main] o.a.tomcat.jdbc.pool.ConnectionPool      : Unable to create initial connections of pool.
```

</div>

Example configuration in rundeck.config

<div class="language-properties line-numbers-mode">

``` properties
dataSource.driverClassName = com.microsoft.sqlserver.jdbc.SQLServerDriver
dataSource.url = jdbc:sqlserver://mssql.rundeck.local;integratedSecurity=true;DatabaseName=rundeck
dataSource.username = rundeckuser
dataSource.password = rundeckpassword
```

</div>
