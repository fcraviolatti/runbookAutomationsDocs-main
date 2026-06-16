---
title: "Deploy Rundeck on AWS EKS"
source_url: https://docs.rundeck.com/docs/learning/howto/how2-terra-rd-eks.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Deploy Rundeck on AWS EKS

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/terra-eks1.png" />
</figure>

Amazon Elastic Kubernetes Service (Amazon EKS) is a fully-managed Kubernetes service that simplifies the process of building, securing, operating, and maintaining Kubernetes clusters on AWS. Amazon EKS automatically manages the Kubernetes nodes, containers, application availability and stored cluster data.  
Deploying Rundeck on EKS takes advantage of Kubernetes capabilities such as auto-scaling, portability and availability. This makes it a strong choice for cloud deployments. Consequently, itâ€™s common to see Rundeck implemented on Kubernetes clusters.  
This guide explains how to configure different tools that interact with the AWS EKS and how to deploy a basic Rundeck (or commercial Runbook Automation) deployment on an AWS EKS Cluster.  

## Requirements

### AWS

- A **valid AWS account** with sufficient access rights to create EKS clusters.  
- **AWS CLI**, a tool to interact with the AWS resources. Check the most recent version and instructions for installing it for your OS system [here](https://aws.amazon.com/cli/).  
- **K9S**, a tool for monitoring and interacting Kubernetes pods easily, recent version and installation instructions [here](https://k9scli.io/topics/install/).  

### Kubernetes

- **Kubectl**, the command line tool for working with Kubernetes clusters. Find installation instructions [here](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).  
- **EKS CTL**, the command line tool for working with EKS clusters that automates many individual tasks. Find installation instructions [here](https://docs.aws.amazon.com/en_us/eks/latest/userguide/eksctl.html).  
- **K9S**, for monitoring the EKS cluster. This is optional but useful. Learn how to install it on your operating system by visiting [this](https://k9scli.io/topics/install/) page.  

## Environmental Setup

### Configure the AWS CLI tool with the following command

<div class="language-text line-numbers-mode">

``` text
aws configure
```

</div>

When prompted, provide the AWS access and secret key.  

### Create the EKS cluster

EKS CLI is linked to AWS CLI. If AWS CLI was configured successfully in the previous step, create an EKS cluster with the following command.  

<div class="language-text line-numbers-mode">

``` text
eksctl create cluster --name oss-test-cluster --version 1.31 --region eu-north-1 --nodegroup-name test-workers --node-type t3.xlarge --nodes 3 --nodes-min 1 --nodes-max 4 --managed
```

</div>

Included parameters:  
`--name`: The cluster name.  
`--version`: The Kubernetes version. Where possible, use the latest version.  
`--region`: AWS region where the cluster is deployed. The example uses `eu-north-1` (Stockholm).  
`--nodegroup-name`: The node group name. One or more Amazon EC2 instances deployed in an Amazon EC2 Auto Scaling group are referred to as a node group.  
`--node-type`: C2 image type. It is crucial to pick a type with enough resources to run.  
`--nodes`: The number of worker nodes (node groups).  
`--nodes-mi`: Minimum number of workers (node groups).  
`--manage`: Creates managed nodes to use AWS EC2 instances-based nodes, managed nodes are provisioned Amazon EC2 machines that offer Auto Scaling capabilities that are managed by Amazon EKS.  

### Configure `kubectl` to interact with the AWS EKS cluster

#### Enter the following AWS CLI command:

<div class="language-text line-numbers-mode">

``` text
aws eks update-kubeconfig --region eu-north-1 --name oss-test-cluster
```

</div>

### Creating the Rundeck namespace

To avoid interfering with other services, best practice is to create a different namespace than the `default` namespace. This example used the `bangarang` namespace for the deployment.  

#### Create a `bangarang` namespace:

<div class="language-text line-numbers-mode">

``` text
kubectl create namespace bangarang
```

</div>

### Set the custom namespace as the default namespace

#### Set the `bangarang` namespace as the `kubectl` default:

<div class="language-text line-numbers-mode">

``` text
kubectl config set-context --current --namespace=bangarang
```

</div>

#### This should be reflected by `oss-test-cluster` (`bangarang` namespace) using `k9s`

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/terra-eks2.png" />
</figure>

## Deployment

### Deploying the Rundeck service

#### Create a text file named `rundeck-svc.yaml`:

<div class="language-text line-numbers-mode">

``` text
apiVersion: v1
kind: Service
metadata:
 name: rundeck-svc
 labels:
   env: dev
spec:
 type: LoadBalancer
 ports:
 - port: 4440
 selector:
   env: dev
```

</div>

#### Deploy the service using the .yaml file:

<div class="language-text line-numbers-mode">

``` text
kubectl apply -f rundeck-svc.yaml
```

</div>

#### Check service availability:

<div class="language-text line-numbers-mode">

``` text
kubectl get service
```

</div>

#### Result should look like this:

![](https://docs.rundeck.com/docs/assets/img/terra-eks3.png) Note: The "EXTERNAL-IP" column is the Service URL for the Rundeck deployment. Copy it for use in the next step.  

### Deploying Rundeck to EKS

#### Create a text file named `rundeck-deployment.yaml`:

<div class="language-text line-numbers-mode">

``` text
apiVersion: apps/v1
kind: Deployment
metadata:
 name: rundeck
 labels:
   env: dev
spec:
 replicas: 1
 selector:
   matchLabels:
     env: dev
 template:
   metadata:
     labels:
       env: dev
   spec:
     containers:
     - name: rundeck
       image: rundeck/rundeck:5.8.0
       env:
       - name: RUNDECK_GRAILS_URL
         value: "http://service_url:4440"
       ports:
       - containerPort: 4440
```

</div>

Note: `http://service_url:4440` is the URL taken from the service URL. Use this URL to access the Rundeck instance.  

#### Deploy Rundeck in the EKS:

<div class="language-text line-numbers-mode">

``` text
kubectl apply -f rundeck-deployment.yaml
```

</div>

The deployment should look as follows in `k9`:  
![](https://docs.rundeck.com/docs/assets/img/terra-eks4.png) Rundeck is available via the service's external URL.  

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/terra-eks5.png" />
</figure>

## Production Deployment with Helm Chart

For production environments, using a Helm chart provides a more robust and maintainable deployment approach compared to raw manifest files. The PagerDuty Runbook Automation Helm chart offers:

- **High Availability:** Multiple replicas with session affinity and load balancing
- **Production-Ready Configuration:** Integration with RDS, S3, Route53, and ACM
- **Security:** Proper secrets management and ACL configuration
- **Scalability:** Resource limits, auto-scaling capabilities, and cluster configuration
- **Maintainability:** Version control, easy upgrades, and rollback capabilities

### Quick Start with Helm

#### Prerequisites

- **Helm 3.x** installed ([Installation Guide](https://helm.sh/docs/intro/install/))
- AWS infrastructure:
  - AWS Load Balancer Controller
  - ExternalDNS
  - RDS Database (MySQL/MariaDB)
  - S3 Bucket for logs
  - Route53 Hosted Zone
  - ACM Certificate

#### Installation Steps

1.  **Create namespace and database secret:**

<div class="language-bash line-numbers-mode">

``` bash
kubectl create namespace rundeck
kubectl create secret generic database-password \
  --from-literal=password='YOUR_DATABASE_PASSWORD' \
  --namespace=rundeck
```

</div>

1.  **Prepare configuration files:**

    - `admin-role.aclpolicy` - Admin ACL permissions
    - `realm.properties` - Local user accounts

2.  **Customize values.yaml** with your environment settings:

    - Ingress host and ACM certificate ARN
    - RDS database endpoint
    - S3 bucket for logs
    - LDAP/AD configuration (if applicable)

3.  **Install the Helm chart:**

<div class="language-bash line-numbers-mode">

``` bash
# Clone the docker-zoo repository
git clone https://github.com/rundeck/docker-zoo.git
cd docker-zoo/kubernetes/helm

# Install the chart
helm install rundeckpro ./rundeckpro \
  --namespace=rundeck \
  --set-file aclFile=./admin-role.aclpolicy \
  --set-file realm=./realm.properties \
  --values values.yaml
```

</div>

1.  **Verify the deployment:**

<div class="language-bash line-numbers-mode">

``` bash
kubectl get pods -n rundeck
kubectl get ingress -n rundeck
```

</div>

### Full Documentation

For complete Helm chart documentation, including:

- Architecture overview
- Detailed prerequisites and AWS infrastructure setup
- All configuration options
- LDAP/AD integration
- Production vs. development configurations
- Troubleshooting guide
- Security best practices

Visit the [Runbook Automation Helm Chart README](https://github.com/rundeck/docker-zoo/tree/master/kubernetes/helm/rundeckpro).

### Uninstalling

#### To uninstall the basic Rundeck deployment use:

<div class="language-text line-numbers-mode">

``` text
kubectl delete deployment rundeck-deployment
```

</div>

#### Destroy the Service with:

<div class="language-text line-numbers-mode">

``` text
kubectl delete service rundeck-svc
```

</div>

#### To uninstall a Helm-based deployment:

<div class="language-text line-numbers-mode">

``` text
helm uninstall rundeckpro --namespace=rundeck
```

</div>

**Note:** The Helm uninstall command removes all Kubernetes resources (deployments, services, ingress, secrets) but does NOT delete the RDS database, S3 bucket, or Route53 records.

## Resources

- AWS EKS [Introduction](https://aws.amazon.com/eks/)  
- AWS CLI [Documentation](https://aws.amazon.com/cli/)  
- EKS CTL [Getting Started](https://eksctl.io/getting-started/)  
- Kubectl [Getting Started](https://kubernetes.io/docs/setup/)  
- Rundeck K8s [examples](https://github.com/rundeck/docker-zoo/tree/master/kubernetes) (DockerZoo)
