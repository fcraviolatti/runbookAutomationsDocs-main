---
title: "Import/Export Calendars"
source_url: https://docs.rundeck.com/docs/manual/calendars/import-export.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Import/Export Calendars

Project calendars can be exported on the projectâ€™s export archive. If Calendar feature is enabled, you will see a checkbox where you can enable the calendar export.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-project-export.png" alt="Project Export" />
<figcaption aria-hidden="true">Project Export</figcaption>
</figure>

Also, for import project archive, you will see a checkbox where you can define if you want to import the calendars from an archive file.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-project-import.png" alt="Project Export" />
<figcaption aria-hidden="true">Project Export</figcaption>
</figure>

## Export Calendar on Job Definition

When you export a job that is associated with a specific Project Calendar, the job definition will include the list of calendars by name.

When you import the job on another rundeck instance or project, if an existing project calendar doesnâ€™t match with the calendar name, a warning will be displayed. Otherwise, the named calendar will be updated to apply to the Job.

<div class="language-xml line-numbers-mode">

``` xml
<joblist>
  <job>
    <calendars>
      <calendar name='New Calendar' />
      <calendar name='CleanUp March' />
    </calendars>
    <defaultTab>nodes</defaultTab>
    <description></description>
    <executionEnabled>true</executionEnabled>
    <id>553c7ea3-918d-4923-a049-4fe387664715</id>
    <loglevel>INFO</loglevel>
    <name>test-scheduled3</name>
    <nodeFilterEditable>false</nodeFilterEditable>
    <plugins />
    <schedule>
      <month month='*' />
      <time hour='12' minute='50' seconds='0' />
      <weekday day='*' />
      <year year='*' />
    </schedule>
    <scheduleEnabled>true</scheduleEnabled>
    <sequence keepgoing='false' strategy='node-first'>
      <command>
        <exec>ls -lrt</exec>
      </command>
    </sequence>
    <uuid>553c7ea3-918d-4923-a049-4fe387664715</uuid>
  </job>
</joblist>
```

</div>
