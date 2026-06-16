---
title: "Learn more about Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

### Overview

Automated diagnostics is a solution provided by integrating PagerDuty's Incident Response and Runbook Automation products. By automating the retrieval of â€œdiagnosticâ€? data during incidents, you can shorten the length of incidents, reduce the number of individuals paged to help with resolution, and gather evidence for fixing the root-cause after the incident.

### Use Cases

There are multiple use-cases and benefits to the Automated Diagnostics solution. Here are a few of the most common examples:

- **Improve Triage**: surfacing diagnostic data can improve the time spent troubleshooting and the number of people pulled into incidents.
- **Capture Environment State**: by capturing the *environment* or *application* "state" during an incident, operations engineers and developers have *evidence* to help them fix code-level bugs and configuration errors - perhaps a while after the incident has been resolved.
- **Realtime Updates**: by querying backend services in realtime, an Incident Commander can more easily provide updates to stakeholders during an incident.

For more details on these use-cases, see [**this section**](https://docs.rundeck.com/learning/solutions/automated-diagnostics/automation-beyond-triage) of the solution-guide.

### Prebuilt Automation

PagerDuty provides a solution that helps users start automating diagnostics quickly. This Solution consists of **prebuilt Automation Jobs** that retrieve data from common infrastructure and services for investigating, debugging and diagnosing incidents:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/diag-on-pd-timeline.png" alt="Automated Diagnostics within PagerDuty" />
<figcaption aria-hidden="true">Automated Diagnostics within PagerDuty</figcaption>
</figure>

  
![Verbose Diagnostics in Runbook Automation](https://docs.rundeck.com/docs/assets/img/diag-verbose-output.png)

As an example, if an incident is triggered for a service running in Kubernetes, PagerDuty Runbook Automation can retrieve information from logs, APIâ€™s, databases and other sources that support this service. This could be triggered with the click of a button or through event-driven invocation.

### Simplifying and Sharing Diagnostics

Diagnostics retrieved using **Runbook Automation** can be made available in multiple interfaces such as PagerDuty's Mobil App, Slack, and Microsoft Teams:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/diag_in_slack.png" alt="Diagnostics in Slack" />
<figcaption aria-hidden="true">Diagnostics in Slack</figcaption>
</figure>

## Examples & Templates

This guide includes a full section on Examples & Best Practices - a preview of that is shown here:

| Examples                                                                                                                                                                                                                                |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](https://docs.rundeck.com/docs/assets/img/ecs.png) [Stopped ECS Task Error](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html)                                             |
| ![](https://docs.rundeck.com/docs/assets/img/elb.svg)[ELB Targets Health](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html)                                                  |
| ![](https://docs.rundeck.com/docs/assets/img/cloudwatch-logo.png)[CloudWatch Logs](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html)                                         |
| ![](https://docs.rundeck.com/docs/assets/img/azure-function.png)[Azure Function App Health](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#azure)                          |
| ![](https://docs.rundeck.com/docs/assets/img/azure-logo.png)[Azure File Sync](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#azure)                                        |
| ![](https://docs.rundeck.com/docs/assets/img/azure-load-balancer.png)[Load Balancer Health Probes](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#azure)                   |
| ![](https://docs.rundeck.com/docs/assets/img/gcp-load-balancer.png)[Load Balancer Health Checks](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#google-cloud-platform-gcp) |
| ![](https://docs.rundeck.com/docs/assets/img/gcp-firewall.png)[Troubleshoot Firewall Rules](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#google-cloud-platform-gcp)      |
| ![](https://docs.rundeck.com/docs/assets/img/gke-logo.png)[GKE Cluster Connectivity](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#google-cloud-platform-gcp)             |
| ![](https://docs.rundeck.com/docs/assets/img/linux-logo.png)[Top CPU Consuming Processes](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/linux.html)                                                   |
| ![](https://docs.rundeck.com/docs/assets/img/linux-logo.png)[Retrieve Errors from Syslog](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/linux.html)                                                   |
| ![](https://docs.rundeck.com/docs/assets/img/linux-logo.png)[List Top Disk Consuming Files](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/linux.html)                                                 |
| ![](https://docs.rundeck.com/docs/assets/img/active-directory-logo.svg)[Active Directory Replication Statistics](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/windows.html)                          |
| ![](https://docs.rundeck.com/docs/assets/img/windows-logo.png)[Retrieve IIS Web Server Logs](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/windows.html)                                              |
| ![](https://docs.rundeck.com/docs/assets/img/windows-logo.png)[SMB Connection Failures](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/windows.html)                                                   |
| ![](https://docs.rundeck.com/docs/assets/img/webhook-logo.jpeg)[API Health Check](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/apis.html)                                                            |
| ![](https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png)[Recent Pod Logs](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html)                                                     |
| ![](https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png)[Recent Kubernetes Events](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html)                                            |
| ![](https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png)[Pod Status & Errors](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html)                                                 |
| ![](https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png)[Retrieve Deployment Diagnostics](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html)                                     |
| ![](https://docs.rundeck.com/docs/assets/img/mysql-logo.png)[Top Resource Consuming Queries](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/databases.html)                                            |
| ![](https://docs.rundeck.com/docs/assets/img/mysql-logo.png)[Blocking Locks](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/databases.html)                                                            |
| ![](https://docs.rundeck.com/docs/assets/img/mysql-logo.png)[Missing Indexes](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/databases.html)                                                           |
| ![](https://docs.rundeck.com/docs/assets/img/network-switch.png)[BGP Route Flapping](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/network-devices.html)                                              |
| ![](https://docs.rundeck.com/docs/assets/img/network-switch.png)[Check Spanning Tree](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/network-devices.html)                                             |
| ![](https://docs.rundeck.com/docs/assets/img/network-switch.png)[Check Duplex Mismatch](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/network-devices.html)                                           |
| ![](https://docs.rundeck.com/docs/assets/img/cloudwatch-logo.png)[Retrieve Application Logs](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/observability-integrations.html)                           |
| ![](https://docs.rundeck.com/docs/assets/img/cloudwatch-logo.png)[Retrieve Saved Queries](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/observability-integrations.html)                              |
| ![](https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg)[Intrinsic Latency Diagnostics Test](#)                                                                                                                                    |
| ![](https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg)[Check Redis Port Listening](#)                                                                                                                                            |
| ![](https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg)[Retrieve Redis Memory Statistics](#)                                                                                                                                      |
| ![](https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg)[Slow Log Entries](#)                                                                                                                                                      |
| ![](https://docs.rundeck.com/docs/assets/img/rds-logo.png)[Check Database Storage Status](#)                                                                                                                                            |
| ![](https://docs.rundeck.com/docs/assets/img/nginx-logo.png)[Query Nginx Status Endpoint](#)                                                                                                                                            |
| ![](https://docs.rundeck.com/docs/assets/img/nginx-logo.png)[Retrieve Error Logs](#)                                                                                                                                                    |
| ![](https://docs.rundeck.com/docs/assets/img/nginx-logo.png)[Test Nginx Configuration](#)                                                                                                                                               |
| ![](https://docs.rundeck.com/docs/assets/img/postgres-logo.png)[Retrieve Recent PostgreSQL Logs](#)                                                                                                                                     |
| ![](https://docs.rundeck.com/docs/assets/img/postgres-logo.png)[Test for PostgreSQL Server Running](#)                                                                                                                                  |
| ![](https://docs.rundeck.com/docs/assets/img/cassandra-logo.png)[Check Compaction Statistics](#)                                                                                                                                        |
| ![](https://docs.rundeck.com/docs/assets/img/kafka-logo.png)[Describe Kafka Topic](#)                                                                                                                                                   |
| ![](https://docs.rundeck.com/docs/assets/img/kafka-logo.png)[View Topic Messages](#)                                                                                                                                                    |
| ![](https://docs.rundeck.com/docs/assets/img/java-logo.png)[Retrieve Java Thread Dump](#)                                                                                                                                               |
| ![](https://docs.rundeck.com/docs/assets/img/java-logo.png)[Retrieve Java Heap Dump](#)                                                                                                                                                 |
| ![](https://docs.rundeck.com/docs/assets/img/rabbitmq-logo.png)[RabbitMQ Node Health](#)                                                                                                                                                |
