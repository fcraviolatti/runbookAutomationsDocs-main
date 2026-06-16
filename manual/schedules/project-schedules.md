---
title: "Project Schedules (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/schedules/project-schedules.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Project Schedules (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

Project Schedules allow you to define Schedules independently of Jobs. Schedules can apply to any Jobs in the Project. Schedule definitions can be exported into, and imported from, Project Archives.

> **Tips**
>
> Currently only project admins will be able to access the Schedules module. In a future release there will be more granular ACL based access assigned.

## Usage

In the Project Sidebar navigation there is now a link called **Schedules**:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-sidebar.png" alt="Project Schedules Sidebar" />
<figcaption aria-hidden="true">Project Schedules Sidebar</figcaption>
</figure>

You can click **New Schedule** to create a new Schedule:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-create-form.png" alt="New Schedule" />
<figcaption aria-hidden="true">New Schedule</figcaption>
</figure>

Enter a **Name**, and optional **Description**.

### Retain Schedules

For jobs developed without Project Schedules assigned to them, the schedules may become disconnected from those jobs when importing them via SCM or other methods. The **`Retain Schedules`** checkbox is used to maintain job-to-schedule associations currently assigned when a job is imported without schedules. To retain the schedule assignment when importing a job, check this box.

> **Additional Clarification**
>
> This feature was introduced in version `5.2.0`. For backwards compatibility leave the checkbox off (default). If schedules are being disconnected from jobs upon import and that behavior is not desired, check the box for each schedule where jobs should remain scheduled.
>
> This has no impact on schedules configured directly on the job, only Project Schedule associations.

### Schedules

Under **Schedule** you can choose *Simple* or *Crontab*, exactly like Job Schedules.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-create-crontab.png" alt="Schedule Crontab" />
<figcaption aria-hidden="true">Schedule Crontab</figcaption>
</figure>

> **Tips**
>
> For crontab format, see [this tutorial](http://www.quartz-scheduler.org/documentation/quartz-2.2.2/tutorials/tutorial-lesson-06.html)
>
> There is also a helpful crontab expression builder [here](https://www.freeformatter.com/cron-expression-generator-quartz.html)

Optionally enter a **Time Zone**.

Click **Save**.

The Schedule will appear in the list:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-list.png" alt="Schedule List" />
<figcaption aria-hidden="true">Schedule List</figcaption>
</figure>

## Schedule Actions

The Actions menu for a Schedule will show these options:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-action-menu.png" alt="Action Menu" />
<figcaption aria-hidden="true">Action Menu</figcaption>
</figure>

### Edit Schedule

Select **Edit Schedule** to modify the definition.

### Assign to Job

Select **Assign To Job** to choose jobs that the Schedule applies to.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-assign-jobs.png" alt="Assign Jobs to Schedule" />
<figcaption aria-hidden="true">Assign Jobs to Schedule</figcaption>
</figure>

Assigned jobs will be shown on the left, and available jobs will be shown on the right. You can search for jobs using the search fields to search by name or group.

Click on a Job to assign it to the Schedule.

Click **Unassign** to unassign an assigned Job.

Click **Set Job Options...** on an assigned Job to enter Option values to run the Job.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-set-job-options.png" alt="Set Job Options" />
<figcaption aria-hidden="true">Set Job Options</figcaption>
</figure>

You can enter options in the form `-optname value` separated by spaces. Click **Save** to save the Job option values.

These values will be used when the schedule is triggered, instead of the default option values set in the Job Options.

Click **Save** to save the Job assignments.

The Schedule List will indicate how many Jobs are assigned to the Schedule. You can click on the Schedule to see the list of assigned Jobs.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-assigned-job-list.png" alt="Assigned Job List" />
<figcaption aria-hidden="true">Assigned Job List</figcaption>
</figure>

### Download Schedule

Select **Download Schedule** to download a YAML formatted file containing the Schedule Definition.

See [Schedule Definition](#schedule-definition).

### Delete Schedule

Select **Delete Schedule** to delete the Schedule.

## Upload Schedule

Click **Upload Schedule** to upload a YAML schedule definition.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-upload-schedule.png" alt="Upload Schedule" />
<figcaption aria-hidden="true">Upload Schedule</figcaption>
</figure>

## Bulk Delete

If you want to delete multiple schedules, you can click the **Bulk Delete** button above the Schedule List.

Select one or more schedules and choose **Delete Selected Schedules**.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/project-schedules-bulk-delete.png" alt="Bulk Delete" />
<figcaption aria-hidden="true">Bulk Delete</figcaption>
</figure>

## Schedule Definition

Schedules can be defined in YAML format as shown below. Multiple schedules can be included in a single file.

<div class="language-yaml line-numbers-mode">

``` yaml
- description: every day at noon
  id: 166
  name: Noon refresh
  project: schedules-demo
  schedule:
    dayOfWeek: MON,TUE,WED,THU,FRI
    hour: '12'
    minute: '00'
    month: JAN,APR
  timeZone: ''
  type: SIMPLE
- crontabString: 0 */5 * ? * * *
  description: every 5 minutes
  id: 167
  name: Test
  project: schedules-demo
  timeZone: ''
  type: CRON
```

</div>

`name`: Schedule name (required)

`description`: Description (optional)

`timeZone`: Time Zone string (optional). Either an abbreviation such as "PST", a full name such as "America/Los_Angeles", or a custom ID such as "GMT-8:00".

`type`: either `CRON` or `SIMPLE`.

`crontabString`: Required if the `type` is `CRON`, specifies the [crontab format](http://www.quartz-scheduler.org/documentation/quartz-2.2.2/tutorials/tutorial-lesson-06.html)

`schedule`: Required if the `type` is `SIMPLE`, specifying `hour`,`minute`,`month`, and `dayOfWeek`:

- `hour`: Hour of day
- `minute`: Minutes in hour
- `dayOfWeek`: Either `*` for all days, or comma separated list of three-letter day abbreviations. `SUN,MON,TUE,WED,THU,FRI,SAT`
- `month`: Either `*` for all months, or comma separated list of three-letter month abbreviations. `JAN,FEB,MAR,APR,MAY,JUN,JUL,AUG,SEP,OCT,NOV,DEC`

## Feature Flag

To disabled the Project Schedules feature, add the following settings to rundeck-config.properties

<div class="language-properties line-numbers-mode">

``` properties
rundeck.feature.projectSchedules.enabled=false
```

</div>
