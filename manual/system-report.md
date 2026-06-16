---
title: "System Report (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/system-report.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# System Report (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

The Enterprise System Report provides a breakdown of the Rundeck server's system statistics and information.

## General

The **General** tab provides a quick snapshot view of the Rundeck server instance.  
Information about CPU, Uptime, Memory and important version information can all be seen at a glance.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/system-report-general.png" alt="System Report - General Tab" />
<figcaption aria-hidden="true">System Report - General Tab</figcaption>
</figure>

## Diagnostics

The **Diagnostics** tab offers an in-depth view of the configurations of Rundeck.  
The configurations are loaded from Memory rather than directly from the files in order to provide the configuration that the Rundeck server is actively using.

To protect sensitive data configuration entries are classified in two ways:

- **Secure Data** for passwords, secrets, etc. are never be revealed on the System Report page
- **Concealed Data** is hidden by default but can be revealed in the Rundeck GUI only by clicking Show Data on that particular data entry.  
  This would be for IP addresses, user names, etc. This information may be necessary for troubleshooting.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/system-report-showdata.gif" alt="System Report - Diagnostic Tab" />
<figcaption aria-hidden="true">System Report - Diagnostic Tab</figcaption>
</figure>

### Export Report

To streamline support requests we have added the ability to export data from the System Report. Our Enterprise Support team can use these exports to look for common misconfigurations that cause issues. When on the Diagnostic tab click the **Export Report** button. It is possible to export specific sections as needed in either JSON format or plain text format.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/system-report-exportreport.png" alt="System Report - Export Report Window" />
<figcaption aria-hidden="true">System Report - Export Report Window</figcaption>
</figure>

Items in the configuration marked as Secure or Concealed data (described above) will not be included in the export files.

> **Sensitive Data**
>
> Prior to sharing the exports with anyone, including Rundeck Support, please ensure that all sensitive data has been obscured in the export files.
