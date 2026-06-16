---
title: "Jira Dynamic Option Plugins (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/option-plugins/jira.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Jira Dynamic Option Plugins (Commercial)

The Jira Dynamic Option Plugins can provide dynamic lists as Option Inputs for your workflows.

Each option value requires specific settings in the Project Configuration settings.

1.  After loading your project navigate to **Project Settings \> Edit Configuration**
2.  Click **Edit Configuration** button in Upper Right
3.  Use the settings below to configure the plugin(s)

> Note: the `.project` settings are configured with the Project ID for the related JIRA project.

To use these plugins, add an Option to your Job and select the Allowed Values list entry.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/jira-options.png" alt="JIRA Dynamic Options" />
<figcaption aria-hidden="true">JIRA Dynamic Options</figcaption>
</figure>

### Project Configuration Settings

- List of Issues in a Project

Project Settings

<div class="language-text line-numbers-mode">

``` text
project.plugin.OptionValues.jira-option-values.login=login
project.plugin.OptionValues.jira-option-values.passwordStoragePath=keys/jira/pass
project.plugin.OptionValues.jira-option-values.project=JiraProject
project.plugin.OptionValues.jira-option-values.url=https\://test.atlassian.net
```

</div>

- Issue Types Option (list issue types):

Project settings

<div class="language-text line-numbers-mode">

``` text
project.plugin.OptionValues.jira-issue-types-option-values.login=login
project.plugin.OptionValues.jira-issue-types-option-values.passwordStoragePath=keys/jira/pass
project.plugin.OptionValues.jira-issue-types-option-values.project=JiraProject
project.plugin.OptionValues.jira-issue-types-option-values.url=https\://test.atlassian.net
```

</div>

- Issue Transition Option (list transition types):

Project settings

<div class="language-text line-numbers-mode">

``` text
project.plugin.OptionValues.jira-transition-option-values.login=login
project.plugin.OptionValues.jira-transition-option-values.passwordStoragePath=keys/jira/pass
project.plugin.OptionValues.jira-transition-option-values.project=JiraProject
project.plugin.OptionValues.jira-transition-option-values.url=https\://test.atlassian.net
```

</div>
