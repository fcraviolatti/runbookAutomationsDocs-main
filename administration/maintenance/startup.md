---
title: "Startup and Shutdown"
source_url: https://docs.rundeck.com/docs/administration/maintenance/startup.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Startup and Shutdown

Rundeck installation includes a control script used for starting and stopping the Rundeck server process. The control script provides a number of actions:

    rundeckd [start|stop|restart|condrestart|status]

### RPM and DEB

The RPM and DEB installations include the placement of the boot control script that will automatically start Rundeck when the system boots.

The script is located here: `/etc/init.d/rundeckd`

*Startup*

<div class="language-bash line-numbers-mode">

``` bash
/etc/init.d/rundeckd start
```

</div>

*Shutdown*

<div class="language-bash line-numbers-mode">

``` bash
/etc/init.d/rundeckd stop
```

</div>

#### Setting JAVA_HOME

When using the RPM, by default rundeck will use *java* found in your path. Various RPM based distributions provide ways of managing which version of java is found. CentOS uses `/usr/sbin/alternatives` and the processing of setting alternatives can be found here: <http://wiki.centos.org/HowTos/JavaOnCentOS>.

If you have installed a JDK or JRE in a unique directory and do not want to alter the global system configuration, then simply setting JAVA_HOME before running any command will use the version of java found in JAVA_HOME/bin. Updating /etc/rundeck/profile with JAVA_HOME is another option as well.

### Launcher

The Launcher installation generates the script into the RDECK_BASE directory.

The script is located here: `$RDECK_BASE/server/sbin/rundeckd`.

*Startup*

<div class="language-bash line-numbers-mode">

``` bash
$RDECK_BASE/server/sbin/rundeckd start
```

</div>

*Shutdown*

<div class="language-bash line-numbers-mode">

``` bash
$RDECK_BASE/server/sbin/rundeckd stop
```

</div>

You may choose to incorporate this script into your server's operating system specific boot process.
