---
title: "Rundeck Configuration"
source_url: https://docs.rundeck.com/docs/administration/configuration/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Rundeck Configuration

This guide helps you configure Rundeck to meet your organization's needs. Configuration approach varies based on your Rundeck edition and deployment method.

## Configuration Methods

### Rundeck Enterprise / Process Automation

**GUI-Based Configuration:** Enterprise editions provide a System Configuration interface in the web UI for managing most settings without editing files directly. Navigate to System Menu â†’ System Configuration to configure plugins, database connections, and other settings through forms.

**File-Based Configuration:** Advanced settings and some deployment-specific configurations still require editing configuration files like `rundeck-config.properties` and `framework.properties`.

### Rundeck Open Source

**File-Based Configuration Only:** All configuration is done by editing files in the Rundeck installation directory. Common files include:

- `rundeck-config.properties` - Primary configuration file
- `framework.properties` - Framework and plugin settings
- `realm.properties` - User authentication

See the [Configuration File Reference](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html) for complete details on all available properties.

------------------------------------------------------------------------

## Getting Started: Configuration Checklist

### First-Time Setup (All Editions)

**Essential configurations to complete after installation:**

1.  **Database** - Configure an external database for production use (default H2 is for testing only)

    - [Database Configuration â†’](https://docs.rundeck.com/administration/configuration/database/)

2.  **Authentication** - Set up user authentication beyond the default admin account

    - [Authentication & Security â†’](https://docs.rundeck.com/docs/administration/security/authentication.html)

3.  **Email Notifications** - Configure SMTP for job notifications and alerts

    - [Email Settings â†’](https://docs.rundeck.com/docs/administration/configuration/email-settings.html)

4.  **Base URL** - Set `grails.serverURL` to match your hostname/domain

    - [Configuration File Reference â†’](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html)

### Docker Deployments

If you're running Rundeck in Docker, configuration uses environment variables instead of editing files directly:

- Environment variables override configuration file settings
- Volume mounts for persistent data and custom configurations
- Extended Docker images for custom plugins or dependencies

[View Docker Configuration Guide â†’](https://docs.rundeck.com/administration/configuration/docker)

### Cluster Deployments (Enterprise)

Additional requirements for high-availability clusters:

- Shared external database (required)
- Load balancer configuration
- Shared log storage (S3, Azure, or file system)
- Autotakeover and heartbeat settings
- Common authentication source

[View Cluster Configuration â†’](https://docs.rundeck.com/administration/cluster/)

------------------------------------------------------------------------

## Configuration by Use Case

### Production Deployment Essentials

These are critical for any production environment:

- **[Database](https://docs.rundeck.com/administration/configuration/database/)** - MySQL, PostgreSQL, MS SQL Server, or Oracle
- **[Storage Facility](https://docs.rundeck.com/docs/administration/configuration/storage-facility.html)** - For keys, plugins, and uploaded files
- **[Email Settings](https://docs.rundeck.com/docs/administration/configuration/email-settings.html)** - SMTP for notifications
- **[System Properties](https://docs.rundeck.com/docs/administration/configuration/system-properties.html)** - JVM tuning and performance

### Enterprise/Cluster Features

Available in Rundeck Enterprise and Process Automation:

- **[Remote Job Execution](https://docs.rundeck.com/docs/administration/configuration/remote-job-execution.html)** - Distribute jobs across cluster members
- **[HashiCorp Consul](https://docs.rundeck.com/docs/administration/configuration/hashicorp-consul.html)** - Service discovery and configuration management
- **[Encryptable Properties](https://docs.rundeck.com/docs/administration/configuration/encryptable-properties.html)** - Encrypt sensitive configuration values

### Customization & Branding

Personalize the Rundeck interface:

- **[GUI Customization](https://docs.rundeck.com/docs/administration/configuration/gui-customization.html)** - Logos, colors, themes, custom branding
- **[Localization](https://docs.rundeck.com/docs/administration/configuration/localization.html)** - Language and regional format settings

### Plugin Management

Extend Rundeck functionality:

- **[Plugins Configuration](https://docs.rundeck.com/administration/configuration/plugins/)** - Install and configure plugins
- **[Repository](https://docs.rundeck.com/docs/administration/configuration/repository.html)** - Artifact repository for plugin distribution

------------------------------------------------------------------------

## Common Configuration Scenarios

### Scenario: First Production Deployment

**You're deploying Rundeck for the first time in production.**

**Required configurations:**

1.  [Database](https://docs.rundeck.com/administration/configuration/database/) - Set up PostgreSQL or MySQL
2.  [Base URL configuration](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#grails-serverurl) - Set `grails.serverURL`
3.  [Authentication](https://docs.rundeck.com/docs/administration/security/authentication.html) - Configure LDAP, Active Directory, or SSO
4.  [Email Settings](https://docs.rundeck.com/docs/administration/configuration/email-settings.html) - Enable notifications

**Recommended configurations:** 5. [Storage Facility](https://docs.rundeck.com/docs/administration/configuration/storage-facility.html) - Configure key storage backend 6. [System Properties](https://docs.rundeck.com/docs/administration/configuration/system-properties.html) - Tune JVM settings for your workload 7. [GUI Customization](https://docs.rundeck.com/docs/administration/configuration/gui-customization.html) - Add company branding

### Scenario: Docker Deployment

**You're deploying Rundeck using Docker containers.**

**Key differences:**

- Configuration via environment variables instead of editing files
- Volume mounts for persistent data (`/home/rundeck/server/data`)
- Custom plugins require extending the Docker image or volume mounts

**Start here:** [Docker Configuration Guide â†’](https://docs.rundeck.com/administration/configuration/docker)

**Also configure:**

- [Database](https://docs.rundeck.com/administration/configuration/database/) - External database (don't use embedded H2)
- [Storage Facility](https://docs.rundeck.com/docs/administration/configuration/storage-facility.html) - External storage (S3, database, etc.)

### Scenario: High-Availability Cluster (Enterprise)

**You need multiple Rundeck instances for high availability.**

**Required configurations:**

1.  [Cluster Overview](https://docs.rundeck.com/administration/cluster/) - Understand cluster architecture
2.  [Database](https://docs.rundeck.com/administration/configuration/database/) - Shared external database
3.  [Log Storage](https://docs.rundeck.com/administration/cluster/logstore/) - Shared log storage (S3, Azure, NFS)
4.  [Load Balancer](https://docs.rundeck.com/administration/cluster/loadbalancer/) - Configure sticky sessions
5.  [Autotakeover](https://docs.rundeck.com/administration/cluster/autotakeover/) - Automatic failover for scheduled jobs

**Optional configurations:** 6. [Remote Job Execution](https://docs.rundeck.com/docs/administration/configuration/remote-job-execution.html) - Distribute job execution 7. [HashiCorp Consul](https://docs.rundeck.com/docs/administration/configuration/hashicorp-consul.html) - Configuration management

### Scenario: Migration or Upgrade

**You're migrating Rundeck or upgrading to Enterprise.**

**Important configurations to preserve:**

- Export existing jobs, projects, and keys before migration
- Note current database type and version
- Document authentication configuration
- Back up `rundeck-config.properties` and `framework.properties`

**After migration/upgrade:**

- [Database](https://docs.rundeck.com/administration/configuration/database/) - Verify connection strings
- [Storage Facility](https://docs.rundeck.com/docs/administration/configuration/storage-facility.html) - Migrate key storage if needed
- Test authentication and authorization
- For Enterprise: Explore [System Configuration UI](https://docs.rundeck.com/docs/manual/configuration-mgmt/configmgmt.html)

### Scenario: Security Hardening

**You need to secure Rundeck for compliance or security requirements.**

**Critical configurations:**

1.  [Authentication](https://docs.rundeck.com/docs/administration/security/authentication.html) - Enterprise SSO or MFA
2.  [SSL/HTTPS Configuration](https://docs.rundeck.com/docs/administration/security/ssl.html) - Enable HTTPS
3.  [Access Control](https://docs.rundeck.com/docs/administration/security/authorization.html) - Configure ACL policies
4.  [Encryptable Properties](https://docs.rundeck.com/docs/administration/configuration/encryptable-properties.html) (Enterprise) - Encrypt sensitive values
5.  [Audit Stream Plugin](https://docs.rundeck.com/docs/administration/security/audit-stream-plugin.html) (Enterprise) - Send audit logs to SIEM

**Also review:**

- [Key Storage](https://docs.rundeck.com/manual/key-storage/) - Secure credential management
- [System Properties](https://docs.rundeck.com/docs/administration/configuration/system-properties.html) - Disable unnecessary features

------------------------------------------------------------------------

## Complete Configuration Reference

### Core Configuration

| Topic                                                                                                                 | Description                                                  | Edition |
|-----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|---------|
| [Configuration File Reference](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html) | Complete reference for all properties in configuration files | All     |
| [Database](https://docs.rundeck.com/administration/configuration/database/)                                           | External database setup (MySQL, PostgreSQL, MS SQL, Oracle)  | All     |
| [Storage Facility](https://docs.rundeck.com/docs/administration/configuration/storage-facility.html)                  | Configure storage for keys, plugins, and uploaded files      | All     |
| [System Properties](https://docs.rundeck.com/docs/administration/configuration/system-properties.html)                | JVM settings and advanced configuration                      | All     |
| [Email Settings](https://docs.rundeck.com/docs/administration/configuration/email-settings.html)                      | SMTP configuration for notifications                         | All     |

### Deployment-Specific

| Topic                                                                                           | Description                                                  | Edition    |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------|------------|
| [Docker Configuration](https://docs.rundeck.com/administration/configuration/docker)            | Environment variables, volumes, and Docker-specific settings | All        |
| [System Configuration](https://docs.rundeck.com/docs/manual/configuration-mgmt/configmgmt.html) | GUI-based configuration interface                            | Enterprise |
| [Cluster Configuration](https://docs.rundeck.com/administration/cluster/)                       | High-availability cluster setup                              | Enterprise |

### Enterprise Features

| Topic                                                                                                            | Description                                    | Edition    |
|------------------------------------------------------------------------------------------------------------------|------------------------------------------------|------------|
| [Remote Job Execution](https://docs.rundeck.com/docs/administration/configuration/remote-job-execution.html)     | Distribute jobs across cluster members         | Enterprise |
| [HashiCorp Consul](https://docs.rundeck.com/docs/administration/configuration/hashicorp-consul.html)             | Service discovery and configuration management | Enterprise |
| [Encryptable Properties](https://docs.rundeck.com/docs/administration/configuration/encryptable-properties.html) | Encrypt sensitive configuration values         | Enterprise |

### Customization

| Topic                                                                                                  | Description                                 | Edition |
|--------------------------------------------------------------------------------------------------------|---------------------------------------------|---------|
| [GUI Customization](https://docs.rundeck.com/docs/administration/configuration/gui-customization.html) | Logos, colors, themes, branding             | All     |
| [Localization](https://docs.rundeck.com/docs/administration/configuration/localization.html)           | Language and regional settings              | All     |
| [Plugins](https://docs.rundeck.com/administration/configuration/plugins/)                              | Install and configure plugins               | All     |
| [Repository](https://docs.rundeck.com/docs/administration/configuration/repository.html)               | Plugin distribution and artifact management | All     |

------------------------------------------------------------------------

## Quick Tips

**Finding Configuration Files:**

- **Linux/Unix:** `/etc/rundeck/` (RPM/DEB packages) or `$RDECK_BASE/etc/`
- **Docker:** Mount volumes or use environment variables
- **Windows:** `%RDECK_BASE%\etc\`

**Applying Configuration Changes:**

- Most changes require restarting Rundeck
- Some plugin configurations can be changed via System Configuration UI (Enterprise) without restart
- Docker: Restart container after changing environment variables

**Configuration Priority (from highest to lowest):**

1.  Environment variables (Docker)
2.  `rundeck-config.properties`
3.  System properties
4.  Default values

**Getting Help:**

- Check [Troubleshooting Guide](https://docs.rundeck.com/docs/learning/howto/troubleshooting.html)
- Review [Rundeck Logs](https://docs.rundeck.com/docs/administration/maintenance/logs.html)
- Search [Rundeck Discussions](https://github.com/rundeck/rundeck/discussions)
- Contact [PagerDuty Rundeck Support](https://support.pagerduty.com)

------------------------------------------------------------------------

## What's Next?

After completing initial configuration:

1.  **[Create Your First Project](https://docs.rundeck.com/manual/projects/)** - Set up projects to organize jobs
2.  **[Configure Node Sources](https://docs.rundeck.com/manual/projects/resource-model-sources/)** - Add servers/nodes to manage
3.  **[Create Jobs](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html)** - Define automation workflows
4.  **[Set Up Access Control](https://docs.rundeck.com/docs/administration/security/authorization.html)** - Configure user permissions
5.  **[Configure Integrations](https://docs.rundeck.com/learning/solutions/)** - Connect to external systems
