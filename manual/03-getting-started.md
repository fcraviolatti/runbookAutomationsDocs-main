---
title: "Getting Started"
source_url: https://docs.rundeck.com/docs/manual/03-getting-started.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Getting Started

The best way to get started with Rundeck is through our [Learning section](https://docs.rundeck.com/docs/learning/).  
[Terminology](https://docs.rundeck.com/learning/tutorial/terminology), [Tutorials](https://docs.rundeck.com/learning/tutorial/preparing) and [How To articles](https://docs.rundeck.com/learning/how-to/overview) that show the many ways to use Rundeck.

## Essential Concepts

Several fundamental concepts underlie and drive the Rundeck system. If you are a new user, knowing about them will help you use or integrate Rundeck into your environment.

- **Projects**: A *[project](https://docs.rundeck.com/docs/manual/projects/)* is a place to separate management activity. All Rundeck activities occur within the context of a project. Multiple projects can be maintained on the same Rundeck server.

- **Jobs** : A *job* encapsulates a sequence of steps, job options and nodes where the steps execute. See [Jobs](https://docs.rundeck.com/docs/manual/jobs/) and [Creating Jobs](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html).

- **Nodes**: A *[node](https://docs.rundeck.com/docs/manual/05-nodes.html)* is a resource that is either a physical or virtual instance of a network accessible host. A *resource model* is a representation of Nodes in a project.

- **Commands**: A *[command](https://docs.rundeck.com/docs/manual/06-commands.html)* is a single executable string executed on a Node. Rundeck invokes commands on nodes via a *node executor*, which evaluates the command string and executes it.

- **Executions**: An *[execution](https://docs.rundeck.com/docs/manual/07-executions.html)* is a representation of the activity of a running or completed command or job. The data about the execution is used in rundeck to monitor the progress of a job or command, and later for reporting about what happened.

- **Role-based Access Control Policies**: A Rundeck *[access control policy](https://docs.rundeck.com/docs/administration/security/authorization.html)* grants users and user groups certain privileges to perform actions against rundeck resources like projects, jobs, nodes, commands and API.

- **Plugins**: Extending Rundeck functionality is done through *plugins*. Plugins exist to execute commands on nodes, perform steps in a job, send a notification about job status, gather information about the hosts in your network, copy a file to a remote server, store and stream logs, talk to a user directory, and so much more.

  Our Enterprise version includes built-in plugins to further enhance functionality for [Scheduling](https://docs.rundeck.com/docs/manual/schedules/project-schedules.html) job executions, providing [Guided Tours](https://docs.rundeck.com/docs/manual/tour-manager.html), incorporating [Health Checks](https://docs.rundeck.com/docs/manual/healthchecks.html), and much more.

  See [Job Plugins](https://docs.rundeck.com/docs/manual/jobs/job-plugins/) and [Plugin Developer Guide](https://docs.rundeck.com/docs/developer/) and [Rundeck Plugins](https://docs.rundeck.com/docs/manual/plugins/).

## Download and Installation

If a running Rundeck instance isn't already available to you, there are a couple ways you can try it.

- Check out the Docker based Welcome Projects described on the [Learning Overview Page](https://docs.rundeck.com/docs/learning/).

- Visit our download site [download](http://rundeck.org/downloads.html) and install the Rundeck software. There are several package formats. Choose the one that best suits the target infrastructure. After installation, be sure Rundeck has been started.

  > **Tips**
  >
  > See [Startup](https://docs.rundeck.com/docs/administration/maintenance/startup.html) to learn how to startup and shutdown rundeck.

The default port for the web interface is `4440`. If you installed Rundeck on your local machine, go to this URL: `http://locahost:4440`

## Login

Rundeck requires every user to login. The default installation defines an "admin" user with access to perform all actions. Use "admin" for username and password.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0202.png" alt="Login form" />
<figcaption aria-hidden="true">Login form</figcaption>
</figure>

## Project setup

A new installation will not contain any projects so Rundeck will present you with a dialog to create one. Press the "New Project" button to create a project. Fill the project creation form with a desired name. Project names can contain letters and numbers, but do not use spaces or special characters. The [project](https://docs.rundeck.com/docs/manual/projects/) section will teach you how to add Nodes, automate the creation and maintenance of Rundeck projects.

Once the project has been created, you are ready to use your Rundeck instance.

## Rundeck Graphical Console (GUI)

### Navigation

Using the project picker in the top bar it is possible to quickly search, list and switch between the various projects configured. Once inside a project navigation is done using the navigation bar on the left side of the page. *Dashboard*, *Jobs*, *Nodes*, *Commands*, *Activity*, and other pages. Project administrators will also be able to access the *Project Settings* pages menu.

For those with Rundeck administrator access, the System settings can be accessed by clicking the gear icon in the page header.

Finally, the user profile and logout functions are found under the User icon.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0201.png" alt="Top level navigation" />
<figcaption aria-hidden="true">Top level navigation</figcaption>
</figure>

#### Projects menu

Select the desired project. If only one project exists, the menu will automatically be selected. You can create new projects from this menu, too.

#### Dashboard

View the project description, Readme and executions summary. Runbook Automation users may see additional visualizations for schedules and execution history.

#### Jobs

From the Jobs page, one can list, create, and run Jobs. A configurable filter allows a user to limit the Job listing to Jobs matching the filtering criteria. These filter settings can be saved to a user profile. Only authorized jobs will be visible.

> **Tips**
>
> See [Jobs](https://docs.rundeck.com/docs/manual/jobs/).

#### Nodes

The Nodes page is used to browse the Nodes configured in your Project resource model. A filter control can be used to limit the listing to just the Node resources matching the filter criteria. Given the appropriate authorization, you can also execute ad hoc commands to your filtered node set.

> **Tips**
>
> See [Nodes](https://docs.rundeck.com/docs/manual/05-nodes.html).

#### Commands

The Commands page lets you execute arbitrary commands against the nodes that match the node filter.

> **Tips**
>
> See [Commands](https://docs.rundeck.com/docs/manual/06-commands.html).

#### Activity

From the Activity page, one can view currently executing Commands and Jobs, or browse execution history. The execution history can be filtered based on user-selected parameters. Once the filter has been set, the matching history is displayed. The current filter settings also configure an RSS link, found in the top right of the page (see Rundeck Administration to enable RSS).

> **Tips**
>
> See [Activity](https://docs.rundeck.com/docs/manual/08-activity.html).

#### System

If your login belongs to the "admin" group and therefore is granted "admin" privileges, a "System" icon will be displayed in the top navigation bar. From the System menu you can access the Key Storage, System Configuration, Access Control, System Report, Log Storage, List Plugins, Password Utility and Execution model.

> **Tips**
>
> See [Configure](https://docs.rundeck.com/docs/manual/system-configs.html)

#### User

The User menu lets you logout and view your profile page. Your user profile lists your group memberships and a form to list and generate API tokens.

> **Tips**
>
> See [User](https://docs.rundeck.com/docs/manual/10-user.html)

## Command Line Tools

Rundeck includes a number of shell tools to dispatch commands, load and run Job definitions, and interact with the dispatcher's queue. These command line tools are an alternative to functions accessible in the graphical console.

See the [Command line tools](https://docs.rundeck.com/docs/manual/command-line-tools/).

## API

You can also use the Web API to interface with all aspects of Node and Job execution.

See the [Rundeck API](https://docs.rundeck.com/docs/api/) page for a reference on the endpoints and examples.

## Document Formats

If you prefer to manage job and resource definitions using text files, you can do so using XML or YAML formats.

See the [Document Format Reference](https://docs.rundeck.com/docs/manual/document-format-reference/).
