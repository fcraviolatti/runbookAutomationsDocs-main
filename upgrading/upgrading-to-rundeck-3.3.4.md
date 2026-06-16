---
title: "Upgrading to Rundeck 3.3.4"
source_url: https://docs.rundeck.com/docs/upgrading/upgrading-to-rundeck-3.3.4.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Upgrading to Rundeck 3.3.4

## MySQL

> **Caution**
>
> **For MySQL users**: Starting with Rundeck `3.3.4` the MySQL JDBC driver will no longer be bundled in any of the distributions(war, deb, rpm, Docker, etc). You must take action for Rundeck to continue connecting to the database after upgrading.

The MariaDB Connector/J JDBC driver will continue to be bundled with Rundeck, and can be used as a replacement.

**For deb, rpm, and war**  
Set the following in `rundeck-config.properties`

<div class="language-properties line-numbers-mode">

``` properties
dataSource.driverClassName=org.mariadb.jdbc.Driver
```

</div>

**For Docker**  
Set the following environment variable:

<div class="language-bash line-numbers-mode">

``` bash
RUNDECK_DATABASE_DRIVER=org.mariadb.jdbc.Driver
```

</div>
