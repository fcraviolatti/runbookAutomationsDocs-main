---
title: "Use SSH on Linux/Unix Nodes"
source_url: https://docs.rundeck.com/docs/learning/howto/ssh-on-linux-nodes.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Use SSH on Linux/Unix Nodes

Rundeck allows users to dispatch jobs to remote Linux/UNIX servers to manage and automate any task using Rundeck workflows. The most common protocol for connecting to Linux/Unix servers is SSH. This is an example of how to add a remote node and configure Rundeck to use SSH to connect to it.

*Note: If this is the first time adding remote nodes. It is suggested to review the [Rundeck Tutorial](https://docs.rundeck.com/docs/learning/tutorial/) before adding remote SSH nodes. This exercise assumes some experience with Linux, SSH Keys, and Rundeck basics covered in the Tutorial.*

> **Warning**
>
> This documentation is for use with the [Welcome Projects](https://docs.rundeck.com/docs/learning/) on non-production instances. It is strongly recommended to follow best practices when generating, managing and configuring SSH keys and access. For detailed configuration of SSH use [this documentation](https://docs.rundeck.com/docs/manual/projects/node-execution/ssh.html).

## Configuring Rundeck

Rundeck can store the authentication keys necessary to authenticate to our Linux example host in Rundeckâ€™s built-in Key Storage.

1.  Click on the System Menu (gear icon) and choose **Key Storage**. ![Key Storage Menu](https://docs.rundeck.com/docs/assets/img/howto-ssh-keystoragemenu.png)
2.  Click on the **Add or Upload a Key** button to create a **New entry** in the Rundeck Key Storage. ![Add Key Entry](https://docs.rundeck.com/docs/assets/img/howto-ssh-addkey.png)
3.  For *Key Type* select `Private Key`.
4.  Add Rundeck instance private key file content in *Enter text*. The key is located at `/var/lib/rundeck/.ssh/id_rsa`.
5.  In the **Storage path** field itâ€™s possible to define specific subfolders for the keys if needed, for this example just leave it blank.
6.  In the *Name* textbox enter a key name that corresponds to the Rundeck host, in this example is just `rundeck` (now the Key Storage entry is `keys/rundeck`). ![Key Entry](https://docs.rundeck.com/docs/assets/img/howto-ssh-keyentry.png)

## Adding Nodes

Now, itâ€™s time to add the remote node.

Enterprise Exercise

Community Exercise

Enterprise Exercise

Included in Enterprise is the Node Wizard Node Source. Use that to add a new node by following these steps:

1.  Click **Project Settings \| Edit Nodes**  
    ![Key Entry](https://docs.rundeck.com/docs/assets/img/howto-ssh-editnodes.png)
2.  Click the Modify button under the Node Wizard entry.  
    ![Modify Button](https://docs.rundeck.com/docs/assets/img/howto-ssh-modifynodesource.png)
3.  Click + Add Node.  
    ![Add Node](https://docs.rundeck.com/docs/assets/img/howto-ssh-addnode.png)
4.  Set the *Node Name* to `node1`
5.  Set *HostName* to `node1`
6.  Set *OS Family* to `Unix`  
    ![Wizard Entry](https://docs.rundeck.com/docs/assets/img/howto-ssh-nodeewizardentry.png)
7.  Click the **Authentication Tab** at the top.
8.  Enter `agent` for the *UserName*.  
      
    ![Authentication Tab](https://docs.rundeck.com/docs/assets/img/howto-ssh-wizardauthtab.png)
9.  Click **Add Node** to save that node entry.
10. Click the **Save** button under the list of nodes.  
    ![Save Node Wizard](https://docs.rundeck.com/docs/assets/img/howto-ssh-savenodewizard.png)

Community Exercise

Rundeck Community

1.  Click **Project Settings \| Edit Nodes**![Key Entry](https://docs.rundeck.com/docs/assets/img/howto-ssh-editnodes.png)
2.  Click on the **Add new Node Source** button.  
    ![Add Node Source](https://docs.rundeck.com/docs/assets/img/howto-ssh-addnodesource.png)
3.  There will be a list of options, select the **File** Node Source.  
    ![File Node Source](https://docs.rundeck.com/docs/assets/img/howto-ssh-filenodesource.png)
4.  In the drop-down menu on the right, select **resourceyaml**.
5.  In *File Path* choose a path reachable by the Rundeck user - e.g: in the `/var/lib/rundeck/resources.yml` directory. *Itâ€™s important to leave the filename at the end, otherwise, it will not be created.*
6.  Next, check **Generate**, **Include Server Node** and **Writeable**.  
    ![alt_text](https://docs.rundeck.com/docs/assets/img/howto-ssh-filenodesource-filled.png)
7.  Finally, click on the **Save** button. The file will be added to the server and ready for a node entry.

Once created, the file can be edited by clicking on the "Modify" button (Edit tab) where we can add an extra entry corresponding to our remote SSH server.

Use the following `resources.yaml` file content:

<div class="language-text line-numbers-mode">

``` text
remote-node:
  description: Remote SSH server node
  hostname: node1
  nodename: node1
  osArch: amd64
  osFamily: unix
  osName: Linux
  osVersion: 5.11.0-7612-generic
  tags: 'node1'
  username: agent
  ssh-key-storage-path: keys/rundeck
```

</div>

In the *hostname* attribute, place the DNS name of our remote node. In *username* the user who is trying to access the SSH server, In *ssh-key-storage-path* specifies the path that was created in key storage earlier.

## Running Commands on Nodes

**Letâ€™s dispatch some commands!**

1.  Clicking on the "Nodes" tab (left menu) and using the drop-down to choose *Select All Nodes* will display all the nodes that have been configured. The screenshot below shows the listing with 2 nodes (the Rundeck node and the node added recently).  
    ![Two Nodes Shown](https://docs.rundeck.com/docs/assets/img/howto-ssh-dispatch1.png)
2.  To select the node created earlier, put the name in *Nodes* textbox; In this case, `node1` and press Enter key, now the node is selected.  
    ![Filter for one node](https://docs.rundeck.com/docs/assets/img/howto-ssh-dispatch2.png)
3.  In the *Enter a command* textbox put a command, e.g.: `df`, and click on the **Run on 1 Node** green button.  
    ![Command Output](https://docs.rundeck.com/docs/assets/img/howto-ssh-dispatch3.png)

**Congratulations!** A remote SSH node to dispatch commands and jobs is setup in Rundeck. Stay tuned to the next blog entry where we build a job to execute on this Node.

## Additional Resources

[ssh-keygen command documentation](https://linux.die.net/man/1/ssh-keygen)
