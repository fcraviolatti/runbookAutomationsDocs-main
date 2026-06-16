---
title: "Installing on Ubuntu or Debian Linux distributions"
source_url: https://docs.rundeck.com/docs/administration/install/linux-deb.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Installing on Ubuntu or Debian Linux distributions

## Installing Rundeck

> **Warning**
>
> Please refer to the [System Requirements](https://docs.rundeck.com/docs/administration/install/system-requirements.html) for the latest preparation recommendations.

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get install openjdk-11-jre-headless
```

</div>

Enterprise

Community

Enterprise

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/deb-setup.sh 2> /dev/null | sudo bash -s rundeckpro
```

</div>

Import the repo signing key:

<div class="language-bash line-numbers-mode">

``` bash
curl -fsSL https://packages.rundeck.com/pagerduty/rundeck/gpgkey | sudo tee /etc/apt/trusted.gpg.d/rundeck-key.asc && chown root:root /etc/apt/trusted.gpg.d/rundeck-key.asc && chmod 644 /etc/apt/trusted.gpg.d/rundeck-key.asc
```

</div>

Add the following to `/etc/apt/sources.list.d/rundeck.list` replacing existing entries:

<div class="language-bash line-numbers-mode">

``` bash
deb https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
deb-src https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
```

</div>

Update apt cache and install:

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get update
sudo apt-get install rundeckpro-enterprise
```

</div>

1.  First, Check for existing versions installed

<div class="language-bash line-numbers-mode">

``` bash
dpkg --list | grep -i rundeckpro-enterprise
```

</div>

1.  Then, remove existing version to perform a clean install.

<div class="language-bash line-numbers-mode">

``` bash
apt remove rundeckpro-enterprise
dpkg --purge rundeckpro-enterprise && apt install rundeckpro-enterprise
```

</div>

Download `deb` package from [the download page](https://download.rundeck.com/) and run:

<div class="language-bash line-numbers-mode">

``` bash
sudo dpkg -i rundeckpro-enterprise_5.20.1-20260518-1_all.deb
```

</div>

Community

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/deb-setup.sh 2> /dev/null | sudo bash -s rundeck
```

</div>

Import the repo signing key:

<div class="language-bash line-numbers-mode">

``` bash
curl -L https://packages.rundeck.com/pagerduty/rundeck/gpgkey | sudo apt-key add -
```

</div>

Add the following to `/etc/apt/sources.list.d/rundeck.list` replacing existing entries:

<div class="language-bash line-numbers-mode">

``` bash
deb https://packages.rundeck.com/pagerduty/rundeck/any/ any main
deb-src https://packages.rundeck.com/pagerduty/rundeck/any/ any main
```

</div>

Update apt cache and install:

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get update
sudo apt-get install rundeck
```

</div>

Download deb package from [the download page](https://docs.rundeck.com/downloads.html) and run:

<div class="language-bash line-numbers-mode">

``` bash
sudo dpkg -i rundeck_5.20.1-20260518-1_all.deb
```

</div>

## Starting Rundeck

To start Rundeck:

<div class="language-bash line-numbers-mode">

``` bash
sudo systemctl daemon-reload
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

1.  Navigate to [http://localhost:4440/](http://localhost:4440) in a browser.
2.  Log in with the username **admin** and password **admin**

Rundeck is now up and running!

Next, learn how to [create your first project](https://docs.rundeck.com/docs/manual/03-getting-started.html#project-setup)
