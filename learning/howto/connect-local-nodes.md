---
title: "Connect Welcome Projects to Nodes on a Local Network"
source_url: https://docs.rundeck.com/docs/learning/howto/connect-local-nodes.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Connect Welcome Projects to Nodes on a Local Network

The [Welcome Projects](https://docs.rundeck.com/docs/learning/howto/welcome-project-starter.html) are a great way to learn Rundeck along with all the HowTos. Docker Desktop (especially on Mac/Windows) does not easily support connecting to nodes on your local network. This article can be used to map a single Rundeck Node to a single node on your local network\*.

> **Caution**
>
> Disclaimer: These steps aren't supported or recommended for production. It's just a cool solution we found for the Welcome Projects. If you have better ways please feel free to connect with us in the [Rundeck Forums](https://community.pagerduty.com)s.

The following assumes your Welcome Projects are running under Docker Desktop. We will use a program called `socat` to forward traffic through the local Docker Host to the other endpoint on your local network.

## Exercise

MacOS

Windows

Linux

MacOS

1.  Install `socat` using [HomeBrew Instructions](https://formulae.brew.sh/formula/socat).
2.  From your **Terminal** program execute the following command: `socat -d TCP4-LISTEN:<port1>,fork,reuseaddr TCP:<nodeip>:<port2>`
    - `<port1>`: Port on the Docker Host machine that Rundeck will connect to.
    - `<nodeip>`: IP address or host that you would like to forward traffic to.
    - `<port2>`: Port on the destination host where traffic should be sent.
3.  When configuring the Node in your project the *hostname* should be listed as `host.docker.internal`

The `socat` command will remain running until you use *Control-C* to exit.

Windows

Steps coming soon, but should be essentially the same as the MacOS once you have `socat` installed.

Linux

1.  Install `socat` using your package manager:
    - Deb: `apt-get update && apt-get install socat`
    - RPM: `yum install socat`
2.  From your **Terminal** program execute the following command: `socat -d TCP4-LISTEN:<port1>,fork,reuseaddr TCP:<nodeip>:<port2>`
    - `<port1>`: Port on the Docker Host machine that Rundeck will connect to.
    - `<nodeip>`: IP address or host that you would like to forward traffic to.
    - `<port2>`: Port on the destination host where traffic should be sent.
3.  When configuring the Node in your project the *hostname* should be listed as `host.docker.internal`

The `socat` command will remain running until you exit.

An example `socat` command to open up a path to a [Windows Host using WinRM](https://docs.rundeck.com/docs/learning/howto/configuring-windows-nodes.html) on IP address `192.168.1.10` would be:

`socat -d TCP4-LISTEN:5985,fork,reuseaddr TCP:192.168.1.10:5985`

::::

Notes: \*It is possible to use this method to connect to more than one node on your local network, but not within the same destination port. Destinations that use different ports could be handled using multiple `socat` executions. For example, if you wanted to have one Windows Host for WinRM (port 5985) and one for a local mail server (port 25) run the Windows example above a second execution of `socat -d TCP4-LISTEN:25,fork,reuseaddr TCP:192.168.1.10:25` and point your mail server in Rundeck also to `host.docker.internal`

\*\* It would also possible to get extra complicated and map different `<port1>` values to the same destination ports on different end points. Be creative.
