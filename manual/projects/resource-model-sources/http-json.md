---
title: "HTTP-JSON Node Source"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/http-json.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# HTTP-JSON Node Source

> **Available in PagerDuty Runbook Automation Commercial products.**

The HTTP-JSON Node Source will gather Node definitions from an HTTP endpoint.

### Features

- Ability to specify authentication credentials to the endpoint.
- Ability to specify custom headers on the request to the endpoint.
- Ability to transform the JSON payload returned by the endpoint with a JQ expression.
- Ability to add supplemental tags to all the nodes returned by the endpoint.

### Requirements

- The configured endpoint must return a JSON payload.
- The JSON should conform to the [JSON](https://docs.rundeck.com/docs/manual/document-format-reference/resource-json-v10.html) Rundeck nodes format. There is an option to transform other sources using a JQ Transform

## Configuration

1.  Specify the **URL** endpoint to hit.
2.  (Optional) **Authorization Header** If your endpoint requires authentication, either manually type in the value or select a Key Storage path that will be used for the `Authorization` header. Note: If your token needs a 'Bearer' prefix, you must add it manually.\`
3.  (Optional) **Supplemental Headers** If your URL requires custom headers, add them here.

> Note: If you manually add a `Content-Type` header it will be overridden by the plugin because the plugin requires an `application/json` response.

1.  (Optional) **JQ Transform** If your JSON payload needs to be transformed, add a JQ expression here. The transformed JSON should conform to the [JSON](https://docs.rundeck.com/docs/manual/document-format-reference/resource-json-v10.html) Nodes format. If you don't supply a JQ expression, the plugin will assume the JSON payload retrieved from the URL conforms to the proper format.
2.  (Optional) **Supplemental Tags** If you want to add tags to all the nodes returned by the endpoint, add them here as a comma separated list.

## Tips

Use [JQ Playground](https://www.devtoolsdaily.com/jq_playground/) to explore ways to convert your existing JSON into the expected Node format.
