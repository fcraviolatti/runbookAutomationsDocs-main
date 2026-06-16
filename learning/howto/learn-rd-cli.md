---
title: "Learn the Rundeck CLI"
source_url: https://docs.rundeck.com/docs/learning/howto/learn-rd-cli.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Learn the Rundeck CLI

## What is RD-CLI?

Rundeck CLI (RD-CLI) is a Java client to access and interact with a Rundeck Instance from the command line. In a few words, Rundeck CLI is a Rundeck API abstraction tool. With Rundeck CLI is possible to view system information, list executions, list and manage jobs, manage keys, list and manage node source, projects, and jobs in the command line.

## Installation

RD-CLI is available as a separate install from Rundeck Open Source/Enterprise for multiple platforms. There are options to install it using a specific repository or just download the .zip file, uncompress it, and execute the binary directly (inside the `bin` folder).

### CentOS/Redhat based operating systems:

1.  Add the repository with:
    <div class="language-text line-numbers-mode">

    ``` text
    curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh 2> /dev/null | bash -s rundeck
    ```

    </div>
2.  Then install with the following command:
    <div class="language-text line-numbers-mode">

    ``` text
    yum install rundeck-cli
    ```

    </div>
3.  Test RD-CLI with the following command:
    <div class="language-text line-numbers-mode">

    ``` text
    rd
    ```

    </div>

### Debian/Ubuntu based operating systems

1.  Add the repository with the following command:
    <div class="language-text line-numbers-mode">

    ``` text
    curl -s https://packagecloud.io/install/repositories/pagerduty/rundeck/script.deb.sh | os=any dist=any bash
    ```

    </div>
2.  Install with:
    <div class="language-text line-numbers-mode">

    ``` text
    apt-get install rundeck-cli
    ```

    </div>
3.  Test the installation with the following command:
    <div class="language-text line-numbers-mode">

    ``` text
    rd
    ```

    </div>

    ![rd Commands](https://docs.rundeck.com/docs/assets/img/learn-rd-cli-1.png)
    rd Commands

## Configuration

Rundeck CLI needs the Rundeck instance connection information and valid credentials (via user/password method or using a valid token), check [here](https://docs.rundeck.com/docs/manual/10-user.html#generate-api-token) to know how to generate a valid user token on Rundeck.

### Connection info env vars

RD-CLI needs the Rundeck instance address and port, for this, the `RD_URL` environment variable is needed, to save it in your environment just do:

<div class="language-text line-numbers-mode">

``` text
export RD_URL=http://rundeck:4440
```

</div>

Also, itâ€™s possible to define the specific API version in the following way:

<div class="language-text line-numbers-mode">

``` text
export RD_URL=http://rundeck:4440/api/12
```

</div>

These env vars could be saved on `.bashrc` file directly or in `~/.rd/rd.conf` config file (needs the following environment variable to get work: `export RD_CONF=/path/to/rd.conf`).

### Using the User/password method

The following environment variables work to connect to the Rundeck instance via the user/password method.

<div class="language-text line-numbers-mode">

``` text
export RD_USER=rundeck_user

export RD_PASSWORD=password
```

</div>

### Using the Rundeck token method

The following environment variable it work to connect to the Rundeck instance via API token method, take a look at this to see how to create a new token in Rundeck.

<div class="language-text line-numbers-mode">

``` text
export RD_TOKEN=rundeck_token
```

</div>

## How to use the help on RD-CLI

This point is important because RD-CLI offers help for every option that includes. A good way to get help on any RD-CLI command is to put "help" after any action, for example, to get all options available to get jobs info just type:

<div class="language-text line-numbers-mode">

``` text
rd jobs info help
```

</div>

That's applicable for any action. Another example, to see all system options available:

<div class="language-text line-numbers-mode">

``` text
rd system help
```

</div>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/learn-rd-cli-2.png" alt="rd Commands" />
<figcaption aria-hidden="true">rd Commands</figcaption>
</figure>

Now you can see the available commands, so, if you need specific help for `rd system info` action, just do: `rd system info help `and now the command description is available.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/learn-rd-cli-3.png" alt="rd Commands" />
<figcaption aria-hidden="true">rd Commands</figcaption>
</figure>

## First Steps with RD-CLI

1.  See a complete Rundeck instance information `rd system info`![System Info](https://docs.rundeck.com/docs/assets/img/learn-rd-cli-4.png)
2.  See a job information
    <div class="language-text line-numbers-mode">

    ``` text
    rd jobs info -v -i job_id
    ```

    </div>

    Where `-v` is to increase the verbosity and `-i` is the parameter to define the job UUID. ![Job Info](https://docs.rundeck.com/docs/assets/img/learn-rd-cli-5.png)
3.  Upload a job from a file (also updates a job with the same UUID).
    <div class="language-text line-numbers-mode">

    ``` text
    rd jobs load -f SpaceCat.yaml -F yaml -p ProjectEXAMPLE
    ```

    </div>

    ![Job Upload](https://docs.rundeck.com/docs/assets/img/learn-rd-cli-6.png) Where `-f` is the parameter to define the yaml job definition file, `-F` is the file format, and `-p` is the project name parameter.
4.  See an execution info
    <div class="language-text line-numbers-mode">

    ``` text
    rd executions info -v -e 17
    ```

    </div>

    ![Execution Info](https://docs.rundeck.com/docs/assets/img/learn-rd-cli-7.png) Where `-v` is the parameter to increase the output verbosity, `-i` is the parameter to define the execution id and `job_id` is the job id.
5.  Run a job
    <div class="language-text line-numbers-mode">

    ``` text
    rd run -v -i job_id
    ```

    </div>

    ![Run a Job](https://docs.rundeck.com/docs/assets/img/learn-rd-cli-8.png) Where `-v` is the parameter to increase the output verbosity, `-i` is the parameter to define the execution id and `job_id` is the job id.
6.  Run a job with options
    <div class="language-text line-numbers-mode">

    ``` text
    rd run -v -i job_id -- -option_name option_value
    ```

    </div>

    ![Job with Options](https://docs.rundeck.com/docs/assets/img/learn-rd-cli-9.png) Where `-v` is the parameter to increase the output verbosity, `-i` is the parameter to define the execution id, `job_id` is the job id, `-option_name` is the job option name and `option_value` is the value of `-option_name` option.
