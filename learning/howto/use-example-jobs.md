---
title: "Use Rundeck Example Jobs"
source_url: https://docs.rundeck.com/docs/learning/howto/use-example-jobs.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Use Rundeck Example Jobs

## Overview

A good way to understand different problem solving approaches in Rundeck is by seeing how theyâ€™re implemented. The [Community Welcome Project](https://github.com/rundeck/welcome-project-community) has a series of individual [example jobs](https://github.com/rundeck/welcome-project-community/tree/main/runbooks/yaml) that you can download, import into your Rundeck instance, adapt, and test. The example jobs are written to work with the Welcome Projects, but these steps can be used to import into any project.

The library of example jobs provides examples of job definitions for common use-cases and platform-focused runbooks to help show new users the power of runbook automation and make it easy for existing users to add new job definitions to their Rundeck. Rundeck uses exchangeable formats to share their jobs: XML or/and YAML, making it easy to store on any repository.

This guide covers:

- How to test individual job definitions in the Community Welcome Project

## Testing the Job Definitions on a Local Rundeck Instance

The job definitions are available to download here: <https://github.com/rundeck/welcome-project-community/tree/main/runbooks/yaml>

Download the zip file from the repository:

1.  Navigate to <https://github.com/rundeck/welcome-project-community>
2.  Click on the â€œlatestâ€? release in the right,
3.  Download the Source Code (.zip) file.
4.  Extract the contents to a folder on your local hard drive.

All runbook job definitions are located in the `runbooks/yaml` folder inside the main repository directory.

1.  Click on the **Jobs** page (left menu) of your Project.
2.  And click on the **Upload a job definition** button.  
      
    ![Upload Definition](https://docs.rundeck.com/docs/assets/img/howto-jobs-uploaddef.png)  
      
3.  Click on **Browse** to select any YAML file downloaded from the repository.  
      
    ![Select Job Definition](https://docs.rundeck.com/docs/assets/img/howto-browse-jobdef.png)  
      
4.  Scroll down and click on the **Upload** button.
5.  Now the job is imported. In the screenshot we chose to upload the *Global Log Filter Usage* example job.  
      
    ![Definition Upload Success](https://docs.rundeck.com/docs/assets/img/howto-jobdef-success.png)  
      
6.  Run the job by **clicking on the job name** and then on **Run Job Now**  
      
    ![Run Job Now](https://docs.rundeck.com/docs/assets/img/howto-jobdefs-runjobnow.png)  
      
7.  Then, you can see the results.  
      
    ![Job Results](https://docs.rundeck.com/docs/assets/img/howto-jobdef-jobresults.png)
