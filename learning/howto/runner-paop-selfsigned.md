---
title: "Runner connection to a Runbook Automation Self-Hosted using self signed certificate"
source_url: https://docs.rundeck.com/docs/learning/howto/runner-paop-selfsigned.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Runner connection to a Runbook Automation Self-Hosted using self signed certificate

We recommend the usage of real certificates, but we also know that there are situations when you need to test using self signed certificates. If Runbook Automation Self-Hosted is configured to use a self signed certificate, here is how to launch the Runner for a successful connectivity.

> **Note**
>
> Below steps work also when Runbook Automation is behind a Load Balancer using self signed certificate.

There are several ways to set the Runbook Automation's certificate where the Runner will be launched.

## Cacerts file

Add the `process_automation.crt` certificate to the OS's cacerts file.

<div class="language-bash line-numbers-mode">

``` bash
sudo keytool -import -alias MYALIAS -file process_automation.crt -cacerts -storepass changeit
```

</div>

To verify it is imported:

<div class="language-bash line-numbers-mode">

``` bash
sudo keytool -list -cacerts -storepass changeit | grep MYALIAS
```

</div>

## Other truststore

> **Tip**
>
> Keep in mind the `file:` part in the path field.

### Directly from command line

<div class="language-bash line-numbers-mode">

``` bash
java -Dmicronaut.ssl.trust-store.path=file:/path/to/truststore -Dmicronaut.ssl.trust-store.password=PASSWORD -jar runner.jar
```

</div>

### Using environment variables

<div class="language-bash line-numbers-mode">

``` bash
export MICRONAUT_HTTP_CLIENT_SSL_TRUST_STORE_PATH=file:/path/to/truststore
export MICRONAUT_HTTP_CLIENT_SSL_TRUST_STORE_PASSWORD=PASSWORD
java -jar runner.jar
```

</div>

### From a config file

Config file:

<div class="language-bash line-numbers-mode">

``` bash
cat application.yaml
micronaut:
  http:
    client:
      ssl:
        enabled: true
        trust-store:
          path: file:/path/to/truststore
          password: PASSWORD
```

</div>

<div class="language-bash line-numbers-mode">

``` bash
java -Dmicronaut.config.files=/path/to/application.yaml -jar runner.jar
```

</div>

### Docker env vars

<div class="language-text line-numbers-mode">

``` text
MICRONAUT_HTTP_CLIENT_SSL_TRUST_STORE_PATH=file:/path/to/truststore
MICRONAUT_HTTP_CLIENT_SSL_TRUST_STORE_PASSWORD=PASSWORD
```

</div>

Truststore file must be in the proper path in the image.

## Resources

[Enterprise Runner](https://docs.rundeck.com/docs/administration/runner/pre-4-11-runners.html#runner)  
[Micronaut](https://micronaut-projects.github.io/micronaut-docs-mn2/2.0.3/guide/configurationreference.html#io.micronaut.http.ssl.ClientSslConfiguration$DefaultTrustStoreConfiguration)
