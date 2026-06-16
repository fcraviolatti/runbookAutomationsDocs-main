---
title: "Project Delete"
source_url: https://docs.rundeck.com/docs/manual/projects/project-delete.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Project Delete

## Graphical Interface

From the navigation bar choose "Project Settings" and then "Delete Project". You will be asked confirmation before the project is removed.

## CLI Usage

Use the `rd projects delete` command to remove the project. The `--confirm` flag avoids an interactive check.

<div class="language-bash line-numbers-mode">

``` bash
rd projects delete -p MyProject --confirm
```

</div>

## API Usage

Project deletion can be achieved via the [API](https://docs.rundeck.com/docs/api/).

[Delete projects](https://docs.rundeck.com/docs/api/#project-deletion):

    DELETE /api/13/project/MyProject
