---
title: "Manage Jobs as Code (Source Control Management)"
source_url: https://docs.rundeck.com/docs/learning/howto/how2scm.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Manage Jobs as Code (Source Control Management)

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/scm1.png" />
</figure>

[The Rundeck Git plugin](https://docs.rundeck.com/docs/manual/projects/scm/git.html) allows organizations to manage Rundeck jobs as source code by versioning, exporting, or importing their definitions using a remote Git repository. Managing jobs in this way takes advantage of your existing code review processes to ensure that only approved job code is allowed in production projects or instances. Users can backup, manage, and approve changes to their Rundeck jobs using any Git solution like Github/Gitlab/BitBucket, centralizing the job code in one place.

Enable SCM (Source Control Management) for managing Job definitions on a per-project basis. The SCM plugin can be configured to either import or export. This approach can be applied in any way that matches an organizationâ€™s code review processes but is often configured with a development project where jobs can be modified and developed for export to an experimental branch in Git and a production project that imports jobs from the approved and stable branch.

# Background

There are two integration modes for the SCM Plugin, *import,* and *export*, which are managed separately. A Project can be configured with a single SCM plugin to either import or export. After setting up the plugin, the Project and Job level "status" can be read. Changes to Jobs within a project affect the status of import or export.

For example, if the project is set to import, there will be indicators where jobs are out of sync with the source and could be imported.

The Git plugin provides "actions" which are available based on the Project or Job status. For example, a plugin can provide a "commit" action for a Job, which allows a user to save the changes for the job.

# Prerequisites

To follow this tutorial you need to have Docker installed on your computer. Go [here](https://docs.docker.com/get-docker/) to install Docker Desktop depending on your Operating System.

# Example Docker Environment

This Docker-compose file contains both Rundeck and GitBucket servers to test the Git plugin functionality.

<div class="language-text line-numbers-mode">

``` text
version: "3"
services:
 rundeck:
   container_name: rundeck_oss
   image: rundeck/rundeck:4.5.0
   ports:
     - 4440:4440
   environment:
     RUNDECK_GRAILS_URL: http://localhost:4440
 gitbucket:
   container_name: git_bucket
   image: gitbucket/gitbucket
   ports:
     - 8080:8080
```

</div>

To run use:

<div class="language-text line-numbers-mode">

``` text
docker-compose up
```

</div>

## Exporting Jobs

1.  Enter GitBucket server  
    <div class="language-text line-numbers-mode">

    ``` text
    http://localhost:8080`, user: `root`, password: `root`
    ```

    </div>
2.  Once logged in, create a new repository, by clicking on the "+" top icon and then on "New Repository".  
    ![](https://docs.rundeck.com/docs/assets/img/scm2.png)  
3.  Put a name in the "Repository name" textbox and select "Initialize this repository with a README".  
    The new repository should now contain the "master" branch by default.  
4.  Click on the "Create repository" button. That's all you need to complete in GitBucket.  
    ![](https://docs.rundeck.com/docs/assets/img/scm3.png)  
5.  Log in to Rundeck  
    <div class="language-text line-numbers-mode">

    ``` text
    http://localhost:4440, user: admin, password: admin
    ```

    </div>
6.  Add a new password in the key storage.  
      
    **Key Type:** Password  
    **Enter text:** The password for the Git repository  
    **Storage path:** Can be left blank  
    **Name:** gitbucket_passwd  
      
    ![](https://docs.rundeck.com/docs/assets/img/scm4.png)  

> **Tips**
>
> If you're using GitHub, it doesn't allow passwords to connect to the repositories via HTTPS. Instead of a password, GitHub accepts personal tokens. To create a token, follow these steps:  
>
> 1.  Go to your User Icon (up to right) and select "Settings".  
> 2.  Scroll down and click "Developer settings" at the end of the left menu.  
> 3.  Now click on "Personal access tokens".  
> 4.  Click the "Generate new token" button and then create a new token.  
> 5.  The token value could be used as a password in the SCM configuration.  

## Exporting Jobs, continued

1.  Now, configure SCM in a Rundeck project. Go to the left navigation and click on "Project Settings" and select the "SETUP SCM" option from the menu.  
    ![](https://docs.rundeck.com/docs/assets/img/scm5.png)  
2.  Click on "Setup" in the â€œGit Exportâ€? section.  
    ![](https://docs.rundeck.com/docs/assets/img/scm6.png)  
3.  In the "Project" section, add the Git repository username and a valid committer/author email.  
    ![](https://docs.rundeck.com/docs/assets/img/scm7.png)  
4.  Scroll and check the "Git Repository" section. The Git URL must be filled in using the following format to connect via the HTTPS method:  
    `http(s)://user@git_hostname:port/git/user/repo.git`. In this example we used: `http://root@gitbucket:8080/git/root/rdeck_jobs.git`. Additionally, make sure to fill the "Branch" with the first branch created in step 2, "master".  
    ![](https://docs.rundeck.com/docs/assets/img/scm8.png)  
5.  Job Source Files (XML or YAML)  
    **Format** yaml  
    **Authentication** Enter key storage password path created in the third step.  
    ![](https://docs.rundeck.com/docs/assets/img/scm9.png)  
6.  Save the config.  
    ![](https://docs.rundeck.com/docs/assets/img/scm10.png)  
7.  Create a couple of jobs. You should see a green exclamation icon next to each, which signals the job is available in Rundeck and ready to export to the GitBucket repository configured above.  
    ![](https://docs.rundeck.com/docs/assets/img/scm11.png)  
8.  To export both jobs to the GitBucket repo, click on "Job Actions" and select "Commit Changes to Git".  
    ![](https://docs.rundeck.com/docs/assets/img/scm12.png)  
9.  In the "Commit Message" put a friendly commit message, which is mandatory. Click on the "Commit" button.  
    ![](https://docs.rundeck.com/docs/assets/img/scm13.png)  
10. "Remote push result: OK" should appear at the top  
    ![](https://docs.rundeck.com/docs/assets/img/scm14.png)  
11. To verify, go to GitBucket and look at the repository. You should see both jobs.  
    ![](https://docs.rundeck.com/docs/assets/img/scm15.png)  
12. Test further by editing a job in Rundeck and adding a description. The job structure will change and the SCM plugin will detect this change to export it.  
    ![](https://docs.rundeck.com/docs/assets/img/scm16.png)  
13. After saving, the blue "Modified" message appears.  
    ![](https://docs.rundeck.com/docs/assets/img/scm17.png)  
14. A blue exclamation icon will appear in the job list as well.  
    ![](https://docs.rundeck.com/docs/assets/img/scm18.png)  
15. An additional way to see the job change is by clicking on the job "Actions" button and then on "Diff Changesâ€?.  
    ![](https://docs.rundeck.com/docs/assets/img/scm19.png)  
16. To commit changes to GitBucket, click on the "Commit Changes to Git" blue button.  
    ![](https://docs.rundeck.com/docs/assets/img/scm20.png)  
17. Add a comment on the last change and click on the green "Commit" button.  
    ![](https://docs.rundeck.com/docs/assets/img/scm21.png)  
    ![](https://docs.rundeck.com/docs/assets/img/scm22.png)  
18. Now go back to the GitBucket repository. The changes should be uploaded with the new comment attached.  
    ![](https://docs.rundeck.com/docs/assets/img/scm23.png)  

> **Tips**
>
> Note: The SCM plugin should be used either for Import or Export on a single project, not both. To test importing, you should use or create a different project than you used for the export section above.  

## Importing Jobs

1.  In your import project, select "Projects Settings" from the left navigation and click on "SETUP SCM".  
    ![](https://docs.rundeck.com/docs/assets/img/scm24.png)  
2.  Scroll to the "Import" section and click on "Setup".  
    ![](https://docs.rundeck.com/docs/assets/img/scm25.png)  
3.  Git Repository section  
    **Git URL**  
    Must be filled in the following format to connect via HTTPS method: `http(s)://user@git_hostname:port/git/user/repo.git`. We used: `http://root@gitbucket:8080/git/root/rdeck_jobs.git`.  
      
    ![](https://docs.rundeck.com/docs/assets/img/scm26.png)  
4.  Setup section  
    **Regular Expression** .\*\yaml  
5.  Job Source/Files section  
    **Format** Select "yaml"  
6.  Authentication section  
    **Password Storage Path** Add the key storage path for the GitBucket account user password  
    ![](https://docs.rundeck.com/docs/assets/img/scm27.png)  
7.  Click on the "Setup" button. Now the configuration is saved.  
    ![](https://docs.rundeck.com/docs/assets/img/scm28.png)  
8.  Click on Jobs in the left navigation. If the repository contains jobs, you will see a blue banner. Scroll over the banner and you will see the number of jobs available to import to the Rundeck instance.  
    ![](https://docs.rundeck.com/docs/assets/img/scm29.png)  
    ![](https://docs.rundeck.com/docs/assets/img/scm30.png)  
9.  Rundeck shows the available jobs to import. Click on the "Import" button.  
    ![](https://docs.rundeck.com/docs/assets/img/scm31.png)  
10. The jobs should be imported from the Rundeck instance to the GitBucket repository.  
    ![](https://docs.rundeck.com/docs/assets/img/scm32.png)  

### Resources

[About the Git Plugin](https://docs.rundeck.com/docs/manual/projects/scm/git.html#git-plugin) (Rundeck Documentation)
