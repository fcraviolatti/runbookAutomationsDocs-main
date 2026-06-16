---
title: "Intro to Setting up a New Server"
source_url: https://docs.rundeck.com/docs/learning/getting-started/server-setup-overview.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Intro to Setting up a New Server

Installing a Rundeck server involves a series of crucial steps that must be executed with precision and attention to detail. When done correctly, it can provide organizations with a powerful platform to automate routine tasks, improve operational efficiency, and enhance collaboration between teams.  
The following steps show you how to prepare the Server properly. These steps are also valid for PagerDuty Runbook Automation.  

### Step 1: [Prepare the Server](https://docs.rundeck.com/docs/administration/install/system-requirements.html)

Ensure that your server meets the minimum system requirements for Rundeck and keep all the server packages updated.  

### Step 2: [Install Java](https://docs.rundeck.com/docs/administration/install/system-requirements.html#java)

Rundeck requires Java JRE to run. Install the Java Runtime Environment (JRE).  
For example, on Ubuntu, you can use `sudo apt install openjdk-11-jre`  

### Step 3: [Install Rundeck](https://docs.rundeck.com/docs/administration/install/)

Add the Rundeck repository to your package manager and install the latest Rundeck version depending on your operating system. For Windows-based servers, follow [this](https://docs.rundeck.com/docs/administration/install/windows.html#installing-on-windows).  

### Step 4: [Set the right server URL for Rundeck server](https://docs.rundeck.com/docs/administration/install/#server-url)

Out of the box the Rundeck configurations set the `grails.ServerURL` (`rundeck-config.properties` file) value to `localhost`. To get access from another host, the `grails.ServerURL` must be defined using the server IP address or domain name.  

### Step 5: [Configure Rundeck against a database](https://docs.rundeck.com/docs/administration/install/#database-configuration)

By default, Rundeck includes a testing database ([H2](https://docs.rundeck.com/administration/configuration/database/#default-database-h2)). However, this backend isn't recommended for production environments. Configure Rundeck to use an external database as the backend as a best practice.  

### Step 6: [Start the Rundeck Server](https://docs.rundeck.com/docs/administration/maintenance/startup.html#startup-and-shutdown)

To start the Rundeck service, for systemd based systems (like the most popular Linux distributions) you can use the [service tool](https://docs.rundeck.com/docs/administration/maintenance/startup.html#rpm-and-deb). On a war launcher based installation, you can use the [rundeckd script](https://docs.rundeck.com/docs/administration/maintenance/startup.html#launcher). For Windows servers, set the process up as a [service](https://docs.rundeck.com/docs/administration/install/windows.html#run-rundeck-as-a-service).  

### Step 7: Accessing Rundeck

To access Rundeck, open your favorite web browser and go to `http://ip_or_domainname:4440`. The default admin user name is `admin` (password: `admin`).  

## Resources

[Introduction to Rundeck](https://docs.rundeck.com/docs/about/introduction.html)  
[Startup and Shutdown Rundeck](https://docs.rundeck.com/docs/about/introduction.html)  
[Welcome Project tutorial](https://docs.rundeck.com/docs/learning/tutorial/)
