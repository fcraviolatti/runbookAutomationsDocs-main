---
title: "kubernetes"
source_url: https://docs.rundeck.com/docs/learning/solutions/containers/kubernetes.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# kubernetes

## Kubernetes Solutions

Kubernetes is an open-source platform that allows for the management on a containers on a large scale. Developers, IT administrators, and DevOps engineers use Kubernetes to automate the deployment, scaling, maintenance, scheduling, and operation of *"containerized"* applications and services. Kubernetes is frequently used for managing microservices applications with multiple service instances, where each microservice is deployed in an individual container.

### Troubleshooting Kubernetes

Because of so many moving components, it is sometimes difficult to pin down the root cause of an issue for an application running on Kubernetes. Unintended behavior could be isolated to a single container, one or more pods, a controller, control-plane components or one of the underlying infrastructure components.

Because some organizations only have a handful of Kubernetes experts on staff, this results in frequent escalations to these experts or prolonged incidents while non-experts try to diagnose issues.

In order to effectively troubleshoot issues in Kubernetes, teams must be equipped with the right tooling that spreads expert-level knowledge and reduces silos between application-development teams and their counterparts in Operations.

### Plugins for Kubernetes

There are numerous plugins that make it possible to get started quickly with Auto-Diagnostics in Kubernetes:

- [Kubernetes Pods - Resource Model](https://github.com/rundeck-plugins/kubernetes#resource-model)
- [Kubernetes Node Executor](https://github.com/rundeck-plugins/kubernetes#node-executor)
- [Check on a Kubernetes Deployment](https://github.com/rundeck-plugins/kubernetes#create--update--delete--check--wait-a-deployment)

It is also very common for users to want to â€œwrap aroundâ€? the Kubernetes command-line **`kubectl`**.

### Template Jobs
