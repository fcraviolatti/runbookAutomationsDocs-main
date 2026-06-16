---
title: "HTTP Request Workflow Step"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/http-request.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# HTTP Request Workflow Step

This plugin executes an HTTP/S request to a remote endpoint.

![HTTP Request Workflow](https://docs.rundeck.com/docs/assets/img/http-request-workflow-step.png)  

#### Configuration

- **Remote URL**: The remote endpoint for the HTTP request. This can be an HTTP or HTTPS endpoint. The URL must begin with `http://` or `https://`.

- **HTTP Method**: The method of the HTTP request. One of: `GET`, `POST`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`, `PATCH`.

- **Headers**: Additional headers to include in the request. The headers can be added in YAML or JSON format.

  - YAML example:

  - <div class="language-yaml line-numbers-mode">

    ``` yaml
    - name: "User-Agent"
      value: "Buddy"
    - name: "Content-Type"
      value: "application/json"
    ```

    </div>

  - JSON example:

  - <div class="language-json line-numbers-mode">

    ``` json
    {
       "User-Agent": "Buddy"
    },
    {
       "Content-Type": "application/json",
    }
    ```

    </div>

- **Body**: The body of the HTTP request.

- **Request Timeout**: The timeout in milliseconds for the HTTP request.

- **Validate SSL Certificates**: If true, validate the SSL certificate of the remote endpoint.

- **Authentication**: Optionally set the method of authentication to use - Basic or OAuth 2.0.  
  ![HTTP Node Step - Authentication](https://docs.rundeck.com/docs/assets/img/http-node-step-auth.png)  

- **Username/Client ID**: The username or client ID used for authentication.

- **Password/Client Secret**: The password or secret key used for authentication. Select a secret from Key Storage.

- **OAuth Token URL**: If using OAuth, provide the endpoint URL at which to obtain tokens.

- **OAuth Validate URL**: If using OAuth, provide the endpoint URL at which to validate token responses.

- **Check Response Code?**: If true, the step will fail if the response code does not match the expected response code.

- **Response Code**: The expected response code from the HTTP request.

- **Print Response?**: If true, the response from the HTTP request will be printed to the log.

- **Print Response to File?**: If true, the response from the HTTP request will be printed to a file.

  - **File Path**: The path to the file where the response will be written.

- **Print Response Code?**: If true, the response code from the HTTP request will be printed to the log.

- **Use Proxy Settings?**: If true, the step will use the proxy settings.

  - **Proxy Settings from JVM Configuration**
    >
    > If proxy settings are configured in the JVM configuration or startup command, this plugin can use those settings. To use the JVM proxy settings, set the following property:
    >
    > - Project properties: `project.plugin.WorkflowNodeStep.edu.ohio.ais.rundeck.HttpWorkflowNodeStepPlugin.useJvmProxySettings=true`
    > - Framework properties: `framework.plugin.WorkflowNodeStep.edu.ohio.ais.rundeck.HttpWorkflowNodeStepPlugin.useJvmProxySettings=true` :::

- **Proxy IP**: The host of the proxy server. This can be an IP address or a hostname.

- **Proxy Port**: The port of the proxy server.

> **Tips**
>
> This plugin doesn't support unsafe characters.  
> If you get this error message: `Illegal character in scheme name at index` it means that an unsafe character was used in the HTTP Request. All unsafe characters must always be encoded within a URL. For more information on unsafe characters see [IETF \| Internet Engineering Task Force](https://www.ietf.org/rfc/rfc1738.txt)
