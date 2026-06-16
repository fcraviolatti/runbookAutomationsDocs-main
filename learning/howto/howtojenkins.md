---
title: "Integrate with Jenkins"
source_url: https://docs.rundeck.com/docs/learning/howto/howtojenkins.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Integrate with Jenkins 

![ ](https://docs.rundeck.com/docs/assets/img/jenkins1_RDplusJenkins.png)  
[Jenkins](https://www.jenkins.io/) has transformed development tooling by putting control over building pipelines into the hands of individual developers. For Operations, Rundeck delivers the same openness, ease of use, and extensibility - while giving individuals control over defining and creating self-service operations tasks. Rundeck is built specifically to turn any operations procedure into a repeatable and secure service that can be accessed securely via a Web GUI or API. Because it is not focused specifically on building software artifacts, Rundeck jobs can make real changes, update network and infrastructure configuration, and simplify all types of business workflows.  
  
Jenkins and Rundeck integrate well and are commonly used by organizations who are looking to achieve high-velocity and high-quality results across the full Development to Operations lifecycle. In summary, Jenkins manages software build pipelines, and Rundeck manages and provides self-service access to all operations tasks.  
  
In this article, we will explain the basic Rundeck / Jenkins integration and walk you through an example use case.  

## The Rundeck Jenkins Plugin 

The Rundeck plugin integrates Rundeck in the Jenkins pipeline. The plugin connects to a Rundeck instance (via its API) to schedule a job execution on Rundeck after a successful build on Jenkins.  
  
It is also a Trigger that will schedule a build in Jenkins after a job execution is completed in Rundeck (using Rundeck WebHook Notification). In addition, it turns Jenkins into an Option provider for Rundeck, which allows you to use your Jenkins build artifacts as an option for a Rundeck job.  
  
The Rundeck plugin allows for Jenkins and Rundeck to connect in three ways:  

- To build a "deployment pipeline," you commit a change, Jenkins picks it up, builds, tests, and so on, and then triggers a job execution in Rundeck for deploying your application. This requires some configuration on Jenkins, both global configuration and job configuration, to connect a Jenkins job with a Rundeck job.  
- To continue your pipeline after the deployment, Rundeck deploys your application, then triggers a build on Jenkins to run some integration tests. This requires some configuration on Rundeck (WebHook notification) and on Jenkins (Trigger configuration, and optionally, filter the notifications from Rundeck).  
- To use Jenkins as an Option provider for Rundeck, when you execute a Rundeck job, you can have an (input) option, whose values could be retrieved from an external system (here, Jenkins). So you can have a Rundeck job that uses a Jenkins artifact (from a Jenkins build) as an input.  
  [Here](https://github.com/jenkinsci/rundeck-plugin) is the official pluginâ€™s GitHub space.  

### Installing the plugin 

So, to install the Rundeck Jenkins plugin, follow these steps:  

1.  After logging into the Jenkins instance, click on the "Manage Jenkins" link.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins2_manage.png)  
2.  Click on the "Manage Plugins" option.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins3_manageplugins.png)  
3.  On the Plugin Manager page, click the "Available" tab, type "rundeck" in the search textbox (right), and click on the "Install without restart" button (bottom).  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins4_pluginmanager.png)  
4.  To check if the plugin is available, click on the "Manage Plugin" link, click on the "Installed" tab, and type "rundeck" on the search textbox.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins5_installingplugins.png)  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins7_pluginsinstalled.png)  
    Now the plugin is listed and ready to use.  

### Configuring the Rundeck instance on Jenkins 

Next, configure the plugin to point at the Rundeck instance.  
  

1.  On the Jenkins main page click on the "Manage Jenkins" link (left) and then click on the "Configure System" option.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins8_configsys.png)  
2.  Now, with the Rundeck plugin installed, a new "Rundeck" section is available on the main Jenkins options. In that section, click on the "Add Rundeck" button.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins9_addrundeck.png)  
3.  Give it a name, URL (specifying the full URL Rundeck instance including the port, 4440 in this case), username/password or auth token (to learn how to create auth token please visit [this](https://docs.rundeck.com/docs/manual/10-user.html#user-api-tokens) doc entry), and the API version.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins10_testconnection.png)  
4.  To check if all information is well configured, click on the "Test Connection" button, if all is right, you can see a "Your Rundeck instance is alive, and your credentials are valid!" message, and just click on the â€œSaveâ€? button.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins11_saveconfig.png)  
    Now, the Rundeck instance is configured to use on any Jenkins pipeline.

# Example Use Case

In this scenario, Jenkins is triggering Rundeck to do deployments in a Continuous Deployment scenario, which allows direct Jenkins access to production environments to be restricted.  
![ ](https://docs.rundeck.com/docs/assets/img/jenkins12_fancy.png)  
For calling Rundeck jobs from Jenkins, the Rundeck Jenkins plugin plays a key role. Jenkins can also be an option provider that delivers dynamic input to Rundeck jobs, in the following example letâ€™s start a Rundeck job after a Jenkins deployment.  

1.  Create a new Jenkins project, click on the "New Item" link (left menu on the main Jenkins page).  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins13_newproject.png)  
2.  Select "Freestyle project" and give it a name. In this example the name is "BuildAndDeployApp".  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins14_freestyle.png)  
3.  Optionally add a description (on the "Description" section).  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins15_desc.png)  
4.  Scroll down and locate the Build section. It's possible to add multiple build steps. For now, click on the "Add build step" button and select "Execute shell".  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins16_buildstep.png)  
5.  This example just prints a "building..." string with five seconds of sleep time. If you want to add more steps just click on the "Add build step" button again.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins17_shellcommand.png)  
6.  Now it's time to call the Rundeck job, scroll down and locate the "Add post-build action button", then select Rundeck.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins18_callrundeck.png)  
7.  This step uses the general plugin configuration. So, it isn't necessary to fill in the username, password, and token textboxes. The step needs the [Job ID](https://docs.rundeck.com/docs/manual/jobs/#job-uuids) to launch it. Once that is entered, click on the "Save" button.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins19_jobid.png)  
8.  Now run the Jenkins build by clicking the "Build Now" link (on the left menu).  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins20_buildnow.png)  
9.  Below, in the same menu, a new entry appears.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins21_newentry.png)  
10. Click on the execution number and then click on the "Console Output" option.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins22_consoleoutput.png)  
      
11. The job output is available in the Jenkins console output, including Rundeck.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins23_fullconsoleoutput.png)  
12. And checking the Rundeck activity execution, all steps were executed.  
    ![ ](https://docs.rundeck.com/docs/assets/img/jenkins24_activity.png)  
    Jenkins and Rundeck are often used together by Development and Operations teams. Using both Jenkins and Rundeck together connects repeatable build, test, and integration processes with infrastructure and production operations. With this integration, itâ€™s easier to meet security and compliance obligations while reducing the toil that impacts your ability to deliver meaningful value to the business.
