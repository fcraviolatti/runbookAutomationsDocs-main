---
title: "Project Message Of The Day (MOTD)"
source_url: https://docs.rundeck.com/docs/manual/projects/project-motd.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Project Message Of The Day (MOTD)

A MOTD file is a great way to make an announcement to the project's users. The MOTD content is interpreted as [markdown](http://commonmark.org/help/) text letting you format your text and embed images and links.

## Graphical Interface

To edit the project Message of the Day follow this navigation path. ![MOTD Menu Selection](https://docs.rundeck.com/docs/assets/img/motd-menu-item.png)

Enter the text that needs to be shared with users of this project and click Save. ![Figure: Project motd](https://docs.rundeck.com/docs/assets/img/motdgui02.png)

From **Project Settings \> Edit Configuration \> GUI** choose where the Message of the Day will be displayed. ![Figure: Project motd](https://docs.rundeck.com/docs/assets/img/motdgui01.png)

The Message of the Day will be shown when a user has access to that project. ![Figure: Project motd](https://docs.rundeck.com/docs/assets/img/motdgui03.png)

## CLI Usage

Update the motd with the [rd-cli](https://docs.rundeck.com/docs/manual/command-line-tools/rd.html) tool.

<div class="language-bash line-numbers-mode">

``` bash
rd projects readme put -p MyProject --motd -t "This is the **motd** for MyProject"
```

</div>

Now, you must add a property to set where to show the motd message, these options are `projectList` to show it in the main list of projects, `projectHome` to show it in the project view, or `navbar` to have a button in the navigation bar to display the motd at will, you could add more than one option as comma separated attributes:

Example to show that motd in the project list and the main project

<div class="language-text line-numbers-mode">

``` text
rd projects configure update -p MyProject -- --project.gui.motd.display=projectList,projectHome
```

</div>

## API Usage

[Project motd/motd modification](https://docs.rundeck.com/docs/api/#project-motd-file)

As we saw above, setting the motd using the GUI is the easiest way, less used is the API, but you can accomplish the same as by GUI or rd-cli, using below example:

<div class="language-text line-numbers-mode">

``` text
PUT /api/35/project/myproject/motd.md
Content-Type: text/plain
"This is the **motd** for MyProject"
```

</div>

## Filesystem

If using the *filesystem* storage type only, you can create the file in the project base directory:

- launcher: \$RDECK_BASE/projects/{project}/motd.md
- rpm/deb: /var/rundeck/projects/{project}/motd.md

If using the *db* storage type, use the GUI, the [CLI](https://docs.rundeck.com/docs/manual/command-line-tools/rd.html) or [API](#api-usage).
