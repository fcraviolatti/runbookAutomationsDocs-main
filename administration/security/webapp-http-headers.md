---
title: "Webapp HTTP Headers"
source_url: https://docs.rundeck.com/docs/administration/security/webapp-http-headers.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Webapp HTTP Headers

Rundeck adds these HTTP headers to responses by default:

<div class="language-text line-numbers-mode">

``` text
X-Frame-Options: deny
X-XSS-Prevention: 1
X-Content-Type-Options: nosniff
Content-Security-Policy: ...
```

</div>

You can configure these, or add additional custom headers with the configuration settings described in [Rundeck Configuration - Configuration File Reference - Security Http Headers](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#security-http-headers).
