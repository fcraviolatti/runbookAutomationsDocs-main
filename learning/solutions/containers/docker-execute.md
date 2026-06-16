---
title: "Executing Commands in Docker Containers"
source_url: https://docs.rundeck.com/docs/learning/solutions/containers/docker-execute.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Executing Commands in Docker Containers

Executing a command in a Docker Container can be beneficial in many ways to DevOps teams. Docker can dynamically provide very specific environments which allow for controlled testing and execution of commands. In this solution example we will run a simple command in a Docker Image.

## Pre-requisites & Environment Setup

- For ease of testing, have an [Enterprise Runner](https://docs.rundeck.com/docs/administration/runner/runner-overview.html) running on the same host that is running Docker and use the [Automatic Runner Dispatch](https://docs.rundeck.com/docs/administration/runner/runner-management/project-dispatch-configuration.html) setup.
- Must setup Docker Node Source before running this job.
- The example job assumes the base OS of Docker image is Linux based.

#### Setting up Docker Node Source

1.  Open the `Example Content` project.
2.  Navigate to *Project Settings* \> *Edit Nodes*
3.  Click **Add A Node Source**
4.  Choose the `docker / container / model` entry.
5.  Specify your Runner and **Save**.

[More specifics about setting up this Node Source can be found on it's documentation page here.](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/docker.html)

#### Running the Job

> **Tips**
>
> To find the Docker jobs quickly in the job listing click on the `docker` tag at the top of the list.

![Select Job Image](https://docs.rundeck.com/docs/assets/img/solutions-docker-selectjob.png)  

The default node filter for this job is `tags: "docker"`. Nodes discovered by the Docker node source above will automatically get this tag assigned to them. If you'd like to run the job on a particular container select it from the list.

The default command will run `ls -last` on any container in the target list along with the other steps in the job definition.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/solutions-docker-runjob.png" alt="Run Job Screen" />
<figcaption aria-hidden="true">Run Job Screen</figcaption>
</figure>

Here is some example output

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/solutions-docker-output.png" alt="Example Output" />
<figcaption aria-hidden="true">Example Output</figcaption>
</figure>
