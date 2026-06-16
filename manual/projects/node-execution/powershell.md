---
title: "WinRM Node Execution"
source_url: https://docs.rundeck.com/docs/manual/projects/node-execution/powershell.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# WinRM Node Execution

These plugins will only execute through Runbook Automation installed on Windows or an Enterprise Runner installed on Windows.

There are two plugins:

- **WinRM File Copier**: Copies files to the remote node for execution by the Node Executor. This plugin would be used to execute any Script steps in your workflows, or to copy your own files stored on the Runbook Automation host.
- **WinRM Node Executor Python**: Executes the command and script steps.

The plugins can be enabled in the Project Configuration page by selecting the WinRM Node Executor Python and WinRM File Copier as the default Node Executor and File Copiers.

## Authentication Types

Authentication can happen in two ways, via trusted domain account or by username and password.

### Hosts in Trusted Domain

When all hosts are in a trusted domain, remote execution requires just the username to access the remote hosts. Authentication will be made to the remote nodes as the domain user account that is executing the Rundeck server process.

### Username and Password

If all hosts are not in a trusted domain, both username and password are required to access the remote hosts.

## Plugin Configuration

Trusted Domain authentication will be used by default, unless a username and password are configured to be used.

You can configure the plugins to use a password via the Key Storage facility when accessing remote hosts.

- password storage - using a password that is stored in the Key Storage facility.

You can configure the username and password or password storage path at a project-wide level, on a per-node basis or upon job execution.

To pass the credentials upon job execution, it is required for the job to have the following job options:

- username: to override the username defined in Project or Node settings.
- winrmpassword: to overrise the password defined in the Project or Node settings. This should be using 'Secure 'Input Type.

### Password Storage

Passwords can be stored securely in the Runbook Automation Keystore facility. These passwords can be stored in a tree like structure to help you organize them any way you wish. The passwords can be referenced using an attribute named "password-storage-path". When Rundeck needs the password, it looks up the file as referenced by the storage path, reads, decrypts, and passes the value to the plugins.

## Node Configuration

Each host is configurable via "nodes" in the project resource model. Nodes are defined in terms of attributes.

Attributes

- hostname: The hostname of the remote node accessible to the Rundeck server host.
- username: The login account name to the remote host.
- password-storage-path: The path to the file containing the password in the keystore. This path will start with "keys/".
- connectionUri: Alternate connection parameters as a URI. e.g. "https://hostname:port"
- output-charset: The character encoding used for outputs of the node. Necessary in very specific cases where the output of commands is not printed correctly using the default charset. Default: 'utf-8'

### Example resource model definitions

The following example show a node defined using the XML format.

**Note the password-storage-path attribute referencing the key path.**

<div class="language-xml line-numbers-mode">

``` xml
 <node name="winhost123"
       hostname="xxx.xxx.xxx.xxx"
       username="myaccount"
       password-storage-path="keys/winhost123.passwd" 
       output-charset: 'utf-8'.../>
```

</div>

## Project Configuration

The Password storage path can be configured at the project level. In the Project Configuration page, set the Password Storage Path to a key path. The path can contain references to information from the node or user who is executing the command, for example:

<div class="language-text line-numbers-mode">

``` text
keys/nodes/${node.name}.password
```

</div>

or

<div class="language-text line-numbers-mode">

``` text
keys/users/${job.username}.password
```

</div>

## WinRM Setting to use WinRM Node Executor Plugin

In order to connect Rundeck with remote Windows nodes, it is necessary to set WinRM in both, the server and the remote nodes.

### On the rundeck server

<div class="language-text line-numbers-mode">

``` text
winrm quickconfig
winrm set winrm/config/client @{TrustedHosts="*"}
```

</div>

### On the remote nodes

<div class="language-text line-numbers-mode">

``` text
winrm quickconfig
âwinrm set winrm/config/service/Auth @{Basic="true"}
winrm set winrm/config/service @{AllowUnencrypted="true"}
winrm set winrm/config/winrs @{MaxMemoryPerShellMB="1024"}
```

</div>

### Other setting

To enable the execution of remote command:

<div class="language-powershell line-numbers-mode">

``` powershell
Set-ExecutionPolicy RemoteSigned
```

</div>

To enable permission to a user to execute remote command:

<div class="language-powershell line-numbers-mode">

``` powershell
Set-PSSessionConfiguration -ShowSecurityDescriptorUI -Name Microsoft.PowerShell
```

</div>

Increase the concurrent shell issue:

<div class="language-powershell line-numbers-mode">

``` powershell
set-item wsman:\localhost\shell\maxshellsperuser 50
```

</div>

## Enable CredSSP Authentication On Windows Domain

### On the Rundeck server

#### Enable CredSSP

Open a powershell windows and run:

<div class="language-powershell line-numbers-mode">

``` powershell
Enable-WSManCredSSP -Role "Client" -DelegateComputer "*.something.com"
```

</div>

Where `something.com` is the DNS domain of the target computer

or

<div class="language-powershell line-numbers-mode">

``` powershell
Enable-WSManCredSSP -Role "Client" -DelegateComputer "*"
```

</div>

To enable unencrypted access for the purpose of establishing a connection, run this command on both the Rundeck server and the remote nodes:

<div class="language-text line-numbers-mode">

``` text
winrm/config/service @{AllowUnencrypted="true"}
```

</div>

#### Allow Delegating Fresh Credentials

- Click **Start**, type **mmc** and then click **OK**.
- Click **File** and then click **Add/Remove Snap-in**.
- Click **Group Policy Object** and then click **Add**.
- Select **Local Computer** and then click **Finish**.
- Go to **Computer Policy\Administrative Templates\System\Credentials Delegation\Allow Delegating Fresh Credentials** â†’ Set to **enabled**

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/allow-delegating-fresh-credentials-1.png" alt="Enable delegating fresh credentials" />
<figcaption aria-hidden="true">Enable delegating fresh credentials</figcaption>
</figure>

- Add **WSMAN/\*** to list of computers and check the box for **Concatenate OS defaults with input above**.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/allow-delegating-fresh-credentials-2.png" alt="Add servers to list" />
<figcaption aria-hidden="true">Add servers to list</figcaption>
</figure>

#### Enable CredSSP authentication on Winrm Client

Open a CMD Prompt as an Administrator user and execute:

<div class="language-text line-numbers-mode">

``` text
winrm set winrm/config/client/auth @{CredSSP="true"}
```

</div>

You need to have winrm service configured and running.

### On the remote node

#### Enable CredSSP

Open a powershell windows and run:

<div class="language-powershell line-numbers-mode">

``` powershell
Enable-WSManCredSSP -Role "Server"
```

</div>

#### Make sure that you enable the CredSSP on WinRM Service settings

To get the WinRm Service config:

<div class="language-text line-numbers-mode">

``` text
winrm get winrm/config/service
```

</div>

To enable the CredSSP:

<div class="language-text line-numbers-mode">

``` text
winrm set winrm/config/service/auth @{CredSSP="true"}
```

</div>

To enable unencrypted access for the purpose of establishing a connection, run this command on the Rundeck server and the remote nodes:

<div class="language-text line-numbers-mode">

``` text
winrm/config/service @{AllowUnencrypted="true"}
```

</div>

### Troubleshooting

#### Using non-administrator user

If you are using a non-administrator user (or a not- domain-administrator user) to execute command to remote nodes, you need to set up the access on the remote machine ( to the user or some of its groups, eg: Domain User group).

To add permissions to non-administrator user to execute remote commands:

<div class="language-powershell line-numbers-mode">

``` powershell
Set-PSSessionConfiguration Microsoft.Powershell -ShowSecurityDescriptorUI
```

</div>

#### Access is denied error

If you get "Access is denied" error when you try to access to a shared folder on the remote node, it is possible that you must use the [CredSSP Authentication](#enable-credssp-authentication-on-windows-domain).

Then, you can define the authentication type like:

<div class="language-xml line-numbers-mode">

``` xml
<node name="XXXXX"
      description="Windows Server 2012"
      tags="Win2012"
      hostname="XXXXX"
      osArch="amd64"
      osFamily="windows"
      osName="Windows Server 2012"
      osVersion="6.3"
      username="rundeckuser@Domain.Local" password-storage-path="keys/xxxxx"
      ps-authentication-type="CredSSP" />
```

</div>

If you get this error, you have to change the network category:

<div class="language-text line-numbers-mode">

``` text
WinRM service is already running on this machine.

WSManFault
   Message
       ProviderFault
           WSManFault
               Message = WinRM firewall exception will not work since one of the network connection types on this machine is set to Public. Change the network connection type to either Domain or Private and try again.
Error number:  -2144108183 0x80338169

WinRM firewall exception will not work since one of the network connection types on this machine is set to Public. Change the network connection type to either Domain or Private and try again.
```

</div>

Workaround using PowerShell as Administrator User:

<div class="language-powershell line-numbers-mode">

``` powershell
# (to get the InterfaceIndex)
Get-NetConnectionProfile

Set-NetConnectionProfile -InterfaceIndex [INTERFAZ_INDEX] -NetworkCategory Private
```

</div>

It could be necessary to change the userâ€™s log-on in tomcat service when the remote connection does not work:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/powershell-troubleshooting.png" alt="Tomcat settings" />
<figcaption aria-hidden="true">Tomcat settings</figcaption>
</figure>

For more information about installing and configuring Windows Remote Nodes, see [Windows Remote Nodes](https://docs.microsoft.com/en-us/windows/win32/winrm/installation-and-configuration-for-windows-remote-management#:~:text=To%20configure%20WinRM%20with%20default,command%20at%20a%20command%20prompt).

## Use utf-8 scripts

If you need to use UTF-8 scripts from an `unix` instance to a `windows` node, powershell is unable to identify correctly the encoding of UTF-8 files without bom. You can force the file to be UTF-8 with bom adding the `file-copier-add-utf8-bom` property to the node:

<div class="language-xml line-numbers-mode">

``` xml
<node
  name="windowsServer"
  description="Windows server node"
  tags="windows"
  osArch="x86_64"
  osFamily="windows"
  osName="Windows 10"
  osVersion="10"
  hostname="192.168.56.101:5985"
  file-copier-add-utf8-bom="true"
  />
```

</div>
