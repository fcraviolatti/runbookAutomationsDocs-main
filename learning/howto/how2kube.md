---
title: "Manage Kubernetes with Rundeck"
source_url: https://docs.rundeck.com/docs/learning/howto/how2kube.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Manage Kubernetes with Rundeck

[Kubernetes](https://kubernetes.io/) (K8s) is an open-source platform for managing containerized services. It is used in many environments, but particularly as part of cloud-native applications where it is important to be able to scale up and down at will. The architecture makes scaling and recycling container based services easy.

Kubernetes services, support, and tools are widely available and very customizable and can be used in two different ways in the context of Rundeck. K8s can be used to automate the build and management of Rundeck as a container. For the purposes of this article, weâ€™ll be focused on the more common way to use Kubernetes and Rundeck together, managing a complete Kubernetes cluster environment.

The article is written assuming use of Rundeck Community, our open-source offering, but can also be done using the commercial version, [PagerDuty Runbook Automation](https://www.pagerduty.com/platform/automation/process-software/).

## Kubernetes and Rundeck

Rundeck uses the [Kubernetes workflow step plugin](https://github.com/rundeck-plugins/kubernetes) to manage K8s. In this guide, we explain how to configure the plugin, how to manage pods as nodes, and how to use the workflow steps to interact with Kubernetes components.

## Prerequisites for This Tutorial

1.  **Minikube as a local Kubernetes cluster**  
    Minikube is a local Kubernetes implementation and itâ€™s an easy way to learn Kubernetes using any computer.  
    To install Minikube on Linux, download and copy the binary to`/usr/local/bin/` path with the correct permissions:  
    <div class="language-text line-numbers-mode">

    ``` text
    $ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    $ sudo install minikube-linux-amd64 /usr/local/bin/minikube
    ```

    </div>

    Click [here](https://minikube.sigs.k8s.io/docs/start/) to learn more about the minikube installation. Minikube can be configured using a specific driver (such as docker, VirtualBox, qemu, etc.). An easy way to get started is to run using Virtualbox on a local machine. After [installing Virtualbox](https://itsfoss.com/install-virtualbox-ubuntu/), you can launch minikube in the following way:  
    <div class="language-text line-numbers-mode">

    ``` text
    minikube start --driver=virtualbox
    ```

    </div>
2.  Kubectl to interact with minikube  
    Kubectl is a command-line tool for interacting with minikube. Click [here](https://kubernetes.io/docs/tasks/tools/#kubectl) to learn how to install Kubectl  
3.  K9s for cluster monitoring (optional)  
    K9s is a tool focused on monitoring and interacting with the cluster. Click [here](https://k9scli.io/topics/install/) to learn how to install K9s  
4.  Rundeck  

## Kubernetes Rundeck Plugin Prerequisites

1.  Python3  
2.  Kubernetes pip module  
    Can be installed with  
    <div class="language-text line-numbers-mode">

    ``` text
    pip3 install kubernetes
    ```

    </div>

## Installing the Kubernetes Plugin in Rundeck

1.  Go to the System Menu \> Plugins \> Upload plugin  
    ![](https://docs.rundeck.com/docs/assets/img/kube1.png)  
2.  Put in the latest version .zip file full URL path here.  
    ![](https://docs.rundeck.com/docs/assets/img/kube2.png)  
3.  Click on the "install" button.  

## Kubernetes Model Source

To manage K8s pods as nodes, it's necessary to add the Kubernetes model source.  

1.  Go to Project Settings \> Edit Nodes  
    ![](https://docs.rundeck.com/docs/assets/img/kube3.png)  

2.  Click on the â€œAdd a new Node Source +" button.  
    ![](https://docs.rundeck.com/docs/assets/img/kube4.png)  

3.  From the list select "Kubernetes / Pods / Resource model"  

4.  Save  
    ![](https://docs.rundeck.com/docs/assets/img/kube5.png)  

    > **Tips**
    >
    > By default and if authentication parameters are not set, the plugin will check the file `~/.kube/config` to get the authentication parameters.  
    > Otherwise, you can set the following parameters:  
    >
    > - **Kubernetes Config File Path**: a custom path for the Kubernetes config file  
    > - **Cluster URL**: Kubernetes Cluster URL  
    > - **Kubernetes API Token**: Token to connect to the Kubernetes API  
    > - **Verify SSL**: Enable/disable the SSL verification  
    > - **SSL Certificate Path**: SSL certificate path for SSL connections  

5.  Create a file named `deployment.yaml` with the following content:  
    <div class="language-text line-numbers-mode">

    ``` text
    apiVersion: apps/v1
    kind: Deployment
    metadata:
     name: nginx-deployment
     labels:
       app: nginx
    spec:
     replicas: 1
     selector:
       matchLabels:
         app: nginx
    template:
      metadata:
        labels:
          app: nginx
      spec:
        containers:
        - name: nginx
          image: nginx:1.15.4
          ports:
          - containerPort: 80
    ```

    </div>

6.  Deploy the test deployment with the following command:  
    <div class="language-text line-numbers-mode">

    ``` text
    kubectl apply -f ./deployment.yaml
    ```

    </div>

7.  Check if the deployment is running with k9s (just run the `k9s` command).  
    ![](https://docs.rundeck.com/docs/assets/img/kube6.png)  

8.  Go back to Rundeck and refresh the Rundeck model source  
    ![](https://docs.rundeck.com/docs/assets/img/kube7.png)  

9.  Now go to the Commands section and select the Kubernetes pod in the node filter and put any command.  
    ![](https://docs.rundeck.com/docs/assets/img/kube8.png)  

## Kubernetes Workflow Steps 

Next, weâ€™ll simulate a simple deployment using the `Kubernetes / Generic / Create` workflow step, carrying out a MySQL database deployment:  

1.  Create a new Job and give it a name.  
2.  Select the first Kubernetes step: `Kubernetes / Generic / Create`.  
    ![](https://docs.rundeck.com/docs/assets/img/kube9.png)  
3.  Go to the "YAML String" textbox and add the following YAML content.  
    <div class="language-text line-numbers-mode">

    ``` text
    apiVersion: apps/v1
    kind: Deployment
     metadata:
         labels:
           app: mysql
       spec:
        containers:
        - image: mysqapiVersion: apps/v1
    kind: Deployment
    metadata:
     name: mysql
     labels:
       app: mysql
    spec:
     selector:
        matchLabels:
          app: mysql
     strategy:
      type: Recreate
     template:
    l:5.6
          name: mysql
          env:
          - name: MYSQL_ROOT_PASSWORD
          value: password
    ```

    </div>
4.  Save the job and run.  
    ![](https://docs.rundeck.com/docs/assets/img/kube10.png)  
5.  Run k9s to see that the new deployment is available on the minikube cluster:  
    ![](https://docs.rundeck.com/docs/assets/img/kube11.png)  
6.  The new deployment is added to the nodes section. Now it's possible to dispatch commands against the pods or create jobs against them.  
    ![](https://docs.rundeck.com/docs/assets/img/kube11.png)  

## Other Available Workflow Steps

The following plugins allow you to deploy/un-deploy applications and run/re-run jobs on Kubernetes. For example, you can create a deployment, services, ingress, etc., and update or delete those Kubernetes resources.  

1.  *Create / Update / Delete / Check / Wait a Deployment*  
    These steps manage Kubernetes Deployment resources. You can create, update or delete a deployment and check its status.  
2.  *Create / Update / Delete Services*  
    These steps manage Kubernetes Service resources. You can create, update or delete a service.  
3.  *Create / Delete / Re-run Jobs*  
    These steps manage Kubernetes Job resources. You can create or delete a Job.
