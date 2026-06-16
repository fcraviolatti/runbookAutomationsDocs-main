---
title: "Builtin Node Steps"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/builtin.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Builtin Node Steps

### Command step

Use the command step to call system commands. Enter any command string you would type at the terminal on the remote hosts.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0404.png" alt="Command step type" />
<figcaption aria-hidden="true">Command step type</figcaption>
</figure>

### Script step

Execute the supplied shell script content. Optionally, can pass an argument to the script specified in the lower text field.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0405.png" alt="Script step type" />
<figcaption aria-hidden="true">Script step type</figcaption>
</figure>

> **Warning**
>
> If an exception is thrown with the message `Cannot run program, error = 26 Text file busy` when executing the script step, a node attribute `enable-sync=true` can be configured to enable a `sync` command to be executed (in background) before executing the script, avoiding this scenario.

### Script file step

Executes the script file local to the server to the filtered Node set. Arguments can be passed to the script by specifying them in the lower text field.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0406.png" alt="Script file step type" />
<figcaption aria-hidden="true">Script file step type</figcaption>
</figure>

### Script URL step

Downloads a script from a URL, and executes it to the filtered Node set. Arguments can be passed to the script by specifying them in the lower text field.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0406.png" alt="Script URL step type" />
<figcaption aria-hidden="true">Script URL step type</figcaption>
</figure>

The URL can contain [Context Variables](https://docs.rundeck.com/docs/manual/jobs/job-variables.html) that will be expanded at runtime.

### Job reference step

To call another saved Job, create a Job Reference step. Enter the name of the Job and its group.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0407.png" alt="Job reference step type" />
<figcaption aria-hidden="true">Job reference step type</figcaption>
</figure>

The Job Reference form provides a Job browser to make it easier to select from the existing set of saved Jobs. Click the "Choose A Job..." link and navigate to the desired Job.

Finally, if the Job defines Options, you can specify them in the commandline arguments text field and can include variable expansion to pass any input options for the current job. Format:

    -optname <value> -optname <value> ...

The format for specifying options is exactly the same as you would pass to the `run` commandline tool, and you can substitute values of input options to the current job. For example:

    -opt1 something -opt2 ${option.opt2}

This would set the value "something" for the Job's "opt1" option, and then pass the "opt2" option directly from the top-level job to the Job reference.

This is similar to calling the other Job with \[run\]:

<div class="language-bash line-numbers-mode">

``` bash
run [filter-options] -j group/jobname -- -opt1 something -opt2 somethingelse
```

</div>

If the Job has required Options that are not specified on the arguments line, then a "defaultValue" of that option will be used if it is defined. If a required option does not have a default value, then the execution will fail because the option is not specified.

Job References can be run as either *Node Steps* or *Workflow Steps* (see [Workflow Steps : Types of Steps](https://docs.rundeck.com/docs/manual/jobs/job-workflows.html#workflow-steps)). When you choose to use a Job Reference as a *Node Step*, you can use the Node context variables within the arguments string to the Job.

#### Overriding Node Filters

You can override the Node Filters used in the referenced Job. Click the "Override Node Filters?" button to expand the Node Filter area.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/job-ref-node-filter-override.png" alt="Job Reference Node Filter Override" />
<figcaption aria-hidden="true">Job Reference Node Filter Override</figcaption>
</figure>

Enter a new filter in the "Node Filter" input field to preview the matched nodes.

Once you enter a new filter, you can modify the other aspects for the Node Dispatching used by the Job Reference:

- Thread Count
- Node failure behavior
- Node Rank attribute
- Node Rank order

### Copy File step

Copy a file to a destination on a remote node.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/copy-file-step.png" alt="Copy File Step" />
<figcaption aria-hidden="true">Copy File Step</figcaption>
</figure>

#### Configuration

Source Path  
Path on the rundeck server for the file or base directory (recursive/wildcard search).

Destination Path  
Path on the remote node for the file destination. If the path ends with a /, the same filename as the source will be used.

Pattern  
Wildcard pattern (optional). E.g: `**/*.txt`

Recursive copy  
Recursively copy source dir, or matched files and dirs to the destination path.

Print transfer information  
Log information about the file copy

### Local Command step

Run a command locally on the server

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/local-command-step.png" alt="Local Command Step" />
<figcaption aria-hidden="true">Local Command Step</figcaption>
</figure>

#### Configuration

Command  
The command (runs locally)

### Data Node step

Produce data values for a node.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/data-node-step.png" alt="Data Node Step" />
<figcaption aria-hidden="true">Data Node Step</figcaption>
</figure>

#### Configuration

Data  
Properties formatted data to set for the current node

Format  
Format for the data. One of: `properties`, `json`, or `yaml`

### HTTP Request Node Step

This plugin executes an HTTP/S request to a remote endpoint.

![HTTP Node Step](https://docs.rundeck.com/docs/assets/img/http-request-step.png)  

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
       "name": "User-Agent",
       "value": "Buddy"
    },
    {
       "name": "Content-Type",
       "value": "application/json"
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
    > - Framework properties: `framework.plugin.WorkflowNodeStep.edu.ohio.ais.rundeck.HttpWorkflowNodeStepPlugin.useJvmProxySettings=true`

- **Proxy IP**: The host of the proxy server. This can be an IP address or a hostname.

- **Proxy Port**: The port of the proxy server.

> **Tips**
>
> This plugin doesn't support unsafe characters.  
> If you get this error message: `Illegal character in scheme name at index` it means that an unsafe character was used in the HTTP Request. All unsafe characters must always be encoded within a URL. For more information on unsafe characters see [IETF \| Internet Engineering Task Force](https://www.ietf.org/rfc/rfc1738.txt)

## Notes

### Advanced Script options

For [Script steps](#script-step), [Script file steps](#script-file-step), and [Script URL steps](#script-url-step), you can specify an optional *Invocation* string to declare how the script should be executed.

Click on the "Advanced" link to reveal the input.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/job_workflow_script_interpreter.png" alt="Advanced Script Settings" />
<figcaption aria-hidden="true">Advanced Script Settings</figcaption>
</figure>

Enter a command that will be used as the *invocation* to run the script, by including `${scriptfile}` to define where the resulting file will appear in the invocation command. For example, you can execute the script using `sudo` by entering:

<div class="language-bash line-numbers-mode">

``` bash
sudo -u username ${scriptfile}
```

</div>

This will then allow your script to make use of [Sudo authentication](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html#secondary-sudo-password-authentication).

The effective commandline for your script will become:

<div class="language-bash line-numbers-mode">

``` bash
sudo -u username [scriptfile] arguments ...
```

</div>

If necessary, you can check the "Quote arguments to script invocation string?" checkbox, which will then quote both the scriptfile and arguments before passing to the invocation command:

    [invocation string] "[scriptfile] arguments ..."

> **Tips**
>
> If an specific encoding is needed when using power shell executor, you can set this through the invocation string:
>
>     powershell [Console]::OutputEncoding = [Text.UTF8Encoding]::utf8 ; "[scriptfile] arguments ..."
>
> <figure>
> <img src="https://docs.rundeck.com/docs/assets/img/powershell_encoding.png" alt="Script Encoding" />
> <figcaption aria-hidden="true">Script Encoding</figcaption>
> </figure>

### Changing the File extension

You can also change the file extension set on the temporary file when it is invoked. This might be necessary if your command expects a file with a certain extension.

Set the "File Extension" field to the desired extension. The `.` is optional, e.g. `.ps` or `sh`. The default is determined by the type of target node. Unix uses `.sh` and Windows uses `.bat`.

### Quoting arguments to steps

When you define a [Command](#command-step) or arguments to any Script or Job reference step, your arguments are interpreted as a space-separated sequence of strings. If you need to use spaces or quotes within the argument, here are some rules for quoting arguments:

- If you have an argument with a space character, you can use either double or single quotes:
  - `"my argument"`: interpreted as `my argument`
  - `'my argument'`: interpreted as `my argument`
- If you need to embed quotes within a quoted argument, you can wrap it in the opposite kind of quote (double or single):
  - `'"double quotes"'`: interpreted as `"double quotes"`
  - `"'single quotes'"`: interpreted as `'single quotes'`
- Or use doubled-up quote characters
  - `"""double quotes"""`: interpreted as `"double quotes"`
  - `'''single quotes'''`: interpreted as `'single quotes'`

> **Tips**
>
> On version 3.4.1 quoting in jobs was changed. If you want to keep using the same quoting behavior as previous versions, you can add a new property in "framework.properties" file.
>
> <div class="language-text line-numbers-mode">
>
> ``` text
> rundeck.feature.quoting.backwardCompatible=true
> ```
>
> </div>
