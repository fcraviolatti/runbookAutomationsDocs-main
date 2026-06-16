---
title: "System Menu"
source_url: https://docs.rundeck.com/docs/manual/system-configs.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# System Menu

The Rundeck GUI has a menu which lets you view and manage system wide configuration settings.

Users with `admin` role access will see the "System Menu" icon in the header:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0701.png" alt="System Menu Icon" />
<figcaption aria-hidden="true">System Menu Icon</figcaption>
</figure>

This page contains links to manage Project configuration as well as system level configuration information.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0702.png" alt="System Menu" />
<figcaption aria-hidden="true">System Menu</figcaption>
</figure>

> **Tips**
>
> Some settings and screenshots show Enterprise version features and may not be available in the open source version.

## Key Storage

The Key Storage facility provides a GUI and [API](https://docs.rundeck.com/docs/api/#key-storage) to manage public keys, private keys, and passwords. These stored keys are used by plugins, node executors, and can be referenced in Job definitions as secure value inputs.

Key Storage features include:

- Secure storage of SSH keys, passwords, and other credentials
- Integration with external secret managers (HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, etc.)
- Project-scoped access control
- File or text-based key upload
- Storage backend options (database or filesystem)

For complete documentation including UI instructions, storage plugins, ACL configuration, and API details, see [Key Storage](https://docs.rundeck.com/docs/manual/key-storage/).

## System Configuration (Enterprise Only)

This section will allow configuration of Rundeck configuration settings from within the GUI. [Check out the full feature documentation here](https://docs.rundeck.com/docs/manual/configuration-mgmt/configmgmt.html).

Open Source Rundeck will display key configuration settings as shown in the screen shot below.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0715.png" alt="System settings" />
<figcaption aria-hidden="true">System settings</figcaption>
</figure>

## Access Control

System security is managed through configuration files. This page describes the current settings the files to change them.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0716.png" alt="Security settings" />
<figcaption aria-hidden="true">Security settings</figcaption>
</figure>

## System Report

The System Report page provides a breakdown of some of the Rundeck server's system statistics and information.  
There is an Enterprise version of this page that includes the ability to view and export important configuration information for sharing with our support team. More details are on the [Enterprise System Report](https://docs.rundeck.com/docs/manual/system-report.html) page.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0703.png" alt="System Report Page" />
<figcaption aria-hidden="true">System Report Page</figcaption>
</figure>

This information is also available via the API: [API \> System Info](https://docs.rundeck.com/docs/api/#system-info)

## Log Storage

See [Logstore](https://docs.rundeck.com/docs/administration/cluster/logstore/)

## Plugins

Rundeck is built on a pluggable core. Plugins can add functionality to connect to 3rd party systems, update the Rundeck UI, etc. Use these menus to find, install, and manage the plugins on your Rundeck instance.

### Find Plugins

Search plugins from the online Rundeck plugin repository.

### Installed Plugins

See what plugins are currently installed.

### Upload Plugin

Use the [Developer Docs](https://docs.rundeck.com/api/rundeck-api) to write your own plugin! Upload it here to use it on your instance.

## Password Utility

## Users

Use this section to see a summary of User accounts and, with Enterprise, manage local user accounts with a GUI based editor.

[More details about the Users section can be found here](https://docs.rundeck.com/docs/manual/user-management/user-mgmt.html).

## Licenses

This page lists the Rundeck and third party library licenses.
