---
title: "Installing Rundeck"
source_url: https://docs.rundeck.com/docs/administration/install/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Installing Rundeck

Installing Rundeck is a straightforward and efficient way to enhance your organization's workflow automation and streamline your IT operations. Rundeck is an open-source, web-based platform that provides a centralized interface for managing and executing tasks across multiple systems. With its intuitive design and robust features, Rundeck empowers users to create and schedule jobs, run ad-hoc commands, and orchestrate complex workflows with ease. Whether you're a system administrator, developer, or operations team member, installing Rundeck can significantly improve your team's productivity and operational efficiency. In this guide, we will explore the step-by-step process of installing Rundeck, ensuring you have all the necessary components and configuration to unleash the full potential of this powerful tool.

1.  [Review the system requirements](https://docs.rundeck.com/docs/administration/install/system-requirements.html)
2.  [Install Rundeck with chosen method](#installation)
3.  [Configure database](#database-configuration)
4.  [Configure Rundeck](#rundeck-configuration)

## Installation

> **Tips**
>
> Docker is fastest way to try out Rundeck

Docker

Deb

Rpm

Windows

Docker

<div class="language-bash line-numbers-mode">

``` bash
docker run --rm -it -p 4440:4440 rundeckpro/enterprise:5.20.1
```

</div>

**Check out the [Docker Zoo](https://github.com/rundeck/docker-zoo) for configuration examples in Docker Compose!** These examples cover common configuration scenarios including connecting to each supported database.

[Detailed Docker instructions can be found here.](https://docs.rundeck.com/docs/administration/install/docker.html)

Deb

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/deb-setup.sh 2> /dev/null | sudo bash -s rundeckpro
sudo apt-get install rundeckpro-enterprise
```

</div>

Import the repo signing key:

<div class="language-bash line-numbers-mode">

``` bash
curl -L https://packages.rundeck.com/pagerduty/rundeckpro/gpgkey | sudo apt-key add -
```

</div>

Add the following to `/etc/apt/sources.list.d/rundeck.list` replacing existing entries:

<div class="language-bash line-numbers-mode">

``` bash
deb https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
deb-src https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
```

</div>

Update apt cache and install:

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get update
sudo apt-get install rundeckpro-enterprise
```

</div>

[Detailed deb instructions can be found here.](https://docs.rundeck.com/docs/administration/install/linux-deb.html)

Rpm

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh 2> /dev/null | sudo bash -s rundeckpro
sudo yum install java rundeckpro-enterprise
```

</div>

Remove `bintray-rundeckpro-rpm.repo` if it exists.

Add the following entries to `/etc/yum.repos.d/rundeck.repo` replacing any existing entries:

<div class="language-properties line-numbers-mode">

``` properties
[rundeckpro]
name=rundeckpro
baseurl=https://packages.rundeck.com/pagerduty/rundeckpro/rpm_any/rpm_any/$basearch
repo_gpgcheck=1
gpgcheck=0
enabled=1
gpgkey=https://packages.rundeck.com/pagerduty/rundeckpro/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

</div>

<div class="language-bash line-numbers-mode">

``` bash
sudo yum install java rundeckpro-enterprise
```

</div>

[Detailed rpm instructions can be found here.](https://docs.rundeck.com/docs/administration/install/linux-rpm.html)

Windows

[Check here for detailed Windows installation instructions.](https://docs.rundeck.com/docs/administration/install/windows.html)

## Database Configuration

Rundeck requires a backend database to store and manage various types of data that are integral to its operation. The backend database serves as a repository for critical information such as job definitions, execution history, project configurations, and user accounts. By leveraging a database, Rundeck ensures data integrity, persistence, and scalability, allowing multiple users to collaborate seamlessly and access the platform's features concurrently.

The backend database plays a crucial role in enabling advanced functionalities within Rundeck, such as job scheduling, execution tracking, and historical data analysis. It allows users to define and store job definitions, which consist of instructions, scripts, and parameters necessary for performing tasks. Moreover, the database records execution history, including timestamps, execution statuses, and output logs, enabling users to review and troubleshoot job runs.

Furthermore, the backend database stores project configurations, which encompass project-specific settings, resource definitions, access controls, and notifications. This central storage ensures consistency and facilitates easy management of project-related data.

Overall, the backend database acts as a reliable foundation for Rundeck's core functionalities, providing a structured and efficient means of storing, retrieving, and organizing data essential for effective workflow automation and orchestration.

> **Warning**
>
> Rundeck will initialize an on-disk database using the embedded H2 database on first start using the stock configurations. Production installations of Rundeck running H2 are not supported! Choose a supported database below to configure a production installation.

### Edit Database Config

> **Tips**
>
> The Rundeck database (or schema) should be setup in advance. The following assumes the database is named `rundeck`.

Update your `rundeck-config.properties` file with settings from the following database list and restart Rundeck. This file is located in different locations depending on your installation method:

- **RPM/DEB**: `/etc/rundeck/rundeck-config.properties`
- **WAR/Custom**: `$RDECK_BASE/server/config/rundeck-config.properties`
- **Docker**: Check out the [Docker Zoo](https://github.com/rundeck/docker-zoo) for configuration examples of each database using Docker Compose!

Replace the following tokens in the instructions for each database:

- `<host>`: The database server hostname.
- `<rundeckuser>`: The database user with permissions on the `rundeck` database.
- `<rundeckpassword>`: The password for the Rundeck database user.

MySQL

PostgreSQL

SQL Server

Oracle

MySQL

<div class="language-properties line-numbers-mode">

``` properties
dataSource.url = jdbc:mysql://<host>/rundeck?autoReconnect=true&useSSL=false
dataSource.username = <rundeckuser>
dataSource.password = <rundeckpassword>
dataSource.driverClassName = org.mariadb.jdbc.Driver
```

</div>

[Detailed MySQL instructions.](https://docs.rundeck.com/docs/administration/configuration/database/mysql.html)

PostgreSQL

<div class="language-properties line-numbers-mode">

``` properties
dataSource.driverClassName = org.postgresql.Driver
dataSource.url = jdbc:postgresql://<host>/rundeck
dataSource.username=<rundeckuser>
dataSource.password=<rundeckpassword>
```

</div>

[Detailed PostgreSQL instructions.](https://docs.rundeck.com/docs/administration/configuration/database/postgres.html)

SQL Server

<div class="language-properties line-numbers-mode">

``` properties
dataSource.driverClassName = com.microsoft.sqlserver.jdbc.SQLServerDriver
dataSource.url = jdbc:sqlserver://<host>;DatabaseName=RUNDECK
dataSource.username = <rundeckuser>
dataSource.password = <rundeckpassword>
```

</div>

[Detailed SQL Server instructions.](https://docs.rundeck.com/docs/administration/configuration/database/mssql.html)

Oracle

<div class="language-properties line-numbers-mode">

``` properties
dataSource.url = jdbc:oracle:thin:@<host>:1521:orcl # (change server name and instance name)
dataSource.driverClassName = oracle.jdbc.OracleDriver
dataSource.username = <rundeckuser>
dataSource.password = <rundeckpassword>
dataSource.dialect = org.rundeck.hibernate.RundeckOracleDialect
dataSource.properties.validationQuery = SELECT 1 FROM DUAL
```

</div>

[Detailed Oracle instructions.](https://docs.rundeck.com/docs/administration/configuration/database/oracle.html)

> **Warning**
>
> When using passwords with **special characters**, ensure there are **no spaces** between the equal sign and the value provided: `dataSource.password=<rundeckpassword>`

## Rundeck Configuration

### Server URL

> **Warning**
>
> The configuration option `grails.serverUrl` **must** be set properly. The value should match the URL *users* would use to access Rundeck(ie the URL they would enter into the browser).

For **Docker** this should be configured with the `RUNDECK_GRAILS_URL` environment variable.

For **deb, rpm, and war** this will be set as `grails.serverUrl=` in the `rundeck-config.properties` file.

### Configuration Reference

[Docker](https://docs.rundeck.com/docs/administration/configuration/docker.html)  
[Configuration file reference](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html)
