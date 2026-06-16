---
title: "Upgrade Rundeck 2.11.X to Rundeck 3.X"
source_url: https://docs.rundeck.com/docs/upgrading/upgrading-to-rundeck3.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Upgrade Rundeck 2.11.X to Rundeck 3.X

Updated June 1, 2018

## Rundeck Launcher

The "launcher jar" for Rundeck 2 is gone. However, the .war file now operates the same way. Just use the .war in the same way as the previous launcher jar, or deploy it as a webapp.

To upgrade to Rundeck 3 using launcher use the following steps:

**NOTE: replace `$RDECK_BASE` below with the real path.**

- Stop Rundeck Service, eg: `$RDECK_BASE/server/sbin/rundeckd stop`
- In case you have customs plugins in `libext` folder, backup them. For example, you can move the full `libext`:
  <div class="language-bash line-numbers-mode">

  ``` bash
  mv $RDECK_BASE/libext $RDECK_BASE/libext.2-11
  ```

  </div>
- Remove previous "source" folders:
  <div class="language-bash line-numbers-mode">

  ``` bash
  rm -rf $RDECK_BASE/server/exp/ $RDECK_BASE/server/lib/ $RDECK_BASE/server/sbin/ $RDECK_BASE/tools/
  ```

  </div>
- Copy the new war file to `$RDECK_BASE` and install it:
  <div class="language-bash line-numbers-mode">

  ``` bash
  java -jar rundeck-3.X.war --installonly
  ```

  </div>
- Add the following attribute to `$RDECK_BASE/server/config/rundeck-config.properties`
  <div class="language-properties line-numbers-mode">

  ``` properties
  rundeck.log4j.config.file = $RDECK_BASE/server/config/log4j.properties
  ```

  </div>
- Copy the "custom" plugins back to `$RDECK_BASE/libext` folder
- Start rundeck 3: `$RDECK_BASE/server/sbin/rundeckd start`

## Rundeck DEB Package

The upgrade process can be done using the `.deb` file or using the command `apt-get`:

**If using deb package**

<div class="language-bash line-numbers-mode">

``` bash
sudo dpkg -i rundeck-3.0.X.deb
```

</div>

**If using apt-get**

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get upgrade rundeck
```

</div>

**Configuration Files:**

When the upgrade command is run, the upgrade process will prompt about what to do with the new version of config files. In the case of `rundeck-config.properties`, a merge needs to be done between the old and new version, because the attribute `rundeck.log4j.config.file` is needed on Rundeck 3 (this attribute is part of the default `rundeck-config.properties` template):

<div class="language-text line-numbers-mode">

``` text
Configuration file '/etc/rundeck/rundeck-config.properties'
 ==> Modified (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** rundeck-config.properties (Y/I/N/O/D/Z) [default=N] ?
```

</div>

For example, if you select "YES" the older file will be moved to `rundeck-config.properties.dpkg-old`, and `rundeck-config.properties` will be loaded with the default values (so a merge will be needed)

<div class="language-text line-numbers-mode">

``` text
-rw-r----- 1 rundeck rundeck  986 May 11 19:13 realm.properties
-rw-r----- 1 rundeck rundeck  730 May 11 19:13 project.properties
-rw-r----- 1 rundeck rundeck 7529 May 11 19:13 log4j.properties
-rw-r----- 1 rundeck rundeck  136 May 11 19:13 jaas-loginmodule.conf
-rw-r----- 1 rundeck rundeck 1104 May 11 19:13 apitoken.aclpolicy
-rw-r----- 1 rundeck rundeck  738 May 11 19:13 admin.aclpolicy
-rw-r----- 1 rundeck rundeck 1438 Jun  1 19:28 framework.properties
-rw-r----- 1 rundeck rundeck  454 Jun  1 19:32 rundeck-config.properties
-rw-r----- 1 rundeck rundeck 3419 Jun  1 19:32 profile
-rw-r----- 1 rundeck rundeck  511 Jun  1 19:32 cli-log4j.properties
-rw-r----- 1 rundeck rundeck  673 Jun  4 14:22 rundeck-config.properties.dpkg-old
drwxr-x--- 1 rundeck rundeck 4096 Jun  4 14:25 ssl
```

</div>

A restart is necessary after the merge of `rundeck-config.properties`

## Rundeck RPM Package

The upgrade process can be done using the `.rpm` file or using the command `yum`:

### Using rpm package

<div class="language-bash line-numbers-mode">

``` bash
# rpm -U rundeck-3.x.rpm rundeck-config-3.X.rpm

warning: /etc/rundeck/framework.properties created as /etc/rundeck/framework.properties.rpmnew
warning: /etc/rundeck/rundeck-config.properties created as /etc/rundeck/rundeck-config.properties.rpmnew
rundeck.server.uuid = XXXXXXXXXXXXXXX
```

</div>

### Using yum

<div class="language-bash line-numbers-mode">

``` bash
# yum upgrade rundeck rundeck-config
```

</div>

In the case of the RPM upgrade, the old properties files are not modified, and the new files are saved with the extension `.rpmnew`. For the configuration file `rundeck-config.properties` a merge is needed to include new default attribute (`rundeck.log4j.config.file`).

<div class="language-bash line-numbers-mode">

``` bash
# ls -lrt
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

If the `profile` file was modified on 2.11.x, the new profile file (for 3.x) will be created with the name `profile.rpmnew`. If that is the case, merge the changes on the old file and move them to the new one, eg:

<div class="language-bash line-numbers-mode">

``` bash
# mv /etc/rundeck/profile.rpmnew /etc/rundeck/profile
```

</div>

A restart is necessary after the merge of `rundeck-config.properties` or/and `profile` file.

## Tomcat War deployment

- Stop Tomcat
- Delete `$tomcat.base/webapps/rundeck`
- Delete `$tomcat.base/webapps/rundeck.war`
- Place Rundeck 3 as the old war file `$tomcat.base/webapps/rundeck.war`
- Remove `$rdeck.base/var/.install_complete` and `$rdeck.base/var/.install_complete-missing-ver` if any.
- In case you have customs plugins in `libext` folder, backup them. For example, you can move the full libext:
  <div class="language-bash line-numbers-mode">

  ``` bash
  mv $rdeck.base/libext $rdeck.base/libext.2-11
  ```

  </div>
- Start Tomcat
- Copy the "custom" plugins back to `$rdeck.base/libext` folder.

### NOTES FOR TOMCAT:

- Due to changes in authentication, `tomcat-users.xml` and other Tomcat's authentication modules no longer work, you should configure users as in a [launcher installation](https://docs.rundeck.com/docs/administration/security/authentication.html#authenticating-users).

- If you do not have "-Drundeck.config.location" defined or configured in `$tomcat.base/bin/setenv.sh` file (`tomcat.base\bin\setenv.bat` for Windows), it will take `$rdeck.base/server/config/rundeck-config.properties`.
