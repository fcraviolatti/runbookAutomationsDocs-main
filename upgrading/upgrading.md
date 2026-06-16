---
title: "General Upgrade Guide"
source_url: https://docs.rundeck.com/docs/upgrading/upgrading.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# General Upgrade Guide

## Preparing to Upgrade

Prior to upgrading it is important to read the specific version upgrade steps covered in this section. Due to the complex nature of the solution some versions require specific steps to ensure a successful upgrade. Any version speicific steps will be covered in those pages. The details below cover the overall process for upgrading to any version.

## Preparing to Upgrade your Server

- Download the latest Rundeck version .war from [Runbook Automation Downloads](https://www.rundeck.com/enterprise-downloads) *(requires license)* or [Rundeck OSS Downloads](https://downloads.rundeck.com)

- Stop Rundeck (stop service or kill the process)

- *Windows* Edit the file start_rundeck.bat located on your `$RDECK_BASE` dir and change the name of your rundeck.war file with the name of the downloaded file, e.g. "rundeckpro-enterprise-5.20.1-20260518.war"

<div class="language-text line-numbers-mode">

``` text
 java %RDECK_CLI_OPTS% %RDECK_SSL_OPTS% -jar rundeckpro-enterprise-4.10.2-20201111.war --skipinstall -d >> %CURDIR%\var\logs\service.log 2>&1
```

</div>

- Backup your `$RDECK_BASE\libext` folder (in case you have any custom plugins)

- Backup both folders, `$RDECK_BASE/server/config` and` $RDECK_BASE/etc`, just in case

- Delete these files and dirs:

  <div class="language-text line-numbers-mode">

  ``` text
  $RDECK_BASE/libext/
  $RDECK_BASE/tools/
  $RDECK_BASE/server/lib/
  $RDECK_BASE/server/sbin/
  $RDECK_BASE/var/.firstLogin
  $RDECK_BASE/var/.first-run-3.0.22-20190512 (version number may be different)
  $RDECK_BASE/var/.install-complete-missing-ver
  ```

  </div>

- Copy or move the downloaded rundeck war file into your` $RDECK_BASE` folder

- Start Rundeck from the console and wait until it boots up successfully

<div class="language-text line-numbers-mode">

``` text
java -jar rundeckpro-enterprise-5.20.1-20260518.war
```

</div>

## Installation Specific Notes

### Runnable War

To upgrade Rundeck using the runnable war use the following steps:

- Stop Rundeck Service:

<div class="language-bash line-numbers-mode">

``` bash
$RDECK_BASE/server/sbin/rundeckd stop
```

</div>

- In case you have customs plugins in `libext` folder, backup them. For example, you can move the full `libext`:

<div class="language-bash line-numbers-mode">

``` bash
mv $RDECK_BASE/libext $RDECK_BASE/libext.3
```

</div>

- Remove previous "source" folders:

<div class="language-bash line-numbers-mode">

``` bash
rm -rf $RDECK_BASE/server/lib/rundeck-core*jar $RDECK_BASE/server/sbin/ $RDECK_BASE/tools/ $RDECK_BASE/var/.install_complete-missing-ver
```

</div>

- Run the following command to ensure that all files and directories are created properly:

<div class="language-bash line-numbers-mode">

``` bash
rm var/.install_complete-missing-ver
```

</div>

- Copy the new war file to `$RDECK_BASE` and install it:

<div class="language-bash line-numbers-mode">

``` bash
java -jar rundeck-5.20.1-20260518.war --installonly
```

</div>

- Start Rundeck 3:

<div class="language-bash line-numbers-mode">

``` bash
$RDECK_BASE/server/sbin/rundeckd start
```

</div>

- Copy the "custom" plugins back to `$RDECK_BASE/libext` folder.

### DEB Package

The upgrade process can be done using the `.deb` file or using the command `apt-get`:

**If using deb package**

<div class="language-bash line-numbers-mode">

``` bash
sudo dpkg -i rundeck-5.20.1-20260518.deb
```

</div>

**If using apt-get**

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get upgrade rundeck
```

</div>

### RPM Package

The upgrade process can be done using the `.rpm` file or using the command `yum`.

In the case of the RPM or Yum upgrade, any changed config files will not be modified, and new files are saved with the extension `.rpmnew`. If you have changed your config file, please compare it to the `.rpmnew` file to see what changes might need to be included.

<div class="language-bash line-numbers-mode">

``` bash
$ ls -lrt
total 56
-rw-r----- 1 rundeck rundeck  455 Jun  1 19:34 rundeck-config.properties.rpmnew
-rw-r----- 1 rundeck rundeck  986 Jun  1 19:34 realm.properties
-rw-r----- 1 rundeck rundeck  729 Jun  1 19:34 project.properties
-rw-r----- 1 rundeck rundeck 3426 Jun  1 19:34 profile
-rw-r----- 1 rundeck rundeck 7538 Jun  1 19:34 log4j.properties
-rw-r----- 1 rundeck rundeck  136 Jun  1 19:34 jaas-loginmodule.conf
-rw-r----- 1 rundeck rundeck 1177 Jun  1 19:34 framework.properties.rpmnew
-rw-r----- 1 rundeck rundeck  511 Jun  1 19:34 cli-log4j.properties
-rw-r----- 1 rundeck rundeck 1104 Jun  1 19:34 apitoken.aclpolicy
-rw-r----- 1 rundeck rundeck  738 Jun  1 19:34 admin.aclpolicy
-rw-r----- 1 rundeck rundeck  673 Jun  4 16:02 rundeck-config.properties
-rw-r----- 1 rundeck rundeck 1505 Jun  4 16:02 framework.properties
drwxr-x--- 1 rundeck rundeck 4096 Jun  4 16:08 ssl
```

</div>

#### Using rpm package

<div class="language-bash line-numbers-mode">

``` bash
$ rpm -U rundeck-5.20.1-20260518.rpm

warning: /etc/rundeck/framework.properties created as /etc/rundeck/framework.properties.rpmnew
warning: /etc/rundeck/rundeck-config.properties created as /etc/rundeck/rundeck-config.properties.rpmnew
rundeck.server.uuid = XXXXXXXXXXXXXXX
```

</div>

#### Using yum

<div class="language-bash line-numbers-mode">

``` bash
$ yum upgrade rundeck
```

</div>
