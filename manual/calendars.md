---
title: "Calendars"
source_url: https://docs.rundeck.com/docs/manual/calendars.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Calendars

> **Available in PagerDuty Runbook Automation Commercial products.**

This feature allows Rundeck to create Calendars at the System or Project level. Calendars define dates and times, and whether they these times are **blackout** or **allowed** for scheduled jobs.

Blackout Calendars  
Scheduled Jobs wonâ€™t run on the matching dates and times, but will run on other dates and times.

Allowed Calendars  
Scheduled Jobs are allowed to run on the matching dates and times, but not on any other dates and times.

> **Notes**
>
> - If calendars overlap the Blackout Calendars will take precedence and prevent the job from running.
> - Blackout Calendars are not considered [Misfired Jobs](https://docs.rundeck.com/docs/manual/schedules/missedjobfires.html).

Calendars can be defined at system level as *System Calendars* or project level as *Project Calendars*.

[System Calendars](https://docs.rundeck.com/docs/manual/calendars/system-calendars.html)  
Can be applied for all Jobs on all Rundeck Projects, or to all Jobs on selected Projects.

[Project Calendars](https://docs.rundeck.com/docs/manual/calendars/project-calendars.html)  
Will be applied for all Jobs on the project or only for selected Jobs in that Project.

### Disable Calendars feature

If there is a need to disable the calendars feature, add the following settings to rundeck-config.properties

<div class="language-properties line-numbers-mode">

``` properties
rundeck.feature.calendars.enabled=false
```

</div>

(Setting the value to 'true' or removing line will enable the feature.)

> **Tips**
>
> Note: This will not prevent manual execution of jobs. It will only affect scheduled jobs.
