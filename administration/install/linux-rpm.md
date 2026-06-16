---
title: "Installing on Red Hat, Amazon or Oracle Linux distributions"
source_url: https://docs.rundeck.com/docs/administration/install/linux-rpm.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Installing on Red Hat, Amazon or Oracle Linux distributions

## Installing Rundeck

> **Warning**
>
> Please refer to the [System Requirements](https://docs.rundeck.com/docs/administration/install/system-requirements.html) for the latest preparation recommendations.

Enterprise

Community

Enterprise

You can use this script to add the Runbook Automation yum repo:

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh 2> /dev/null | sudo bash -s rundeckpro
```

</div>

Remove `bintray-rundeckpro-rpm.repo` if it exists.

Add the following entries to `/etc/yum.repos.d/rundeck.repo` replacing any existing entries:

<div class="language-properties line-numbers-mode">

``` properties
[rundeckpro]
name=rundeckpro
baseurl=https://packages.rundeck.com/pagerduty/rundeckpro/rpm_any/rpm_any/$basearch
repo_gpgcheck=1
gpgcheck=1
enabled=1
gpgkey=https://packages.rundeck.com/pagerduty/rundeckpro/gpgkey,https://docs.rundeck.com/keys/BUILD-GPG-KEY-20260105.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

</div>

<div class="language-bash line-numbers-mode">

``` bash
sudo yum install java rundeckpro-enterprise
```

</div>

When new versions of Runbook Automation are released, you can upgrade to them using the command:

<div class="language-bash line-numbers-mode">

``` bash
sudo yum update rundeckpro-enterprise
```

</div>

Download rpm package from the [download page](https://download.rundeck.com/) and run:

<div class="language-bash line-numbers-mode">

``` bash
sudo rpm -i rundeckpro-enterprise-5.20.1-20260518-1.noarch.rpm
```

</div>

Community

You can use this script to add the Rundeck yum repo and install Rundeck:

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh 2> /dev/null | sudo bash -s rundeck
```

</div>

When new versions of Rundeck are released, you can upgrade to them using the command:

<div class="language-bash line-numbers-mode">

``` bash
sudo yum update rundeck
```

</div>

Add the following entries to `/etc/yum.repos.d/rundeck.repo` replacing any existing entries:

<div class="language-properties line-numbers-mode">

``` properties
[rundeck]
name=rundeck
baseurl=https://packages.rundeck.com/pagerduty/rundeck/rpm_any/rpm_any/$basearch
repo_gpgcheck=1
gpgcheck=1
enabled=1
gpgkey=https://packages.rundeck.com/pagerduty/rundeck/gpgkey,https://docs.rundeck.com/keys/BUILD-GPG-KEY-20260105.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

</div>

Download rpm package from the [download page](https://download.rundeck.com) and run:

<div class="language-bash line-numbers-mode">

``` bash
sudo rpm -i rundeck-5.20.1-20260518-1.noarch.rpm
```

</div>

## Starting Rundeck

To start Rundeck:

<div class="language-bash line-numbers-mode">

``` bash
sudo service rundeckd start
```

</div>

To verify that the service started correctly, tail the logs:

<div class="language-bash line-numbers-mode">

``` bash
tail -f /var/log/rundeck/service.log
```

</div>

The service is ready once you see something similar to:

<div class="language-text line-numbers-mode">

``` text
Grails application running at http://localhost:4440 in environment: production
```

</div>

## Logging in for the first time

1.  Navigate to [http://localhost:4440/](http://localhost:4440/user/login) in a browser
2.  Log in with the username **admin** and password **admin**

Rundeck is now up and running!

Next, learn how to [create your first Runbook Automation project](https://docs.rundeck.com/docs/manual/03-getting-started.html#project-setup)

## Note about Linux Groups

If you installed Rundeck using the RPM installation method, it will have created a unix group called "rundeck".

<div class="language-text line-numbers-mode">

``` text
$ groups rundeck
rundeck : rundeck
```

</div>

Consult the [usermod](https://linux.die.net/man/8/usermod) command to modify a user account.
