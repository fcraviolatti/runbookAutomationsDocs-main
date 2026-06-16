---
title: "Use the plugin bootstrap tool"
source_url: https://docs.rundeck.com/docs/learning/howto/plugin-bootstrap.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Use the plugin bootstrap tool

[Here](https://github.com/rundeck/plugin-bootstrap/releases) you can download the latest release of the plugin-bootstrap tool.

### Installing from zip file

Download the tar or zip distribution, and use the tool `<extraction-path>/bin/rundeck-plugin-bootstrap`.

### Installing from deb package

<div class="language-bash line-numbers-mode">

``` bash
sudo dpkg -i <download-path>/rundeck-plugin-bootstrap-X.Y.Z-1_all.deb
```

</div>

### Installing from rpm package

<div class="language-bash line-numbers-mode">

``` bash
sudo rpm -i <download-path>/rundeck-plugin-bootstrap-X.Y.Z-1.noarch.rpm
```

</div>

### Check the available options

To confirm that you have the bootstrap tool, run:

<div class="language-bash line-numbers-mode">

``` bash
rundeck-plugin-bootstrap --help

Usage: plugin-bootstrap [-hV] -d=<destinationDirectory> -n=<pluginName>
                        -s=<serviceType> -t=<pluginType>
Create a Rundeck plugin artifact.
  -d, --destinationDirectory=<destinationDirectory>
                  The directory in which the artifact directory will be generated
  -h, --help      Show this help message and exit.
  -n, --pluginName=<pluginName>
                  Plugin Name.
  -s, --serviceType=<serviceType>
                  Rundeck Service Type: ResourceModelSource, Notification,
                    WorkflowStep, WorkflowNodeStep, LogFilter, NodeExecutor,
                    Orchestrator, FileCopier, RemoteScriptNodeStep,
                    NodeExecutorFileCopier, Option, UI
  -t, --pluginType=<pluginType>
                  Plugin Type: java, script, ui
  -V, --version   Print version information and exit.
```

</div>

### Generate the Java plugin project structure

Now we're ready to generate the Java plugin project structure using the `rundeck-plugin-bootstrap` tool.

<div class="language-bash line-numbers-mode">

``` bash
rundeck-plugin-bootstrap -d rundeck-plugins/ -n hellojava -t java -s WorkflowStep

Plugin generated at: rundeck-plugins/hellojava
```

</div>

Then we initialize the Gradle build script.

<div class="language-bash line-numbers-mode">

``` bash
cd rundeck-plugins/hellojava
gradle wrapper

BUILD SUCCESSFUL in 1s
1 actionable task: 1 executed
```

</div>

## Verify that we can deploy the plugin

### Running the example tests

To verify that our environment is set up correctly, we can run the plugin tests that the bootstrap tool generated:

<div class="language-bash line-numbers-mode">

``` bash
./gradlew test
```

</div>

To package up the compiled files into a single .jar file that we can easily deploy, run:

<div class="language-bash line-numbers-mode">

``` bash
./gradlew build
```

</div>

Now the plugin should've been generated in `build/libs/<plugin-package-name>.jar`:

<div class="language-bash line-numbers-mode">

``` bash
ls build/libs/

hellojava-0.1.0.jar
```

</div>

### Deploying the plugin to a local environment

Deploy the new plugin on an existant instance or use a [fresh installation](https://docs.rundeck.com/docs/administration/install/#installation).

Once the Rundeck server is up, we must login and click the system menu gear icon, plugins submenu and click on Upload Plugin. AAA

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/upload-plugin-submenu.png" alt="Upload Plugin Menu" />
<figcaption aria-hidden="true">Upload Plugin Menu</figcaption>
</figure>

Browse the plugin in the local filesystem or on the internet and install.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/hellojava-browse-plugin-n-install.png" alt="Browse Plugin and Install" />
<figcaption aria-hidden="true">Browse Plugin and Install</figcaption>
</figure>
