---
title: "Job Plugins"
source_url: https://docs.rundeck.com/docs/learning/getting-started/jobs/job-plugins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Job Plugins

[Plugins](https://docs.rundeck.com/docs/manual/plugins/#plugins) are a key element of Rundeck and the PagerDuty Runbook Automation Self-Hosted products. They get used [in many different ways](https://docs.rundeck.com/developer/) in different parts of the product. Most commonly, they are used to allow integration with third-party tools.  
When talking about plugins in the context of jobs, many of the common node steps and workflow steps are plugins, as are notifications, node orchestrators and log filters (among other things). Creating plugins for jobs allows users to use the same script across multiple jobs. This can be very useful for instances where teams or users are using the same steps in multiple jobs.  

## Plugin development

There are [three ways](https://docs.rundeck.com/developer/) to develop plugins and they are available to any Rundeck or Runbook Automation Self-Hosted user whoâ€™d like to build a plugin. Two of those methods are fairly technical ([Java development](https://docs.rundeck.com/docs/developer/java-plugin-development.html) and [Groovy development](https://docs.rundeck.com/docs/developer/groovy-plugin-development.html)), but the third is fairly accessible for anyone who wants to convert commonly used jobs or portions of jobs into plugins. This method is called [Script Plugin Development](https://docs.rundeck.com/docs/developer/script-plugin-development.html). Script plugins can be used for the following plugin types: [Node Executor](https://docs.rundeck.com/docs/developer/node-executor-plugins.html#script-plugin-type), [File Copier](https://docs.rundeck.com/docs/developer/file-copier-plugins.html#script-plugin-type), [Node Sources](https://docs.rundeck.com/docs/developer/resource-model-source-plugins.html#script-plugin-type) and [Node/Workflow Steps](https://docs.rundeck.com/docs/developer/step-plugins.html#about). The most common scripting languages used to create script plugins are bash, python and Powershell.  

## When to create a Plugin

Watch for cases where job editors are repeatedly using the same set of steps in multiple jobs or calling a job from many other jobs. Either of those cases might be an indication that it is worth creating a script plugin that could be re-used by several jobs and accomplishes the same as the code that would otherwise be copied from job to job.  

## Getting Started with Script Plugins

To get started, check out [this article](https://docs.rundeck.com/docs/learning/howto/custom-script-plugin-hello-world.html) that provides details for how to create a script plugin and shows a good basic example. Additional examples of all plugin types are available [here](https://www.google.com/url?q=https://github.com/rundeck/rundeck/tree/main/examples&sa=D&source=docs&ust=1679435774123407&usg=AOvVaw2ahcjy7g-qWjDi-ZMq9tbm).
