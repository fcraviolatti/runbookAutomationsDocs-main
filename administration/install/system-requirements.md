---
title: "Instance System Requirements"
source_url: https://docs.rundeck.com/docs/administration/install/system-requirements.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Instance System Requirements

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Runbook Automation Self-Hosted</th>
<th>Rundeck Open Source</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Operating Systems</td>
<td><strong>Supported</strong>:<br />
<a href="https://docs.rundeck.com/docs/administration/install/linux-rpm.html">Red Hat Enterprise 8+/Amazon 2+/Oracle Linux 8+</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/linux-deb.html">Ubuntu 22.04.3+/Debian 11.8+</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/windows.html">Windows Server 2019+</a></td>
<td><strong>Recommended</strong>:<br />
<a href="https://docs.rundeck.com/docs/administration/install/linux-rpm.html">Red Hat Enterprise 8+/Amazon 2+/Oracle Linux 8+</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/linux-deb.html">Ubuntu 22.04.3+/Debian11.8+</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/windows.html">Windows Server 2019+</a></td>
</tr>
<tr class="even">
<td>Server Profile</td>
<td><strong>Recommended</strong>:<br />
32GB RAM<br />
(24GB JVM Heap)<br />
8 CPUs per instance<br />
<em>Equivalent to m4.2xlarge in AWS EC2</em><br />
<br />
<strong>Minimum</strong>:<br />
16GB RAM<br />
(12GB JVM Heap)<br />
4 CPUs per instance<br />
<em>Equivalent to m4.xlarge in AWS EC2</em></td>
<td><br />
<br />
<br />
<br />
<br />
<br />
<br />
<strong>Minimum</strong>:<br />
8GB RAM<br />
(4GB JVM Heap)<br />
2 CPUs per instance<br />
<em>Equivalent to m4.large in AWS EC2</em></td>
</tr>
<tr class="odd">
<td><a href="#database">Database</a></td>
<td><strong>Supported</strong>:<br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/mysql.html">MariaDB 10.11.6+/MySQL 8.0.35+</a><br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/postgres.html">PostgreSQL 15.5+</a><br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/mssql.html">Microsoft SQL Server 2022</a><br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/oracle.html">Oracle 19c+</a></td>
<td><strong>Recommended</strong>:<br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/mysql.html">MariaDB 10.11.6+/MySQL 8.0.35+</a><br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/postgres.html">PostgreSQL 15.5+</a><br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/mssql.html">Microsoft SQL Server 2022</a><br />
<a href="https://docs.rundeck.com/docs/administration/configuration/database/oracle.html">Oracle 19c+</a></td>
</tr>
<tr class="even">
<td><a href="#java">Java</a></td>
<td><a href="#java">Java 11/17 runtime</a> installed on each instance</td>
<td><a href="#java">Java 11/17 runtime</a> installed on each instance</td>
</tr>
<tr class="odd">
<td><a href="#logstore">Log Store</a></td>
<td><strong>Recommended</strong>:<br />
<a href="https://docs.rundeck.com/docs/learning/howto/S3-minio.html#s3-or-minio-for-execution-logs">S3-compatible object store</a></td>
<td>File system or<br />
<a href="https://docs.rundeck.com/docs/learning/howto/S3-minio.html#s3-or-minio-for-execution-logs">S3-compatible object store</a></td>
</tr>
<tr class="even">
<td>Install Method</td>
<td><a href="https://docs.rundeck.com/docs/administration/install/linux-rpm.html">.rpm</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/linux-deb.html">.deb</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/jar.html">Java servlet (.war)</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/docker.html">Docker</a></td>
<td><a href="https://docs.rundeck.com/docs/administration/install/linux-rpm.html">.rpm</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/linux-deb.html">.deb</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/jar.html">Java servlet (.war)</a><br />
<a href="https://docs.rundeck.com/docs/administration/install/docker.html">Docker</a></td>
</tr>
<tr class="odd">
<td><a href="#network-access">Network Ports</a></td>
<td>4443 (https)<br />
4440 (http)<br />
22 (Linux machines over SSH)<br />
5985 (Windows machines over http)<br />
5986 (Windows machines over https)</td>
<td>4443 (https)<br />
4440 (http)<br />
22 (Linux machines over SSH)<br />
5985 (Windows machines over http)<br />
5986 (Windows machines over https)</td>
</tr>
<tr class="even">
<td>Admin Access</td>
<td>Root (or Administrator on Windows) is not <a href="#admin-access">required or recommended</a>.</td>
<td>Root (or Administrator on Windows) is not <a href="#admin-access">required or recommended</a>.</td>
</tr>
<tr class="odd">
<td>Browser</td>
<td>Accessing automation typically requires an HTML5 compliant browser. Currently supported version of Mozilla Firefox or Google Chrome are recommended.</td>
<td>Accessing automation typically requires an HTML5 compliant browser. Currently supported version of Mozilla Firefox or Google Chrome are recommended.</td>
</tr>
</tbody>
</table>

## Java

Rundeck is a Java-Servlet based server and therefore requires the Java runtime.

As of version 5.10.0, Java 11 or Java 17 runtime versions are supported (JRE). Java must be installed prior to running the install process. Ensure the JAVA_HOME environment variable is defined properly in your environment before running the launcher. Installers will use the java found on your path. See [Setting JAVA_HOME](https://docs.rundeck.com/docs/administration/maintenance/startup.html#setting-java_home) if you want to run a different version of java.

Verify your Java version to check it meets the requirement:

<div class="language-text line-numbers-mode">

``` text
$ java -version
```

</div>

Example output (actual version numbers can vary)

<div class="language-text line-numbers-mode">

``` text
java version "11.0.7" 2020-04-14 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.7+8-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.7+8-LTS, mixed mode)
```

</div>

> **Java Versions**
>
> [Azul Zulu Open JDK](https://www.azul.com/downloads/?package=jdk#zulu) is what the software is built and tested with and is the recommended distribution.
>
> Sun/Oracle and other flavors of Java may work, but our team has limited capabilities to troubleshoot problems specific to those distributions. The [Azul Zulu Open JDK](https://www.azul.com/downloads/?package=jdk#zulu) is strongly recommended.
>
> - As of version 5.8.0 the [Enterprise Runner](https://docs.rundeck.com/docs/administration/runner/) supports either Java 11 or Java 17 runtime (JRE).
> - As of version 5.10.0 the [Self Hosted RBA and Rundeck Open Source](https://docs.rundeck.com/docs/administration/runner/) support either Java 11 or Java 17 runtime (JRE).
> - Building from source still requires Java 11 (JDK).

## Network access

When the server starts, it binds to several TCP ports by default:

- 4440 (http)
- 4443 (https)

To check if the ports are free on a Unix host, run:

<div class="language-text line-numbers-mode">

``` text
$ netstat -an | egrep '4440|4443'
```

</div>

If the ports are in use on the server, you will see output similar to below:

<div class="language-text line-numbers-mode">

``` text
tcp46 0 0 \*.4440 \*.\* LISTEN
```

</div>

The installation procedures describe how to choose different ports if there is a conflict.

In addition, TCP port 22 (by default) needs to be open on the clients for SSH.

Clients should be set up to allow the Rundeck server user to connect to the clients using SSH via public-key authentication. It should not prompt for a password. See [Configure remote machine for SSH](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html#configuring-remote-machine-for-ssh) for configuration details.

There are various ways for installing SSH on Windows; we recommend [Cygwin (opens new window)](https://www.cygwin.com/).

## Database

When you install the default Rundeck (Or Runbook Automation Self-Hosted) configuration, it will use H2, an embedded database. It is convenient to have an embedded database when testing or using it for a non-critical purpose. Using the H2 database is not considered safe for production because it is not resilient if Rundeck is not shutdown gracefully. When shutdown gracefully, Rundeck can write the data (kept in memory) to disk. If Rundeck is forcefully shutdown, the data is not guaranteed to be written to file on disk and will likely cause truncation and corruption.

Don't use the H2 embedded database for anything except testing and non-production.

For production instances, use an external database like [MariaDB/MySQL](https://docs.rundeck.com/docs/administration/configuration/database/mysql.html) or [PostgreSQL](https://docs.rundeck.com/docs/administration/configuration/database/postgres.html).

Also, be sure to locate your external database on a host with sufficient capacity and performance. Don't create a downstream bottleneck!

For more about setting the datasource see: [Configuration/Database](https://docs.rundeck.com/docs/administration/configuration/database/).

## Logstore 

Rundeck records all job execution data into the Logstore. By default, Rundeck is configured to use the local file system. Normally, that is defined by the framework.logs.dir system setting found in framework.properties.

For clustered setups with Runbook Automation, see: [Configuration/Logstore](https://docs.rundeck.com/docs/administration/cluster/logstore/).

## Admin Access 

Using a dedicated user account such as "rundeck" is recommended. If there is a need for root access, please set up the Rundeck user to have access via [sudo](https://en.wikipedia.org/wiki/Sudo).
