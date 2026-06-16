---
title: "Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/examples/apis.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

## SaaS & Internal Application APIs

A very common type of diagnostic job is to query an API as a way of measuring application or system health.  
This could be a common SaaS API or might be querying the API of an internal application.

In either case, this is accomplished by using the [HTTP Request workflow step](https://resources.rundeck.com/plugins/rundeck-http-workflow-step-plugin/), which can send an http request and trigger further steps based on the response code.  
Whatever data is returned by the http step can be used in later steps in a workflow through the use of [custom variables](https://docs.rundeck.com/docs/learning/howto/passing-variables.html).

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/http-step.png" alt="HTTP Request plugin can query external or internal APIs" />
<figcaption aria-hidden="true">HTTP Request plugin can query external or internal APIs</figcaption>
</figure>

This plugin is very customizable to accommodate whatever is needed, including various authentication methods and support for proxy settings.

In addition to the **HTTP Request Plugin**, APIs can be queried using commands such as **`curl`** using the **Command Step**: ![Command Step to curl an endpoint](https://docs.rundeck.com/docs/assets/img/curl-example.png)
