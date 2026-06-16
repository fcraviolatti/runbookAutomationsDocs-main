---
title: "Plugin Control"
source_url: https://docs.rundeck.com/docs/manual/projects/plugin-control.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Plugin Control

By default all plugins are enabled for each project. You may need to restrict access to plugins for certain projects.

Only enabled plugins are visible to job writers in the Job Edit page.

## Graphical Interface (Commercial)

The Plugin Control page lets you enable and disable specific plugins.

Go to the "Project Settings" and then choose "Plugins Control" menu item.

Uncheck any plugin you wish to disable.

## CLI Usage

Use the `rd projects configure set` command to define the `disabled.plugins` property.

<div class="language-bash line-numbers-mode">

``` bash
rd projects configure set -p MyProject -- \
   --disabled.plugins=pluginA,pluginB
```

</div>

## API Usage

Project configuration can be achieved via the [API](https://docs.rundeck.com/docs/api/).

[Project configuration](https://docs.rundeck.com/docs/api/#project-configuration)

    PUT /api/13/project/MyProject/config
    Content-Type: application/json

    {
        "disabled.plugins":"pluginA,pluginB"
    }
