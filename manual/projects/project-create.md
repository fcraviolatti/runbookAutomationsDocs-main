---
title: "Project Create"
source_url: https://docs.rundeck.com/docs/manual/projects/project-create.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Project Create

A project can be created either from the graphical console or using the [rd](https://rundeck.github.io/rundeck-cli/) shell tool.

## Graphical Interface

In the graphical console, you will notice a Project Picker in the top navigation bar. This is the primary access to the different projects. To see the full Project Menu click on *View All Projects* or click the Rundeck logo in the upper left of the screen.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-picker.png" alt="Project Picker" />
<figcaption aria-hidden="true">Project Picker</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-list-full.png" alt="Full Project Menu" />
<figcaption aria-hidden="true">Full Project Menu</figcaption>
</figure>

If no projects exist, the project menu will not be displayed you will be prompted to create a new project.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-list-empty.png" alt="Creat a project" />
<figcaption aria-hidden="true">Creat a project</figcaption>
</figure>

When one or more projects exist, a project can be created by either clicking on the "New Project" link in the full project menu.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-list-newbutton.png" alt="Creat a project" />
<figcaption aria-hidden="true">Creat a project</figcaption>
</figure>

Press the "New Project" button to create a project.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-create-blank.png" alt="Figure: Create project prompt" />
<figcaption aria-hidden="true">Figure: Create project prompt</figcaption>
</figure>

*Details*

Name  
This is the unique identifier for the project. Project names can contain letters and numbers but do not use spaces or special characters.

Label  
You may wish to use a more user friendly display name for the project. The project label can contain spaces and other characters.

Description  
A brief explanation about the project. Normally, this is just one phrase or sentence explaining the project purpose. If you have large amounts of text, consider creating a project README.

*Execution History Clean*

When you enable Execution History Clean, you can control the frequency which Rundeck removes your execution history.

*Execution Mode*

Disable Execution  
Turn off the ability to execute jobs and ad-hoc commands.

Disable Schedule  
Turn off the job scheduling feature.

*User Interface*

Job Group Expansion Level  
In the Jobs page, how should the job groups be collapsed? A `1` is default and shows one group level opened. Use `0` to collapse all. Use `-1` to expand all.

Display the Readme  
Show the Readme in the project list and/or home page.

Display the MOTD  
Show the Readme in the project list and/or home page.

*Default Node Executor*

The Node Executor is responsible for executing commands and scripts on remote nodes. On Linux machines, SSH will be default.

*Default File Copier*

The File Copier is responsible for copying scripts as files to remote nodes before they are executed. On Linux machines, SCP will be default.

*Create*

After filling in the project create form, Rundeck initializes it and returns you to the default page (eg, "Jobs").

Projects can be created at any time by going back to the Project menu and clicking on the "New Project" link in the navigation menu or by going to the home page and pressing the "New Project" button.

The project setup process generates Project configuration in the server, and a local resource model containing information about the rundeck server node.

## Automating

### CLI Usage

The [rd projects](https://rundeck.github.io/rundeck-cli/) command can be used to script the creation for projects. See the `rd projects create help` output for syntax usage.

Execute the `rd projects create` command and specify a project name, here we use "MyProject":

<div class="language-bash line-numbers-mode">

``` bash
rd projects create -p MyProject
```

</div>

You can also declare configuration properties when you create the project.

Here a project label and the default SSH key properties are declared as command line options:

<div class="language-bash line-numbers-mode">

``` bash
rd projects create -p MyProject -- \
   --project.label="My Project" \
   --project.ssh-keypath=/home/rundeck/.ssh/id_rsa
```

</div>

You can specify a resource model source by specifying keys as command line options, too. Here a Directory model source is also defined.

<div class="language-bash line-numbers-mode">

``` bash
rd projects create -p MyProject -- \
  --project.label="My Project" \
  --project.ssh-keypath=/home/rundeck/.ssh/id_rsa \
  --resources.source.2.type=directory \
  --resources.source.2.config.directory=/home/rundeck/projects/MyProject/resources.d
```

</div>

### API Usage

Project creation can be achieved via the [API](https://docs.rundeck.com/docs/api/).

[Create projects](https://docs.rundeck.com/docs/api/#project-creation):

<div class="language-text line-numbers-mode">

``` text
POST /api/13/projects
Content-Type: application/json

{ "name": "MyProject", "config": { "project.label":"My Project" } }
```

</div>
