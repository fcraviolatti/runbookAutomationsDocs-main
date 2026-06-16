---
title: "Installing as an executable war"
source_url: https://docs.rundeck.com/docs/administration/install/jar.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Installing as an executable war

Use the executable war as an alternative to a system package:

1.  [Download](https://download.rundeck.com) the executable war (Java) file.
2.  Define RDECK_BASE environment variable to the location of the install
    <div class="language-bash line-numbers-mode">

    ``` bash
    export RDECK_BASE=$HOME/rundeck; # or where you like it
    ```

    </div>
3.  Create the directory for the installation.
    <div class="language-bash line-numbers-mode">

    ``` bash
    mkdir -p $RDECK_BASE
    ```

    </div>
4.  Copy the executable war to the installation directory.
    <div class="language-bash line-numbers-mode">

    ``` bash
    cp rundeck-5.20.1-20260518.war $RDECK_BASE
    ```

    </div>
5.  Change directory and run the WAR.
    <div class="language-bash line-numbers-mode">

    ``` bash
    cd $RDECK_BASE
    java -Xmx4g -jar rundeck-5.20.1-20260518.war
    ```

    </div>
6.  Wait for the Started message.
    <div class="language-text line-numbers-mode">

    ``` text
    Grails application running at http://ecto1.local:4440 in environment: production
    ```

    </div>
7.  Update your shell environment
    <div class="language-bash line-numbers-mode">

    ``` bash
    PATH=$PATH:$RDECK_BASE/tools/bin
    MANPATH=$MANPATH:$RDECK_BASE/docs/man
    ```

    </div>

If you get an error message that resembles the one below, you probably are using an unsupported Java version.

<div class="language-text line-numbers-mode">

``` text
Exception in thread "main" java.lang.UnsupportedClassVersionError: Bad version number in .class file
```

</div>

See the [startup and shutdown](https://docs.rundeck.com/docs/administration/maintenance/startup.html) section for instructions on using the `rundeckd` shell tool to manage the rundeck server process.

## Logging in for the first time

1.  Navigate to [http://localhost:4440/](http://localhost:4440/user/login) in a browser
2.  Log in with the username **admin** and password **admin**

Rundeck is now up and running!

Next, learn how to [create your first project](https://docs.rundeck.com/docs/manual/03-getting-started.html#project-setup)

### Updating

When you need to update rundeck and you can not find the relevant section on the docs you are probably on a quite recent version.

- Stop rundeck
- download the new war
- open a prompt, optionally setting RDECK_BASE and launch --installonly
  <div class="language-bash line-numbers-mode">

  ``` bash
  java -jar rundeck-5.20.1-20260518.war --installonly
  ```

  </div>
- copy over your customizations
- don't forget, e.g., sqljdbc41.jar in `%RDECK_BASE%\server\lib`
- start rundeck

### Executable War Options

The executable war can take a number of options to specify how the server should start. If you execute with a "-h" you will see the usage information:

<div class="language-bash line-numbers-mode">

``` bash
java -Xmx4g -jar rundeck-5.20.1-20260518.war -h
```

</div>

<div class="language-text line-numbers-mode">

``` text
usage: java [JAVA_OPTIONS] -jar rundeck.war  [-c PATH] [-d]
       [--installonly] [-s PATH] [-b PATH] [-p PATH] [-h] [-x PATH]
       [--skipinstall] [--serverdir PATH] [--datadir PATH]

Run the rundeck server, installing the necessary components if they do not exist.
    --skipinstall         Skip the extraction of the utilities from the launcher.
    --installonly         Perform installation only and do not start the server.
 -b,--basedir <PATH>      The basedir
 -c,--configdir <PATH>    The location of the configuration.
 -d                       Show debug information
 -h,--help                Display this message.
 -p,--projectdir <PATH>   The location of Rundeck's project data.
 -s,--sbindir <PATH>      The install directory for the tools used by administrators.
 -x,--bindir <PATH>       The install directory for the tools used by users.
```

</div>

These options can be used to customize the directories used by the executable war. By default all the directories are organized by convention within the current working directory where the executable war is located.

### System Properties

See [Rundeck Configuration - System Properties Configuration](https://docs.rundeck.com/docs/administration/configuration/system-properties.html)

For more information about using SSL, see [Configuring Rundeck for SSL](https://docs.rundeck.com/docs/administration/security/ssl.html).
