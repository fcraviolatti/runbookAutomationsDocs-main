---
title: "Load Balancer - Cluster Health Checks"
source_url: https://docs.rundeck.com/docs/administration/cluster/loadbalancer/health-check.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Load Balancer - Cluster Health Checks

### Cluster Health Checks(3.3.4+)

The web load balancer serving traffic to the Rundeck instance should be configured with a health check.

The path for unauthenticated health checks is `/health`.

<div class="language-text line-numbers-mode">

``` text
$host:$port/health
localhost:4440/health
node1.mydomain.com:4440/health
node2.mydomain.com:4440/health
172.31.5.111:4440/health
```

</div>

This endpoint is enabled by default but can be disabled, see [Configuration](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#load-balancer-health-endpoint).

### Authenticated Cluster Health Checks

It is recommend to use unauthenticated health checks to reduce security exposure from load-balancer configurations. If you wish to use authenticated checks please ensure you are using the least privilege principle.

Please reference the documentation for more information about [API Token Authorization Roles](https://docs.rundeck.com/docs/administration/security/authorization.html#api-token-authorization-roles).

<div class="language-text line-numbers-mode">

``` text
$host:$port/api/32/system/executions/status?authtoken=<TOKEN_VALUE>

$host:$port//api/32/system/executions/status?authtoken=<TOKEN_VALUE>
localhost:4440//api/32/system/executions/status?authtoken=<TOKEN_VALUE>
node1.mydomain.com:4440//api/32/system/executions/status?authtoken=<TOKEN_VALUE>
node2.mydomain.com:4440//api/32/system/executions/status?authtoken=<TOKEN_VALUE>
172.31.5.111:4440//api/32/system/executions/status?authtoken=<TOKEN_VALUE>
```

</div>
