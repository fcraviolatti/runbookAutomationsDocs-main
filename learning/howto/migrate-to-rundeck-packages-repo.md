---
title: "Migrate From Bintray"
source_url: https://docs.rundeck.com/docs/learning/howto/migrate-to-rundeck-packages-repo.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Migrate Packages From Bintray Repo

**April 27th, 2021**

In February, JFrog announced that it would be ending their Bintray distribution service. The official download distributions of Rundeck are now available on a new hosting service. See below for full details about new repository sources and guidance about signing keys. **Any automation that your team has created utilizing Rundeckâ€™s Bintray repositories will need to be updated prior to May 1st, 2021**.

## Migration Instructions

> **Warning**
>
> Rundeck has rotated the signing key used to sign release packages. All previously released `deb`, `rpm`, and `war` packages have been re-signed and uploaded. The new public key can be found [here in the Rundeck packaging repo](https://github.com/rundeck/packaging/blob/main/pubring.gpg).

### Enterprise

Deb

Rpm

War

Deb

The [quick setup script](https://github.com/rundeck/packaging/blob/main/scripts/deb-setup.sh) will configure the Runbook Automation repository, import the new repository signing key, and update apt. Legacy configuration will be replaced.

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/deb-setup.sh 2> /dev/null | sudo bash -s rundeckpro
```

</div>

Import the repo signing key:

<div class="language-bash line-numbers-mode">

``` bash
curl -L https://packages.rundeck.com/pagerduty/rundeckpro/gpgkey | sudo apt-key add -
```

</div>

Add the following to `/etc/apt/sources.list.d/rundeck.list` replacing existing entries:

<div class="language-text line-numbers-mode">

``` text
deb https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
deb-src https://packages.rundeck.com/pagerduty/rundeckpro/any/ any main
```

</div>

Update apt cache:

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get update
```

</div>

Rpm

The [quick setup script](https://github.com/rundeck/packaging/blob/main/scripts/rpm-setup.sh) will configure the Runbook Automation repository. Legacy configuration will be replaced.

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
gpgcheck=0
enabled=1
gpgkey=https://packages.rundeck.com/pagerduty/rundeckpro/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

</div>

War

Visit the [Rundeck download page](https://download.rundeck.com) for updated direct download links.

### Community

Deb

Rpm

War

Deb

The [quick setup script](https://github.com/rundeck/packaging/blob/main/scripts/deb-setup.sh) will configure the Rundeck Community repository, import the new repository signing key, and update apt. Legacy configuration will be replaced.

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

Update apt cache:

<div class="language-bash line-numbers-mode">

``` bash
sudo apt-get update
```

</div>

Rpm

The [quick setup script](https://github.com/rundeck/packaging/blob/main/scripts/rpm-setup.sh) will configure the Runbook Automation repository. Legacy configuration will be replaced.

<div class="language-bash line-numbers-mode">

``` bash
curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh 2> /dev/null | sudo bash -s rundeck
```

</div>

Remove `bintray-rundeckpro-rpm.repo` if it exists.

Add the following entries to `/etc/yum.repos.d/rundeck.repo` replacing any existing entries:

<div class="language-properties line-numbers-mode">

``` properties
[rundeck]
name=rundeck
baseurl=https://packages.rundeck.com/pagerduty/rundeck/rpm_any/rpm_any/$basearch
repo_gpgcheck=1
gpgcheck=0
enabled=1
gpgkey=https://packages.rundeck.com/pagerduty/rundeck/gpgkey
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
```

</div>

War

Visit the [Rundeck download page](https://docs.rundeck.com/downloads.html) for updated direct download links.
