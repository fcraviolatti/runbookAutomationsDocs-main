---
title: "System Properties Configuration"
source_url: https://docs.rundeck.com/docs/administration/configuration/system-properties.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# System Properties Configuration

## What Are System Properties?

System properties are Java command-line options that configure how Rundeck starts and runs. They differ from [configuration file properties](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html) in important ways:

**System Properties (this page):**

- Set at JVM startup via `-Dpropertyname=value` flags
- Control server-level settings (ports, paths, SSL, JVM options)
- Require Rundeck restart to change
- Cannot be changed in configuration files

**Configuration File Properties ([rundeck-config.properties](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html)):**

- Set in configuration files like `rundeck-config.properties`
- Control application features and behavior
- Some support live refresh (Enterprise)
- Easier to manage and version control

## When to Use System Properties

Use system properties when you need to configure:

- **Server ports and binding** - HTTP/HTTPS ports, listening address
- **Installation paths** - Base directory, data directory, log directory
- **JVM settings** - Memory allocation, garbage collection
- **SSL/TLS configuration** - Certificate paths, protocols, cipher suites
- **Reverse proxy settings** - Forwarded headers, SSL termination
- **Override defaults** - Change config file location, enable/disable features at startup

**Common scenarios:**

- Changing the port from default 4440
- Running behind a load balancer or reverse proxy
- Setting custom installation directories
- Tuning JVM memory for high-volume environments
- Enforcing security settings that can't be changed at runtime

## How to Set System Properties

The method depends on how you installed Rundeck.

### Method 1: Executable WAR / JAR Installation

**Installation type:** [Executable WAR](https://docs.rundeck.com/docs/administration/install/jar.html), manual Java installation

**How to set:** Add properties directly to the `java` command using `-Dpropertyname=value` syntax.

**Example - Change port and increase memory:**

<div class="language-bash line-numbers-mode">

``` bash
java -server -Xmx4g -Xms1g \
  -Dserver.port=8080 \
  -Dserver.servlet.session.timeout=7200 \
  -jar rundeck-5.20.1-20260518.war
```

</div>

**Example - Enable SSL and set custom base directory:**

<div class="language-bash line-numbers-mode">

``` bash
java -server \
  -Dserver.https.port=4443 \
  -Drdeck.base=/opt/rundeck \
  -Drundeck.ssl.config=/opt/rundeck/server/config/ssl.properties \
  -jar rundeck-5.20.1-20260518.war
```

</div>

**Tips:**

- JVM options like `-Xmx4g` (max memory) come before `-D` properties
- Use `\` for line continuation in shell scripts
- Create a startup script to avoid typing this every time

------------------------------------------------------------------------

## System Properties Reference

### Server Network Settings

Configure ports and network binding.

| Property                         | Default     | Description                      | Example                                  |
|----------------------------------|-------------|----------------------------------|------------------------------------------|
| `server.port`                    | `4440`      | HTTP port for Rundeck            | `-Dserver.port=8080`                     |
| `server.https.port`              | `4443`      | HTTPS port (requires SSL config) | `-Dserver.https.port=443`                |
| `server.address`                 | `localhost` | Network interface to bind to     | `-Dserver.address=0.0.0.0`               |
| `server.servlet.context-path`    | `/`         | URL context path                 | `-Dserver.servlet.context-path=/rundeck` |
| `server.servlet.session.timeout` | `3600`      | Session timeout in seconds       | `-Dserver.servlet.session.timeout=7200`  |

**Common scenarios:**

- Change port from 4440: Use `server.port`
- Run on all interfaces: Set `server.address=0.0.0.0`
- Add URL path prefix: Use `server.servlet.context-path=/rundeck` to access at `http://host/rundeck`

### Installation Paths

Override default installation directories.

| Property                | Default                             | Description                     | When to Change          |
|-------------------------|-------------------------------------|---------------------------------|-------------------------|
| `rdeck.base`            | War directory or `/var/lib/rundeck` | Base installation directory     | Custom install location |
| `rundeck.server.logDir` | `$RDECK_BASE/logs`                  | Log file location               | Separate disk for logs  |
| `server.datastore.path` | `$RDECK_BASE/data`                  | Data storage directory          | Custom data location    |
| `java.io.tmpdir`        | System temp                         | Temporary directory for plugins | Performance, disk space |

**Example - Custom paths:**

<div class="language-bash line-numbers-mode">

``` bash
-Drdeck.base=/opt/rundeck \
-Drundeck.server.logDir=/var/log/rundeck \
-Dserver.datastore.path=/data/rundeck
```

</div>

### SSL/TLS Configuration

Enable and configure HTTPS.

| Property                                           | Default | Description                                            |
|----------------------------------------------------|---------|--------------------------------------------------------|
| `rundeck.ssl.config`                               | (none)  | Path to SSL configuration file (enables HTTPS)         |
| `rundeck.jetty.connector.forwarded`                | `false` | Enable X-Forwarded-\* header support for reverse proxy |
| `rundeck.jetty.connector.ssl.excludedProtocols`    | `SSLv3` | Comma-separated SSL protocols to disable               |
| `rundeck.jetty.connector.ssl.includedProtocols`    | (auto)  | Comma-separated SSL protocols to allow                 |
| `rundeck.jetty.connector.ssl.excludedCipherSuites` | (none)  | Cipher suites to disable                               |
| `rundeck.jetty.connector.ssl.includedCipherSuites` | (auto)  | Cipher suites to allow                                 |

**Example - Enable SSL:**

<div class="language-bash line-numbers-mode">

``` bash
-Drundeck.ssl.config=/etc/rundeck/ssl/ssl.properties
```

</div>

**Example - Behind reverse proxy:**

<div class="language-bash line-numbers-mode">

``` bash
-Drundeck.jetty.connector.forwarded=true
```

</div>

**See also:** [Configuring Rundeck for SSL](https://docs.rundeck.com/docs/administration/security/ssl.html)

### Authentication Settings

Configure authentication behavior at startup.

| Property                | Default                 | Description                        | When to Use                                 |
|-------------------------|-------------------------|------------------------------------|---------------------------------------------|
| `rundeck.jaaslogin`     | `true`                  | Enable JAAS authentication         | Set to `false` to use realm.properties only |
| `loginmodule.name`      | `RDpropertyfilelogin`   | JAAS login module name             | Custom JAAS configuration                   |
| `loginmodule.conf.name` | `jaas-loginmodule.conf` | JAAS config file name              | Custom JAAS config location                 |
| `default.user.name`     | (none)                  | Create default user on first start | Automated deployments                       |
| `default.user.password` | (none)                  | Password for default user          | Automated deployments                       |

**Example - Create default admin user:**

<div class="language-bash line-numbers-mode">

``` bash
-Ddefault.user.name=admin \
-Ddefault.user.password=changeme123
```

</div>

### Security Features

Security-related system properties.

| Property                         | Default | Description                                      |
|----------------------------------|---------|--------------------------------------------------|
| `rundeck.localExecutor.disabled` | `false` | Prevent local script execution on Rundeck server |

**When to use:** Disable local executor in production for security (force all executions to remote nodes).

<div class="language-bash line-numbers-mode">

``` bash
-Drundeck.localExecutor.disabled=true
```

</div>

### Configuration Files

Override default configuration file locations.

| Property                  | Default                     | Description                                                  |
|---------------------------|-----------------------------|--------------------------------------------------------------|
| `rundeck.config.name`     | `rundeck-config.properties` | Name of main config file                                     |
| `logging.config`          | (auto)                      | Absolute path to log4j2 config (required for RPM/DEB/Docker) |
| `log4j.configurationFile` | (auto)                      | Alternative log4j2 config path                               |

**Example - Custom config file:**

<div class="language-bash line-numbers-mode">

``` bash
-Drundeck.config.name=rundeck-config-production.properties
```

</div>

**Example - Custom logging config:**

<div class="language-bash line-numbers-mode">

``` bash
-Dlogging.config=/etc/rundeck/log4j2-custom.properties
```

</div>

------------------------------------------------------------------------

## Common Configuration Examples

### Example 1: Production Server (Port 80, Custom Paths)

<div class="language-bash line-numbers-mode">

``` bash
# RPM/DEB: /etc/sysconfig/rundeckd or /etc/default/rundeckd
RDECK_JVM_SETTINGS="-Xmx8g -Xms2g -server"
RDECK_JVM_OPTS="-Dserver.port=80 \
  -Drundeck.server.logDir=/var/log/rundeck \
  -Dserver.datastore.path=/data/rundeck"
```

</div>

### Example 2: Behind Load Balancer with SSL Termination

<div class="language-bash line-numbers-mode">

``` bash
RDECK_JVM_OPTS="-Dserver.port=8080 \
  -Drundeck.jetty.connector.forwarded=true"
```

</div>

### Example 3: Development Server (High Memory, Custom Port)

<div class="language-bash line-numbers-mode">

``` bash
java -server -Xmx4g \
  -Dserver.port=4441 \
  -Dserver.servlet.session.timeout=86400 \
  -jar rundeck.war
```

</div>

### Example 4: Secure Production (HTTPS, No Local Execution)

<div class="language-bash line-numbers-mode">

``` bash
RDECK_JVM_OPTS="-Drundeck.ssl.config=/etc/rundeck/ssl/ssl.properties \
  -Dserver.https.port=443 \
  -Drundeck.localExecutor.disabled=true \
  -Drundeck.jetty.connector.ssl.excludedProtocols=SSLv3,TLSv1,TLSv1.1"
```

</div>

------------------------------------------------------------------------

## Additional Resources

- [Configuration File Reference](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html) - Properties in rundeck-config.properties
- [SSL Configuration](https://docs.rundeck.com/docs/administration/security/ssl.html) - Detailed SSL/TLS setup
- [Reverse Proxy Configuration](https://docs.rundeck.com/docs/administration/security/ssl.html#using-an-ssl-terminated-proxy) - Running behind nginx, Apache, etc.
- [JVM Tuning](https://docs.rundeck.com/docs/administration/maintenance/tuning-rundeck.html) - Memory and performance optimization

### Method 2: RPM / DEB Package Installation

**Installation type:** Installed via `yum`, `apt`, or package manager

**How to set:** Edit the "defaults" file for your distribution.

| Distribution                          | File to Edit              |
|---------------------------------------|---------------------------|
| **RPM** (RHEL, CentOS, Rocky, Fedora) | `/etc/sysconfig/rundeckd` |
| **DEB** (Debian, Ubuntu)              | `/etc/default/rundeckd`   |

> **Warning**
>
> **Do NOT edit `/etc/rundeck/profile` directly!**
>
> The `profile` file may be overwritten during upgrades, and your changes will be lost. Always use the defaults file above.

#### Adding System Properties

Edit your defaults file and set the `RDECK_JVM_OPTS` variable:

**Example - Change port:**

<div class="language-bash line-numbers-mode">

``` bash
# /etc/sysconfig/rundeckd (RPM) or /etc/default/rundeckd (DEB)
RDECK_JVM_OPTS="-Dserver.port=8080"
```

</div>

**Example - Multiple properties:**

<div class="language-bash line-numbers-mode">

``` bash
RDECK_JVM_OPTS="-Dserver.port=8080 -Dserver.servlet.session.timeout=7200"
```

</div>

**Example - Increase memory and change port:**

<div class="language-bash line-numbers-mode">

``` bash
RDECK_JVM_SETTINGS="-Xmx4g -Xms1g -server"
RDECK_JVM_OPTS="-Dserver.port=8080"
```

</div>

#### Applying Changes

After editing the defaults file:

<div class="language-bash line-numbers-mode">

``` bash
# Restart Rundeck
sudo systemctl restart rundeckd

# Or for older systems
sudo service rundeckd restart
```

</div>

------------------------------------------------------------------------

## Environment Variables Reference (RPM/DEB Only)

**Applies to:** RPM and DEB package installations only

These environment variables are pre-configured in `/etc/rundeck/profile`. You can override them in your defaults file (`/etc/sysconfig/rundeckd` or `/etc/default/rundeckd`).

### Directory Path Variables

Override these to change where Rundeck stores data, logs, and configuration.

| Variable            | Default                     | Description                  | When to Override           |
|---------------------|-----------------------------|------------------------------|----------------------------|
| `RDECK_BASE`        | `/var/lib/rundeck`          | Base installation directory  | Custom install location    |
| `RDECK_CONFIG`      | `/etc/rundeck`              | Configuration files location | Non-standard config path   |
| `RDECK_PROJECTS`    | `/var/lib/rundeck/projects` | Projects directory           | Separate disk for projects |
| `RUNDECK_LOGDIR`    | `/var/lib/rundeck/logs`     | Log files directory          | Separate disk for logs     |
| `RUNDECK_TEMPDIR`   | `/tmp/rundeck`              | Temporary files              | Performance, disk space    |
| `RUNDECK_WORKDIR`   | `/var/lib/rundeck/work`     | Working directory            | Separate disk              |
| `RDECK_SERVER_DATA` | `/var/lib/rundeck/data`     | Data storage                 | Separate disk for data     |

**Example - Custom paths:**

<div class="language-bash line-numbers-mode">

``` bash
# /etc/sysconfig/rundeckd or /etc/default/rundeckd
RDECK_BASE="/opt/rundeck"
RUNDECK_LOGDIR="/var/log/rundeck"
RDECK_PROJECTS="/data/rundeck/projects"
```

</div>

### JVM Configuration Variables

Control Java memory and performance settings.

| Variable             | Default                      | Description                  |
|----------------------|------------------------------|------------------------------|
| `RDECK_JVM_SETTINGS` | `-Xmx1024m -Xms256m -server` | JVM memory and options       |
| `RDECK_JVM_OPTS`     | (empty)                      | Additional system properties |

**Example - Increase memory:**

<div class="language-bash line-numbers-mode">

``` bash
# Allocate 4GB max memory, 1GB initial
RDECK_JVM_SETTINGS="-Xmx4g -Xms1g -server"
```

</div>

### Network Configuration Variables

Override default ports.

| Variable           | Default | Description |
|--------------------|---------|-------------|
| `RDECK_HTTP_PORT`  | `4440`  | HTTP port   |
| `RDECK_HTTPS_PORT` | `4443`  | HTTPS port  |

**Example - Custom ports:**

<div class="language-bash line-numbers-mode">

``` bash
RDECK_HTTP_PORT=8080
RDECK_HTTPS_PORT=8443
```

</div>

### Authentication Variables

Configure authentication method.

| Variable       | Default                              | Description                |
|----------------|--------------------------------------|----------------------------|
| `JAAS_LOGIN`   | `true`                               | Enable JAAS authentication |
| `JAAS_CONF`    | `/etc/rundeck/jaas-loginmodule.conf` | JAAS config file           |
| `LOGIN_MODULE` | `RDpropertyfilelogin`                | Login module name          |

### SSL/TLS Variables

Configure trust store for SSL connections.

| Variable                | Default                       | Description                   |
|-------------------------|-------------------------------|-------------------------------|
| `RDECK_TRUSTSTORE_FILE` | `/etc/rundeck/ssl/truststore` | Java truststore path          |
| `RDECK_TRUSTSTORE_TYPE` | `jks`                         | Truststore type (jks, pkcs12) |

### Security Variables

| Variable                  | Default | Description                    |
|---------------------------|---------|--------------------------------|
| `DISABLED_LOCAL_EXECUTOR` | `false` | Disable local script execution |

------------------------------------------------------------------------

## Complete Example Configuration

Here's a complete example for a production RPM/DEB installation:

<div class="language-bash line-numbers-mode">

``` bash
# /etc/sysconfig/rundeckd (RPM) or /etc/default/rundeckd (DEB)

# JVM Memory Settings
RDECK_JVM_SETTINGS="-Xmx8g -Xms2g -server"

# Network Configuration
RDECK_HTTP_PORT=8080
RDECK_JVM_OPTS="-Drundeck.jetty.connector.forwarded=true"

# Custom Paths
RDECK_BASE="/opt/rundeck"
RUNDECK_LOGDIR="/var/log/rundeck"
RDECK_PROJECTS="/data/rundeck/projects"

# Security
DISABLED_LOCAL_EXECUTOR=true

# Session Timeout
RDECK_JVM_OPTS="$RDECK_JVM_OPTS -Dserver.servlet.session.timeout=7200"
```

</div>

After making changes, restart Rundeck:

<div class="language-bash line-numbers-mode">

``` bash
sudo systemctl restart rundeckd
```

</div>
