---
title: "Rundeck CLI - Java API Library"
source_url: https://docs.rundeck.com/docs/rd-cli/javalib.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Rundeck CLI - Java API Library

The Java library used by RD can be used as a dependency in your Java project to call Rundeck APIs.

## Javadoc

[rd-api-client ![javadoc](https://javadoc.io/badge2/org.rundeck.api/rd-api-client/javadoc.svg)](https://javadoc.io/doc/org.rundeck.api/rd-api-client)

## Gradle usage

A demo project can be seen here: <https://github.com/gschueler/rd-api-demo>

<div class="language-text line-numbers-mode">

``` text
//use maven central
repositories {
    mavenCentral()
}

dependencies {
    compile "org.rundeck.api:rd-api-client:2.1.1
"
}
```

</div>
