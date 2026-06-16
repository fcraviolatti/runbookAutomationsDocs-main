---
title: "Using AWS ALB as loadbalancer"
source_url: https://docs.rundeck.com/docs/administration/cluster/loadbalancer/aws-alb.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Using AWS ALB as loadbalancer

Application Load Balancer overview

Typically Application Load Balancer is used here (ALB), due to it can offload HTTPS labels. For example it can listen on Port 443 and forward the traffic to Port 80 in the backend.

An Application Load Balancer functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model. After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action.

You can add and remove targets from your load balancer as your needs change, without disrupting the overall flow of requests to your application.

You can configure health checks, which are used to monitor the health of the registered targets so that the load balancer can send requests only to the healthy targets.

For more information, see How Elastic Load Balancing works in the [Elastic Load Balancing User Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html).

### Creating an AWS ALB for you Runbook Automation Cluster

<figure>

</figure>

### Health Checks

The web load balancer serving traffic to the Rundeck instance should be configured with a health check.

The default path for unauthenticated health checks is /health.

<div class="language-text line-numbers-mode">

``` text
$host:$port/health
localhost:4440/health
node1.mydomain.com:4440/health
node2.mydomain.com:4440/health
172.31.5.111:4440/health
```

</div>

### Authenticated Health Checks

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

### IMPORTANT! STICKY SESSIONS MUST BE ENABLED.

Enable cookie stickiness via the AWS Console, EC2 -\> Target Groups -\> Your Target Group -\> Group Details -\> Attributes.

This can be enabled to be managed by AWS Load Balancer or by the Rundeck Application using its' JSESSIONID Cookie. The difference is that when the AWS LB option is chosen, you can't set the time for the Cookie duration, and while using the Application Cookie it will timeout according to the Application settings. In the case that you are using an Auto-Scaling group, application stickiness is not recommended.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/lb-aws-alb-stickiness1.png" alt="Target Group Attributes" />
<figcaption aria-hidden="true">Target Group Attributes</figcaption>
</figure>

Enable cookie stickiness via the AWS CLI.

<div class="language-text line-numbers-mode">

``` text
aws elbv2 modify-target-group-attributes \
--target-group-arn $AWS_ALB_TARGET_GROUP_ARN \
--attributes Key=stickiness.enabled,Value=true Key=stickiness.lb_cookie.duration_seconds,Value=86400
```

</div>
