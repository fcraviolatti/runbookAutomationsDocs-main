---
title: "Project README"
source_url: https://docs.rundeck.com/docs/manual/projects/project-readme.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Project README

A readme file is a great way to welcome your users and provide an overview about the project. The readme content is interpreted as [markdown](http://commonmark.org/help/) text letting you format your text and embed images and links.

## Graphical Interface

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-list-readme.png" alt="Figure: Project with Readme" />
<figcaption aria-hidden="true">Figure: Project with Readme</figcaption>
</figure>

### CLI Usage

Update the readme with some text.

<div class="language-bash line-numbers-mode">

``` bash
rd projects readme put -p MyProject -t "This is the **readme** for MyProject."
```

</div>

You might want to set the project home page to show the readme.

<div class="language-bash line-numbers-mode">

``` bash
rd projects configure set -p MyProject -- \
   --project.gui.readme.display=projectHome
```

</div>

## API Usage

[Project readme/motd modification](https://docs.rundeck.com/docs/api/#project-readme-file)

    PUT /api/13/project/MyProject/readme.md
    Content-Type: text/plain

    This is the **readme** for MyProject.

## Filesystem

If using the *filesystem* storage type only, you can create the file in the project base directory:

- launcher: \$RDECK_BASE/projects/{project}/readme.md
- rpm/deb: /var/rundeck/projects/{project}/readme.md

If using the *db* storage type, use the GUI, the CLI or [API](#api-usage).
