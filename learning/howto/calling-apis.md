---
title: "Call APIs from Rundeck"
source_url: https://docs.rundeck.com/docs/learning/howto/calling-apis.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Call APIs from Rundeck

Modern applications use the [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP) protocol to communicate with each other and send or obtain information from any web service using [HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) like GET, POST, or PUT. For example, to obtain a valid user ID from a web service to use it later in another process/application.

To make those HTTP calls we can use an [inline-script](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html#script-step)\] with a [cURL](https://curl.se/) command inside, curl is used in scripts or commands to transfer data and itâ€™s available for any operating system. But this implies maintaining a lot of code inside a Rundeck workflow.

Rundeckâ€™s Job Steps offer a more user-friendly way to make these calls. For HTTP calls, use the [HTTP Workflow Step Plugin](https://resources.rundeck.com/plugins/rundeck-http-workflow-step-plugin/) in Rundeck. This plugin will send HTTP calls to any web service or HTTP endpoint. The returned data can then be used in subsequent steps. (Check out our [Passing Variables](https://docs.rundeck.com/docs/learning/howto/passing-variables.html) guide).

If you are using our Enterprise version the plugin is already bundled with your installation. Skip straight to the exercises.

## Community Version Prerequisite

The HTTP Workflows Step plugin isnâ€™t bundled with the Rundeck Community version (it is included with [Runbook Automation](https://www.pagerduty.com/platform/automation/process-software/)). For Rundeck Community, follow these steps to install it.

1.  Go to the **System Menu** (Gear Icon in upper right) **\> Plugins \> Upload Plugin**.
2.  Copy the plugin file location from the repository *(Latest link as of last update is below)*
    <div class="language-text line-numbers-mode">

    ``` text
    https://github.com/rundeck-plugins/http-step/releases/download/1.0.12/http-step-1.0.12.jar
    ```

    </div>

    ![Upload Plugin](https://docs.rundeck.com/docs/assets/img/upload-plugin.png)
    Upload Plugin
3.  Paste it on the **Plugin URL** textbox, and click on the **Install** button. ![Plugin Installed!](https://docs.rundeck.com/docs/assets/img/plugin-installed.png)

> An alternative method to install the plugin is to download the .jar file directly from the [repository](https://github.com/rundeck-plugins/http-step/releases/download/1.0.12/http-step-1.0.12.jar) and put it on the `libext` directory (at `` /var/lib/rundeck/libext` on RPM / DEB based installations or  ``\$RDECK_BASE/libext\` directory on WAR based installations). Just copy the the .jar to the folder, no restart is needed.

## Exercise

> **Warning**
>
> For this exercise we will use the site [httpbin.org](http://httpbin.org/) test website, [httpbin.org](http://httpbin.org/) is a simple HTTP request and response service written in python by Ken Reitz. This is not a site owned or run by PagerDuty. **Note: Don't send any sensitive data.** This site is simply used as a test. If you would like to run your own their site has more information about using their [Docker Images](https://github.com/postmanlabs/httpbin#httpbin1-http-request--response-service).

Community Exercise

Community Exercise

## Other Parameters

Other parameters available:

- Request Timeout (How long to wait for a request to complete before failing).
- Validate [SSL Certificates](https://en.wikipedia.org/wiki/Transport_Layer_Security#Digital_certificates) (true or false, validate that SSL certificates are trusted, match the hostname, etc.)
- Authentication section. If the HTTP service uses Basic / [OAuth2](https://en.wikipedia.org/wiki/OAuth#OAuth_2.0_2) authentication. On Basic Auth itâ€™s possible to define the user and password from the Rundeck Key Storage. On OAuth 2.0 add the OAuth Token URL and OAuth Validate URL.
- Validate Response can check the [HTTP response code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) that is returned and fail the step if it is not the expected value. (typically looking for 200)
- Proxy Settings section, if the HTTP service is behind a proxy server, you can define the Proxy IP address and port.

## Additional Information

- If you need to use variables in the *HTTP Request Steps* Headers or Body sections use the format `${data.variable-name}`. For more information about using variables check out [Passing Data Between Steps](https://docs.rundeck.com/docs/learning/howto/passing-variables.html)
- Link to [Example Job](https://github.com/rundeck/welcome-project-community/blob/main/runbooks/yaml/HowTos/Calling_APIs_from_Rundeck.yaml) built using the steps above. Download the YAML and use it in your Rundeck.
- Official plugin description from [the plugin's GitHub repository](https://github.com/rundeck-plugins/http-step).
- [Documentation on different HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).
