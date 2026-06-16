---
title: "Connect to Windows Nodes with PyWinRM"
source_url: https://docs.rundeck.com/docs/learning/howto/configuring-windows-nodes.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Connect to Windows Nodes with PyWinRM

Rundeck allows users to execute jobs to remote Windows nodes to manage and automate tasks using Rundeck workflows. This article shows how to add a Windows node and execute Rundeck jobs and commands with windows-based systems.

To communicate with Windows nodes, Rundeck uses an out-of-the-box [Node Execution/ File Copier plugin](https://github.com/rundeck-plugins/py-winrm-plugin) that uses the [WinRM](https://docs.microsoft.com/en-us/windows/win32/winrm/portal) (Windows Remote Management) protocol.

> Note: If this is the first time adding remote nodes, we suggest reviewing the [Rundeck Tutorial](https://docs.rundeck.com/docs/learning/tutorial/) before adding Windows nodes. This exercise assumes some experience with Windows and Rundeck basics covered in the Tutorial.

## Basic pywinrm Plugin Requirements

The [pywinrm plugin](https://github.com/rundeck-plugins/py-winrm-plugin) needs the following requirements on the Rundeck server to work properly. It is supported on Rundeck running on Linux, Mac OS X, or Windows operating systems.

### Requirements:

> **Tips**
>
> Make sure that your python installation is same that the one that is exported in your "PATH" environment variable, so the PyWinRm plugin can access its packages.
>
> - We recommend this commands to check the python installation:
>
> <div class="language-text line-numbers-mode">
>
> ``` text
> # Windows OS
> where python - "example/path/to/python"
> # linux OS
> which python - "example/path/to/python"
> ```
>
> </div>
>
> **The path to the executable must be the same if we dispatch the command to the required node with the AD-HOC command functionality.**

The [pywinrm plugin](https://github.com/rundeck-plugins/py-winrm-plugin) uses the python [WinRM Library](https://github.com/diyan/pywinrm/) to provide the WinRM implementation.

- Python 3.3-3.5 or PyPy2 installed on Rundeck server. *(Python 3 strongly recommended)*
- Pywinrm library (It can be installed with the following command: `pip install pywinrm`)
- OpenSSL version 1.1.1 or higher. (openssl version can be checked with the following command: `openssl version - "OpenSSL 1.1.1k"`)
  - `requests-kerberos` and `requests-credssp` are optional.

Note: Due to networking complexity issues this exercise will not work with the Welcome Projects. These steps assume you have Rundeck installed [using these instructions](https://docs.rundeck.com/docs/administration/install/). For more information see the [Additional Information](#additional-information) section.

## Basic Windows Requirements

To follow this How to Guide, your Windows system needs the following requirements:

- A Windows node in the same network as the Rundeck instance
- Windows Server 2008 R2 or above
- PowerShell 2.0 or above

## Windows Configuration

The first step is to configure the Windows machine. To do this, go to the Windows instance and follow the these steps:

1.  Open a PowerShell terminal as an admin user profile.
2.  Enable the WinRM protocol on Windows:
    <div class="language-text line-numbers-mode">

    ``` text
    winrm qc
    ```

    </div>
3.  Define the authentication type:
    <div class="language-text line-numbers-mode">

    ``` text
    winrm set winrm/config/service/Auth '@{Basic="true"}'
    ```

    </div>
4.  Define the client authentication type:
    <div class="language-text line-numbers-mode">

    ``` text
    winrm set winrm/config/client/Auth '@{Basic="true"}'
    ```

    </div>
5.  Allow unencrypted SOAP messages:
    <div class="language-text line-numbers-mode">

    ``` text
    winrm set winrm/config/service '@{AllowUnencrypted="true"}'
    ```

    </div>

> **Warning**
>
> It's important to allow access to the 5985 port via Windows Firewall (any between the Rundeck server and the node), to receive the remote requests.

> Note: These settings are for Exercise purposes only and do not represent the most secure method of implementing. Please follow your own security guidelines for production implementations.

## Rundeck Configuration

Create a Windows-based project on the Rundeck instance.

1.  Create a new project: **Name** `windows`, and **Label` Windows Jobs`**  
      
    ![Create Project](https://docs.rundeck.com/docs/assets/img/howto-winnode-createproject.png)  
      
2.  Go to the Default Node Executor tab and then select **WinRM Node Executor Python**. It may be necessary to set the Python interpreter textbox to `python3` interpreter as the command/path.  
      
    ![Node Executor](https://docs.rundeck.com/docs/assets/img/howto-winnode-nodeexec.png)  
      
3.  Go to the **Default File Copier** tab and select the **WinRM Python File Copier**. Similar to the previous step, it may be necessary to define the Python interpreter textbox as `python3` interpreter for the command/path.  
      
    ![File Copier](https://docs.rundeck.com/docs/assets/img/howto-winnode-filecopy.png)  
      
4.  Click on the **Create** button.

### Additional Configuration

The following properties can optionally be set in the WinRM Node Executor and WinRM File Copier:

- **`No SSL Verification`**: When this is set to `true`, SSL is not validated in the WinRM communication. This can be overridden on nodes with `winrm-nossl`.  
    
  - **`Disable TLS 1.2`**: Check this box to execute over TLS 1.0  
      

- **`WinRM Transport Protocol`**: Optionally choose HTTP or HTTPS for the WinRM transport protocol. This can be overridden on nodes with `winrm-transport`.  
    

- **`WinRM Port`**: The WinRM port to use. The default is port 5985. This can be overridden on nodes with `winrm-port`.  
    

- **`WinRM Username`**: Optional username. The username can be set at node level (using the attribute `username`) or at job level (using an input option called `username`).  
    

- **`Certificate Path`**: The path for SSL verification. This can be overridden on nodes with `winrm-certpath`.  
    

  > **Important**
  >
  > `winrm-certpath` expects a **file system path** (e.g., `/opt/rundeck/certs/certificate.pem`), **NOT** a Rundeck Key Storage path (e.g., `keys/project/...`). The certificate path is passed directly to the pywinrm library without Key Storage resolution. The certificate file must be in PEM format and readable by the Rundeck user on the Enterprise Runner or Rundeck server.

- **`Connect/Read Times Out`**: The maximum seconds to wait before an HTTP connect/read times out (default 30). This value should be slightly higher than operation timeout, as the server can block *at least* that long. This can be overridden on nodes with `winrm-readtimeout`.  
    

- **`Proxy`**: Optionally specify a proxy address for communicating with Windows nodes. Example HTTP proxy strings are `http://server:port` and `http://user:pass@server:port`. An example SOCKS5 proxy string is `socks5://user:pass@server:port`.  
    

- **`Operation Timeout`**: The maximum allowed time in seconds for any single wsman HTTP operation (default 20). Note that operation timeouts while receiving output will be silently retried indefinitely. This can be overridden on nodes with `winrm-operationtimeout`.  
    

- **`Shell`**: The Windows shell interpreter. Options include `cmd` and `powershell`. This can be overridden on nodes `winrm-shell`.  
    

- **`Script Exit Behavior`**: Script Exit Behaviour. Options include:
  - `console` (default): if the std-error console has data, the process fails.
  - `exitcode`: script won't fail by default, the user must control the exit code, such as by using a try/catch block. See [this link](https://github.com/rundeck-plugins/py-winrm-plugin/tree/master#running-scripts) for more details.  
      

- **`Retry connection`**: Retry the connection to the node if the connection fails. This can be overridden on nodes with `winrm-retry-connection`.  
    

- **`Retry Connection Delay`**: Delay in seconds between each retry attempt. This can be overridden on nodes with `winrm-retry-connection-delay`.  
    

- **`krb5 Config File`**: Path to a `krb5.conf` file, either on the Runbook Automation server or Enterprise Runner's host.  
    
  - **`Kerberos Delegations`**: If True, TGT is sent to target server to allow multiple hops.  
      

- **`Clean Escaping`**: Cleans unnecessarily Escaped characters on commands.  
    

## Adding a Windows Test Node

Now Rundeck should ask about the model source. Let's start with the Windows node definition.

Enterprise Steps

Community Steps

Enterprise Steps

1.  Click on the **Add a new Node Source +** button.
2.  Select **Node Wizard**.  
      
    ![Node Wizard](https://docs.rundeck.com/docs/assets/img/howto-winnode-nodewizardsource.png)  
      
3.  Click **Save** on the *Node Wizard Source*.
4.  Click **Save** on the *Sources* tab.
5.  Switch to the *Edit* tab.
6.  Click the Modify button under the Node Wizard entry.  
      
    ![Modify Wizard](https://docs.rundeck.com/docs/assets/img/howto-winnode-modifynodesource.png)  
      
7.  Set the *Node Name* to `mywindows`
8.  Set *HostName* to the IP address of your Windows Host.
9.  Set *OS Family* to `Windows`  
      
    ![Wizard Detail](https://docs.rundeck.com/docs/assets/img/howto-winnode-wizarddetail.png)  
      
10. Click the **Authentication Tab** at the top.
11. Enter your user name for the *UserName*. (e.g. *Administrator*)  
      
    ![Wizard Authentication](https://docs.rundeck.com/docs/assets/img/howto-winnode-wizardauth.png)  
      
12. Set the *Password Storage Path* to `keys/project/windows/windows.password`
13. Click **Add Node** to save that node entry.
14. Click the **Save** button under the list of nodes.

Community Steps

1.  Click on the **Add a new Node Source +** button.
2.  Select **File**  
      
    ![File Source Logo](https://docs.rundeck.com/docs/assets/img/howto-winnode-filesource.png)  
      
3.  In the *Format* section, click on the right list and select the **resourceyaml** option.
4.  Put the file's desired path including the file name and extension. (e.g. `~/windows-nodes.yaml`)
5.  Select check boxes for **Generate**, **Include Server Node** and **Writeable** checkboxes, and then click on the **Save** buttons (*there are two*).  
      
    ![File Source Details](https://docs.rundeck.com/docs/assets/img/howto-winnode-filesourcedetails.png)  
      
6.  Now click on the *Edit* tab, and click on the **Modify** button.  
      
    ![File Source Code](https://docs.rundeck.com/docs/assets/img/howto-winnode-modifyfilesource.png)  
      
7.  Add the following node definition in the node definition text area. Make sure you use your own nodes IP Address for *hostname* and login name for *username*
    <div class="language-text line-numbers-mode">

    ``` text
    mywindows:
      description: Windows Server.
      tags: windows
      hostname: 192.168.1.10
      osArch: amd64
      osFamily: windows
      username: Administrator
      winrm-password-storage-path: "keys/windows.password"
    ```

    </div>
8.  \*\*Save the entry.  
    The node is available now by clicking on the "Nodes" section in the left sidebar and setting the filter to `.*`

Don't forget to add the Windows user password to the Rundeck key storage.

1.  Go to the *System Menu(Gear Icon) \> Key Storage*.  
      
    ![Key Storage](https://docs.rundeck.com/docs/assets/img/howto-winnode-keystorage.png)  
      
2.  Click on the **+ Add or Upload a Key** button.
3.  Enter the Windows password as shown in the image and save.  
      
    ![Key Storage Entry](https://docs.rundeck.com/docs/assets/img/howto-winnode-keystorageentry.png)  
      

> Enterprise Users may need to add `project/windows` to the Storage Path line.

### Testing the New Windows Remote Node

Now it's time to send some commands against the windows remote machine.

1.  Click on the **Commands** section on the left sidebar.
2.  On the **Nodes** section use a filter to dispatch only to the Windows machine, type:
    <div class="language-text line-numbers-mode">

    ``` text
    name: mywindows
    ```

    </div>
3.  On the *Enter a command* textbox type: `dir` (listing directories and files).
4.  Click on the **Run on 1 Node** button.  
      
    ![Success](https://docs.rundeck.com/docs/assets/img/howto-winnode-commandsuccess.png)  
      

And now your Windows node is ready to receive PowerShell commands from the Rundeck instance.

## Additional Information

Using Linux? Read the [Using SSH on Linux/Unix Nodes](https://docs.rundeck.com/docs/learning/howto/ssh-on-linux-nodes.html) article to learn more.

### Networking Issues

Docker Desktop has some limitations to how it handles networking. [Check out this information](https://docs.rundeck.com/docs/learning/howto/connect-local-nodes.html) about how to get the Rundeck Welcome Projects to connect to a single host on your local network.
