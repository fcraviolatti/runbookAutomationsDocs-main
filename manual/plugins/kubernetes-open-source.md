---
title: "Kubernetes Plugins for Rundeck Community"
source_url: https://docs.rundeck.com/docs/manual/plugins/kubernetes-open-source.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Kubernetes Plugins for Rundeck Community

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/kubernetes-icon.png" />
</figure>

Rundeck integrates with Kubernetes through a variety of plugins. By integrating Rundeck with Kubernetes, users can automate and provide self-service interfaces for operations in their Kubernetes Clusters.

> **Commercial Kubernetes Plugins**
>
> This document covers the plugins available in Rundeck Community (open source). If you are using one of the commercial Runbook Automation products, see documentation for the [**Commercial Kubernetes plugins**](https://docs.rundeck.com/docs/manual/plugins/kubernetes-plugins-overview.html).

## Open Source Kubernetes Plugins

**Available in Rundeck Open Source**

| Plugin Name                                                                                                                                                    | Plugin Type    | Description                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|--------------------------------------------------------------------------------|
| [**Create Deployment**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-deployment-plugins.html#kubernetes-deployment-create)      | Node Step      | Create a new deployment.                                                       |
| [**Delete Deployment**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-deployment-plugins.html#kubernetes-deployment-delete)      | Node Step      | Delete an existing deployment.                                                 |
| [**Deployment Status**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-deployment-plugins.html#kubernetes-deployment-status)      | Node Step      | Get the status of an existing deployment.                                      |
| [**Update Deployment**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-deployment-plugins.html#kubernetes-deployment-update)      | Node Step      | Update an existing deployment.                                                 |
| [**Waitfor Deployment**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-deployment-plugins.html#kubernetes-deployment-waitfor)    | Node Step      | Pause workflow until deployment is complete.                                   |
| [**Create Job**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-job-plugins.html#kubernetes-job-create)                           | Node Step      | Create a new Kubernetes job.                                                   |
| [**Delete Job**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-job-plugins.html#kubernetes-job-delete)                           | Node Step      | Delete an existing Kubernetes job.                                             |
| [**Re-run Job**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-job-plugins.html#kubernetes-job-re-run)                           | Node Step      | Re-runs an existing Kubernetes job.                                            |
| [**Waitfor Job**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-job-plugins.html#kubernetes-job-waitfor)                         | Node Step      | Pause workflow until Kubernetes job is complete.                               |
| [**Create Service**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-service-plugins.html#kubernetes-service-create)               | Node Step      | Create a new Kubernetes service.                                               |
| [**Update Service**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-service-plugins.html#kubernetes-service-update)               | Node Step      | Update an existing Kubernetes service.                                         |
| [**Delete Service**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-service-plugins.html#kubernetes-service-delete)               | Node Step      | Delete an existing Kubernetes service.                                         |
| [**Pods Node Source**](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/kubernetes.html)                                                   | Resource Model | Populates node inventory with Kubernetes pods.                                 |
| [**Create Pod**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-pod-plugins.html#kubernetes-pod-create)                           | Node Step      | Create a new Kubernetes pod.                                                   |
| [**Delete Pod**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-pod-plugins.html#kubernetes-pod-delete)                           | Node Step      | Delete an existing Kubernetes pod.                                             |
| [**Describe Pod**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-pod-plugins.html#kubernetes-pod-describe)                       | Node Step      | Describe a running Kubernetes pod.                                             |
| [**Execute Command**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-pod-plugins.html#kubernetes-pod-execute-command)             | Node Step      | Execute a command inside a container in a running pod.                         |
| [**Execute Script**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-pod-plugins.html#kubernetes-pod-execute-script)               | Node Step      | Execute a script inside a container in a running pod.                          |
| [**Pod Logs**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-pod-plugins.html#kubernetes-pod-logs)                               | Node Step      | View the logs of a running pod.                                                |
| [**Waitfor Pod**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-pod-plugins.html#kubernetes-pod-waitfor)                         | Node Step      | Pause workflow until pod is in "ready" state.                                  |
| [**Debug Pod**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-debug-plugins.html#kubernetes-debug-ephemeral-container)           | Node Step      | Debug a running container inside an existing pod using an ephemeral container. |
| [**Waitfor StatefulSet**](https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/kubernetes-statefulset-plugins.html#kubernetes-statefulset-waitfor) | Node Step      | Pause workflow until StatefulSet has been successfully deployed.               |

**Plugins available only in Commercial products**

> Note: All Open Source plugins also included.

| Plugin Name                                                                                                                      | Plugin Type                                                                       | Description                                                                                   |
|----------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| [**Amazon EKS Node Source**](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/aws-eks.html)                  | Node Source                                                                       | Imports Amazon Web Services EKS Clusters as Nodes.                                            |
| [**Azure AKS Node Source**](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/azure-aks.html)                 | Node Source                                                                       | Imports Azure AKS Clusters as Nodes.                                                          |
| [**Google Cloud GKE Node Source**](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/gcp-gke.html)            | Node Source                                                                       | Imports Google Cloud GKE Clusters as Nodes.                                                   |
| [**Kubernetes Cluster Create Object**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-create-object)     | Node Step                                                                         | This plugin creates an object of a selected kind within a Kubernetes cluster.                 |
| [**Kubernetes Cluster Delete Object**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-delete-object)     | Node Step                                                                         | This plugin deletes an object of a selected kind within a Kubernetes cluster.                 |
| [**Kubernetes Cluster Describe Object**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-describe-object) | Node Step                                                                         | This plugin describes an object of a selected kind within a Kubernetes cluster.               |
| [**Kubernetes Cluster List Objects**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-list-objects)       | Node Step                                                                         | This plugin lists objects of a selected kind within a Kubernetes cluster.                     |
| [**Kubernetes Cluster Object Logs**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-object-logs)         | This plugin allows you to view the logs of an object within a Kubernetes cluster. |                                                                                               |
| [**Kubernetes Cluster Run Command**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-run-command)         | Node Step                                                                         | This plugin allows you to execute a command in a pod within a Kubernetes cluster.             |
| [**Kubernetes Cluster Run Script**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-run-script)           | Node Step                                                                         | This plugin executes a script using a predefined container image within a Kubernetes cluster. |
| [**Kubernetes Cluster Update Object**](https://docs.rundeck.com/manual/jobs/job-plugins/node-steps/kubernetes-update-object)     | Node Step                                                                         | This plugin updates a specified object of a selected kind within a Kubernetes cluster.        |

  

> **Tips**
>
> Click above see the full list of plugins for Kubernetes.

### Set up the Open Source Kubernetes Plugins

#### Python Dependencies

In order to use the Open Source Kubernetes plugins listed in the Summary above, Python must be installed on the Runbook Automation cluster-members or on the [Enterprise Runner](https://docs.rundeck.com/docs/administration/runner/) - depending on where the connection to Kubernetes will originate. *(These steps are also needed for Commercial versions using the listed Open Source plugins.)*

The plugins will work with both **Python 2.7.x** and **Python 3.x.x**.

Once python is installed, download and install the **`kubernetes`** python client. For **Python 2.7.x** this can be done with **`pip install kubernetes`** and for **Python 3.x.x** this can be done with **`pip3 install kubernetes`**.

Optionally test that the Kubernetes client has been installed successfully by executing the following at the command-line: **`python`** followed by **`from kubernetes import client, config`**:

<div class="language-text line-numbers-mode">

``` text
ubuntu@ip-172-31-13-91:~$ python
Python 2.7.17 (default, Mar  8 2023, 18:40:28) 
[GCC 7.5.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> from kubernetes import client, config
>>>
```

</div>

#### Kubernetes Authentication for Open Source Plugins

By default, the Kubernetes plugins look for a Kube Config file at **`$RDECK_BASE/.kube/config`**. For **Deb** and **RPM** this would translate to **`/var/lib/rundeck/.kube/config`**. The Kube Config file can be saved to a different location, just be sure to take note of where it is saved for later steps.

If it is preferred to use a Kubernetes API Token, then follow the instructions outlined [here](https://www.cncf.io/blog/2020/07/31/kubernetes-rbac-101-authentication/) to generate the Service Account Token. Once created, save the Token to [Key Storage](https://docs.rundeck.com/docs/manual/system-configs.html#key-storage) as a **Password** secret type.

#### Upload Kubernetes Plugins (Rundeck OSS Only)

Rundeck OSS does not come preloaded with the Kubernetes plugins. To install the Kubernetes plugins, use the following steps:

1.  Navigate to the [latest plugin release](https://github.com/rundeck-plugins/kubernetes/releases/latest) on Github and download the **`kubernetes-X.X.XX.zip`** file.  
      
2.  In Rundeck, click the **Gear Icon** and then click the **Plugins \> Upload Plugin**: ![Upload Plugins Menu](https://docs.rundeck.com/docs/assets/img/upload-plugins-menu.png)
3.  Click **Browse** and select the downloaded **`.zip`** file from Step 2.
4.  Click **Install**: ![Upload Kubernetes Plugins](https://docs.rundeck.com/docs/assets/img/upload-k8s-plugins.png)

### Test Open Source Kubernetes Plugins

To test that the dependencies and authentication have been configured correctly, use a Kubernetes Node Step plugin - as this will provide the option to easily execute the plugin in *debug* mode.

1.  Create a new Job.
2.  Navigate to the **Workflow** tab.
3.  Click **+ Add a step**.
4.  In the **Search step** field type **`Kubernetes`**.
5.  Select the **Kubernetes / Pod / Describe** plugin from the list.
6.  Type in a pod name into the **Name** field. ![K8s Describe Pod](https://docs.rundeck.com/docs/assets/img/k8s-describe-pod.png)
7.  Type in the namespace of the pod in the **Namespace** field.
8.  If the Kube Config file is saved in the directory **`$RDECK_BASE/.kube/config`** (`/var/lib/rundeck/.kube/config`for RPM and Deb), then the authentication fields can be left blank.
    - Otherwise, specify the custom Kube Config location.
9.  Optionally chance the **Python Interpreter** if python scripts are not invoked using `python my_script.py` but rather `python2 my_script.py` or `python3 my_script.py`.
10. Click **Save** on the Job Step and then **Save** to save the Job.
11. Click **Run Job Now** to test that the configuration is correct.

Now that configuration is complete, take a look at use-cases for Runbook Automation with Kubernetes such as [Capturing Debug Data from Apps in Kubernetes](https://docs.rundeck.com/learning/solutions/automated-diagnostics/examples/k8s-app-debug-capture) or [Managing Kubernetes with Rundeck](https://docs.rundeck.com/docs/learning/howto/how2kube.html#managing-kubernetes-with-rundeck).
