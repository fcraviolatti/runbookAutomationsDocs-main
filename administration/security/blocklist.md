---
title: "Plugin Blocklist"
source_url: https://docs.rundeck.com/docs/administration/security/blocklist.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Plugin Blocklist

The Plugin Blocklist can be used when plugins need to be blocked or prevented from being installed or used for security or other use-case situations. To use the plugin blocklist, you will need to create a blocklist yaml file in the following format:

<div class="language-yaml line-numbers-mode">

``` yaml
fileNameEntries:
    - rundeckpro-plugin-jar-name
    - rundeckpro-plugin-jar-name
    - rundeckpro-plugin-jar-name
providerNameEntries:
   ProviderService:
      - provider-name
      - provider-name
```

</div>

> **Tips**
>
> Even if one section is blank, it must still be declared.

**fileNameEntries**: fileNameEntries will prevent entire plugin jars from being copied into the libext folder during setup/installation. For example. if you want to block every single rundeck Jira plugin, you would replace rundeckpro-plugin-jar-name with `rundeckpro-jira`. Keep in mind that you can still add plugins using the GUI or by putting the plugin (JAR file) right into the `/rundeck/libext folder`.

*Example using fileNameEntries:*

<div class="language-yaml line-numbers-mode">

``` yaml
fileNameEntries:
    - rundeckpro-jira-plugins
providerNameEntries:
    none:
```

</div>

File name entries can be found on `rundeck/libext`.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/blocklist-filename.png" alt="Plugins File Names" />
<figcaption aria-hidden="true">Plugins File Names</figcaption>
</figure>

Use only the plugin file name without the version or file extension as shown in the previous example.

**providerNameEntries**: providerNameEntries allows more granular customization. Instead of blocking the whole plugin jar, it will only block the specified plugin. For example, to block a single plugin, the Jira comment issue step, you would add `WorkflowStep` as the providerService and `jira-comment-issue-step` as the provider-name. This is a good option if you need to block a plugin that is bundled in a jar with a plugin you need.

Example using providerNameEntries:

<div class="language-yaml line-numbers-mode">

``` yaml
fileNameEntries:
  - none
providerNameEntries:
    WorkflowStep:
        - jira-comment-issue-step
```

</div>

Provider names can be found by navigating to the System Menu \> Plugins \> Installed Plugins. Click on the information icon for the plugin and find the provider name in the upper left.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/blocklist-providername.png" alt="Provider Name" />
<figcaption aria-hidden="true">Provider Name</figcaption>
</figure>

Once the providers are all listed, add the following config entry to rundeck-config.properties with the path to the file just created: `rundeck.plugins.providerBlockListFile=/path/to/user/blocklist`

If the plugin was correctly blocked with the providerNameEntries you will see the following messages:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/blocklist-console-message.png" alt="On Console" />
<figcaption aria-hidden="true">On Console</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/blocklist-gui-message.png" alt="On GUI" />
<figcaption aria-hidden="true">On GUI</figcaption>
</figure>
