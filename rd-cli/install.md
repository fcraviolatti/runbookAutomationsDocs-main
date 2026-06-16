---
title: "Rundeck CLI - Install"
source_url: https://docs.rundeck.com/docs/rd-cli/install.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Rundeck CLI - Install

All artifacts can be downloaded from: [github releases](https://github.com/rundeck/rundeck-cli/releases/latest)

- [zip install](#zip-install) `rd-2.1.1 .zip` / `rd-2.1.1 .tar`
- [standalone executable jar](#jar-install) `rundeck-cli-2.1.1 -all.jar`
- [rpm install](#yum-usage) `rundeck-cli-2.1.1 .noarch.rpm`
- [debian install](#debian-usage) `rundeck-cli-2.1.1 _all.deb`
- [arch install](#arch-linux-install)

## Homebrew

Installation is now available via [homebrew](https://brew.sh).

<div class="language-text line-numbers-mode">

``` text
brew tap rundeck/rundeck-cli
brew install rundeck-cli
```

</div>

## Jar install

Download the `rundeck-cli-2.1.1 -all.jar` from [github releases](https://github.com/rundeck/rundeck-cli/releases/latest).

Simply execute:

<div class="language-bash line-numbers-mode">

``` bash
    java -jar rundeck-cli-2.1.1
-all.jar
```

</div>

## Zip install

Download the `rd-2.1.1 .zip` from [github releases](https://github.com/rundeck/rundeck-cli/releases/latest).

Install:

    $ unzip rd-2.1.1
    .zip
    rd-2.1.1

    âââ bin
    âÂ Â  âââ rd
    âÂ Â  âââ rd.bat
    âââ lib
        âââ ....jar

Execute:

<div class="language-bash line-numbers-mode">

``` bash
rd-2.1.1
/bin/rd
```

</div>

## Yum usage

------------------------------------------------------------------------

**NOTE**: If you previously installed via Bintray Yum repo (RD version prior to 1.3.9), please remove the `/etc/yum.repos.d/bintray.repo` file if it exists.

------------------------------------------------------------------------

Add Yum Repo:

<div class="language-text line-numbers-mode">

``` text
curl -s https://packagecloud.io/install/repositories/pagerduty/rundeck/script.rpm.sh?any=true | sudo bash
```

</div>

Optional: enable all gpg checks:

<div class="language-text line-numbers-mode">

``` text
$ sed -i.bak s/gpgcheck=0/gpgcheck=1/ /etc/yum.repos.d/rundeck.repo
$ rpm --import https://raw.githubusercontent.com/rundeck/packaging/main/pubring.gpg
```

</div>

Finally: install rundeck-cli

<div class="language-text line-numbers-mode">

``` text
yum install rundeck-cli
```

</div>

### Download RPM Package

Or Download individual packages at [rundeck-cli rpms via packagecloud](https://packagecloud.io/app/pagerduty/rundeck/search?q=rundeck-cli&filter=rpms&filter=rpms&dist=)

## Debian usage

------------------------------------------------------------------------

**NOTE**: If you previously installed via the Bintray APT repo (rd version prior to 1.3.9), please remove the line `deb https://dl.bintray.com/rundeck/rundeck-deb /` from your `/etc/apt/sources.list` file.

------------------------------------------------------------------------

Install the packagecloud APT repo for rundeck:

<div class="language-text line-numbers-mode">

``` text
curl -s https://packagecloud.io/install/repositories/pagerduty/rundeck/script.deb.sh | os=any dist=any bash
```

</div>

Finally: install rundeck-cli

<div class="language-text line-numbers-mode">

``` text
apt-get install rundeck-cli
```

</div>

### Download Deb Package

Or Download individual packages at [rundeck-cli debs via packagecloud](https://packagecloud.io/app/pagerduty/rundeck/search?q=rundeck-cli&filter=debs)

## Arch Linux install

Make sure you're familiarized with [the AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository)

<div class="language-text line-numbers-mode">

``` text
git clone https://aur.archlinux.org/rundeck-cli.git
cd rundeck-cli
makepkg -i
```

</div>

## Windows install

Download the `rd-2.1.1 .zip` from [github releases](https://github.com/rundeck/rundeck-cli/releases/latest).

To install, unzip the file in your desired installation directory.

Add the \$DestinationDirectory\bin folder to Windows PATH.

Set up Windows Environment Variables for RD_URL and RD_TOKEN if desired.

To execute, open a Powershell/CMD and run:

<div class="language-text line-numbers-mode">

``` text
rd.bat
```

</div>

> **To avoid conflicts with 'rd' Windows command to delete a directory, you should rename your 'rd.bat' file to something else, like 'rdcli.bat' :::**
