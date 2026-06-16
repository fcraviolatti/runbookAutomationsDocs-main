---
title: "Install Rundeck Community on Centos"
source_url: https://docs.rundeck.com/docs/learning/howto/install-centos.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Install Rundeck Community on Centos

RPM-based Linux distributions are very popular. Rundeck offers the repository and the specific package for this kind of distribution. In this guide, we will show you how to install Rundeck Community on a CentOS 7 operating system.

In this guide we'll cover:

- How to install Rundeck Community on CentOS 7 operating system
- How to configure Rundeck properly to access it

# Prerequisites

If you planning to install CentOS 7 on a physical server consider the minimum requirements [defined here](https://docs.centos.org/en-US/centos/install-guide/Steps-x86/#sect-installation-planning-system-specifications-x86). Considering the [minimum Rundeck requirements](https://docs.rundeck.com/docs/administration/install/system-requirements.html#system-requirements), these specs should be up to at least 4GB of RAM, 2 cores per instance, and 20 GB of hard disk space. You can see all of the available mirrors to [download the Centos 7 ISO install image here](http://isoredirect.centos.org/centos/7/isos/x86_64/).

To install CentOS 7 on a cloud instance (with any provider like Amazon Web Services or MicrosoftÂ® Azure), make sure to cover the Rundeck [minimal requirements defined here](https://docs.rundeck.com/docs/administration/install/system-requirements.html#system-requirements). In the case of Amazon Web Services, make sure to use an instance size of *m4.large or larger*.

[You can find the full guide to install Centos 7 here](https://docs.centos.org/en-US/centos/install-guide/).

The main package requirement for Rundeck is Java 11.

# Steps to Install the Latest Rundeck Community Version on CentOS 7 Linux.

1.  Get and install the repository:
    <div class="language-text line-numbers-mode">

    ``` text
    curl https://raw.githubusercontent.com/rundeck/packaging/main/scripts/rpm-setup.sh 2> /dev/null | bash -s rundeck
    ```

    </div>
2.  Verify the Java version to ensure it meets the requirement:
    <div class="language-text line-numbers-mode">

    ``` text
    java -version
    ```

    </div>

    Example output (actual version numbers can vary):
    <div class="language-text line-numbers-mode">

    ``` text
    openjdk version "11.0.11" 2021-04-20 LTS
    OpenJDK Runtime Environment 18.9 (build 11.0.11+9-LTS)
    OpenJDK 64-Bit Server VM 18.9 (build 11.0.11+9-LTS, mixed mode, sharing)
    ```

    </div>
3.  If you need to install the Java JRE:
    <div class="language-text line-numbers-mode">

    ``` text
    sudo yum install java-11-openjdk
    ```

    </div>
4.  Install Rundeck:
    <div class="language-text line-numbers-mode">

    ``` text
    sudo yum install rundeck
    ```

    </div>
5.  Start the Rundeck service:
    <div class="language-text line-numbers-mode">

    ``` text
    sudo systemctl start rundeckd
    ```

    </div>
6.  Enable the Rundeck service at system boot:
    <div class="language-text line-numbers-mode">

    ``` text
    sudo systemctl enable rundeckd
    ```

    </div>
7.  Rundeck is now up and running. The Rundeck service is available at the following URL:
    <div class="language-text line-numbers-mode">

    ``` text
    http://localhost:4440
    ```

    </div>

# Basic Rundeck Configuration

After installing Rundeck, by default the instanceâ€™s hostname is `localhost. `You wonâ€™t be able to access the Rundeck instance from any node on the network so you need to configure Rundeck to use the hostname where it is installed.

Community Exercise

Community Exercise

1.  Stop the Rundeck Service.
    <div class="language-text line-numbers-mode">

    ``` text
    systemctl stop rundeckd
    ```

    </div>
2.  Open the rundeck-config.properties file (at `/etc/rundeck` path) with any text editor and update this line: `grails.serverURL=http://localhost:4440` Set to your host name (e.g. â€œ`your-rundeck-hostname`â€? is the Rundeck server hostname, you can check it executing the `hostname` command):
    <div class="language-text line-numbers-mode">

    ``` text
    grails.serverURL=http://your-rundeck-hostname:4440
    ```

    </div>
3.  Open the framework.properties file (at `/etc/rundeck` path) and update these lines:
    <div class="language-text line-numbers-mode">

    ``` text
    framework.server.name = localhost
    framework.server.hostname = localhost
    framework.server.url = http://localhost:4440
    ```

    </div>

    Set to your host name (â€œ`your-rundeck-hostname`â€? is the Rundeck server hostname):
    <div class="language-text line-numbers-mode">

    ``` text
        framework.server.name = your-rundeck-hostname
        framework.server.hostname = your-rundeck-hostname
        framework.server.url = http://your-rundeck-hostname:4440
    ```

    </div>
4.  Add the `firewalld` rule which allows the default Rundeck TCP port (4440):
    <div class="language-text line-numbers-mode">

    ``` text
    sudo firewall-cmd --permanent --zone=public --add-port=4440/tcp
    ```

    </div>
5.  Restart the `firewalld` service:
    <div class="language-text line-numbers-mode">

    ``` text
    sudo firewall-cmd --reload
    ```

    </div>
6.  Restart the Rundeck service to get the changes:
    <div class="language-text line-numbers-mode">

    ``` text
    systemctl restart rundeckd
    ```

    </div>

    Now the Rundeck service is available using the hostname and from any network location: `http://your-rundeck-hostname:4440`

## Additional Resources

- [Rundeck System Requirements](https://docs.rundeck.com/docs/administration/install/system-requirements.html#system-requirements)
- [Rundeck installation on Red Hat/Centos](https://docs.rundeck.com/docs/administration/install/linux-rpm.html#installing-on-centos-or-red-hat-linux-distributions)
- [About the rundeck-config.properties file](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#rundeck-config-properties)
