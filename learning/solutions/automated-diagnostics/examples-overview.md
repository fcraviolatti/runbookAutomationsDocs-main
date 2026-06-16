---
title: "Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples-overview.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

------------------------------------------------------------------------

## Examples & Best Practices

The following sections outline common diagnostics for different types of infrastructure and applications.  
Details are also provided on the various mechanisms that can be used to integrate with the various environments.  
For example, with many technologies, there are options to integrate using plugins, command-line interfaces (CLIs), or API calls.

In addition, many sections include example Jobs that can be imported into your Automation Instance - helping you get started quickly with Automated Diagnostics.  
Other prebuilt Jobs are included in the Automated Diagnostics Solution package, which is preinstalled for Runbook Automation customers and can be downloaded for Runbook Automation customers from the [getting started](https://docs.rundeck.com/learning/solutions/automated-diagnostics/getting-started) section.

<table>
<tbody>
<tr class="odd">
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html"><img src="https://docs.rundeck.com/docs/assets/img/ecs.png" /><br />
<br />
Stopped ECS Task Errors</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html"><img src="https://docs.rundeck.com/docs/assets/img/elb.svg" /><br />
<br />
ELB Targets Health</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html"><img src="https://docs.rundeck.com/docs/assets/img/cloudwatch-logo.png" /><br />
<br />
CloudWatch Logs</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#azure"><img src="https://docs.rundeck.com/docs/assets/img/azure-function.png" /><br />
<br />
Azure Function App Health</a></td>
</tr>
<tr class="even">
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#azure"><img src="https://docs.rundeck.com/docs/assets/img/azure-logo.png" /><br />
<br />
Azure File Sync</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#azure"><img src="https://docs.rundeck.com/docs/assets/img/azure-load-balancer.png" /><br />
<br />
Load Balancer Health Probes</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#google-cloud-platform-gcp"><img src="https://docs.rundeck.com/docs/assets/img/gcp-load-balancer.png" /><br />
<br />
Load Balancer Health Checks</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#google-cloud-platform-gcp"><img src="https://docs.rundeck.com/docs/assets/img/gcp-firewall.png" /><br />
<br />
Troubleshoot Firewall Rules</a></td>
</tr>
<tr class="odd">
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/public-cloud-providers.html#google-cloud-platform-gcp"><img src="https://docs.rundeck.com/docs/assets/img/gke-logo.png" /><br />
<br />
GKE Cluster Connectivity</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/linux.html"><img src="https://docs.rundeck.com/docs/assets/img/linux-logo.png" /><br />
<br />
Top CPU Consuming Processes</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/linux.html"><img src="https://docs.rundeck.com/docs/assets/img/linux-logo.png" /><br />
<br />
Retrieve Errors from Syslog</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/linux.html"><img src="https://docs.rundeck.com/docs/assets/img/linux-logo.png" /><br />
<br />
List Top Disk Consuming Files</a></td>
</tr>
<tr class="even">
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/windows.html"><img src="https://docs.rundeck.com/docs/assets/img/active-directory-logo.svg" /><br />
<br />
Active Directory Replication Statistics</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/windows.html"><img src="https://docs.rundeck.com/docs/assets/img/windows-logo.png" /><br />
<br />
Retrieve IIS Web Server Logs</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/windows.html"><img src="https://docs.rundeck.com/docs/assets/img/windows-logo.png" /><br />
<br />
SMB Connection Failures</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/apis.html"><img src="https://docs.rundeck.com/docs/assets/img/webhook-logo.jpeg" /><br />
<br />
API Health Check</a></td>
</tr>
<tr class="odd">
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html"><img src="https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png" /><br />
<br />
Recent Pod Logs</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html"><img src="https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png" /><br />
<br />
Recent Kubernetes Events</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html"><img src="https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png" /><br />
<br />
Pod Status &amp; Errors</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/kubernetes.html"><img src="https://docs.rundeck.com/docs/assets/img/kubernetes-logo.png" /><br />
<br />
Retrieve Deployment Diagnostics</a></td>
</tr>
<tr class="even">
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/databases.html"><img src="https://docs.rundeck.com/docs/assets/img/mysql-logo.png" /><br />
<br />
Top Resource Consuming Queries</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/databases.html"><img src="https://docs.rundeck.com/docs/assets/img/mysql-logo.png" /><br />
<br />
Blocking Locks</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/databases.html"><img src="https://docs.rundeck.com/docs/assets/img/mysql-logo.png" /><br />
<br />
Missing Indexes</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/network-devices.html"><img src="https://docs.rundeck.com/docs/assets/img/network-switch.png" /><br />
<br />
BGP Route Flapping</a></td>
</tr>
<tr class="odd">
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/network-devices.html"><img src="https://docs.rundeck.com/docs/assets/img/network-switch.png" /><br />
<br />
Check Spanning Tree</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/network-devices.html"><img src="https://docs.rundeck.com/docs/assets/img/network-switch.png" /><br />
<br />
Check Duplex Mismatch</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/observability-integrations.html"><img src="https://docs.rundeck.com/docs/assets/img/cloudwatch-logo.png" /><br />
<br />
Retrieve Application Logs</a></td>
<td><a href="https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/observability-integrations.html"><img src="https://docs.rundeck.com/docs/assets/img/cloudwatch-logo.png" /><br />
<br />
Retrieve Saved Queries</a></td>
</tr>
<tr class="even">
<td><img src="https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg" /><br />
<br />
Intrinsic Latency Diagnostics Test</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg" /><br />
<br />
Check Redis Port Listening</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg" /><br />
<br />
Retrieve Redis Memory Statistics</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/redis-logo.jpeg" /><br />
<br />
Slow Log Entries</td>
</tr>
<tr class="odd">
<td><img src="https://docs.rundeck.com/docs/assets/img/rds-logo.png" /><br />
<br />
Check Database Storage Status</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/nginx-logo.png" /><br />
<br />
Query Nginx Status Endpoint</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/nginx-logo.png" /><br />
<br />
Retrieve Error Logs</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/nginx-logo.png" /><br />
<br />
Test Nginx Configuration</td>
</tr>
<tr class="even">
<td><img src="https://docs.rundeck.com/docs/assets/img/postgres-logo.png" /><br />
<br />
Retrieve Recent PostgreSQL Logs</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/postgres-logo.png" /><br />
<br />
Test for PostgreSQL Server Running</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/cassandra-logo.png" /><br />
<br />
Check Compaction Statistics</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/kafka-logo.png" /><br />
<br />
Describe Kafka Topic</td>
</tr>
<tr class="odd">
<td><img src="https://docs.rundeck.com/docs/assets/img/kafka-logo.png" /><br />
<br />
View Topic Messages</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/java-logo.png" /><br />
<br />
Retrieve Java Thread Dump</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/java-logo.png" /><br />
<br />
Retrieve Java Heap Dump</td>
<td><img src="https://docs.rundeck.com/docs/assets/img/rabbitmq-logo.png" /><br />
<br />
RabbitMQ Node Health</td>
</tr>
</tbody>
</table>
