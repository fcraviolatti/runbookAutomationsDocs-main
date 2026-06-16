---
title: "Using HAProxy as a loadbalancer"
source_url: https://docs.rundeck.com/docs/administration/cluster/loadbalancer/haproxy.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Using HAProxy as a loadbalancer

To avoid sending traffic to unavailable nodes, HAProxy can check the health of their downstream services via http or tcp. This document explains how to create a custom health check for Rundeck.

### On HAProxy, add the following settings

The web load balancer serving traffic to the Rundeck instance should be configured with the health check.

- Add the "httpchk" with the URI of the [execution status API endpoint](https://docs.rundeck.com/docs/api/#get-current-execution-mode). The token value that you want to use is needed.
- Add the "http-check" with the expected status (in this case 200)

<div class="language-text line-numbers-mode">

``` text
backend default_service
cookie JSESSIONID prefix nocache
option httpchk get /api/32/system/executions/status?authtoken=<TOKEN_VALUE>
http-check expect status 200
server rundeck1 192.168.0.1:4440 cookie rundeck1 check inter 2000 rise 2 fall 3
server rundeck2 192.168.0.2:4440 cookie rundeck2 check inter 2000 rise 2 fall 3
server rundeck3 192.168.0.3:4440 cookie rundeck3 check inter 2000 rise 2 fall 3
```

</div>

### Check if HAProxy redirect to the active instance

Once the web load balancer has been configured with the health check, any instance that is not in "active" mode will not be passed traffic.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/haproxy-status.png" alt="HAProxy status" />
<figcaption aria-hidden="true">HAProxy status</figcaption>
</figure>
