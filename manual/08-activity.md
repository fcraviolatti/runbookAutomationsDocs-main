---
title: "Activity"
source_url: https://docs.rundeck.com/docs/manual/08-activity.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Activity

Execution history for commands and Jobs is stored by the Rundeck server. Execution history can be filtered and viewed inside the "Activity" page.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0211.png" alt="Activity page" />
<figcaption aria-hidden="true">Activity page</figcaption>
</figure>

## Filtering Activity

By default, the Activity page will list running executions and history recent executions. The page contains a filter control that can be used to expand or limit the executions.

The filter form contains a number of fields to limit search:

- Within: Time range. Choices include 1 day, 1 week, 1 month or other (given a start after/before to ended after/before).
- Job Name: Job title name.
- User: User initiating action.
- Filter: The node filter used . You can enter just one node name to see if was executed against that node or use the node filter formats. Refer to the [User Guide - Node Filters](https://docs.rundeck.com/docs/manual/11-node-filters.html) Documentation.
- Ad hoc command: Command typed into the command bar or via `dispatch`.
- Result: Success or failure status.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0212.png" alt="History filter form" />
<figcaption aria-hidden="true">History filter form</figcaption>
</figure>

After filling the form pressing the "Filter" button, the page will display executions matching the search.

## Activity in PagerDuty Runbook Automation Self-Hosted Home

On the home page, users can check activity for a specific project, such as failed executions for each project.

> **Warning**
>
> Only the **failed** executions will display, excluding "missed" and other status.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/rundeckHome.png" alt="Project Activity on home page (dark mode)" />
<figcaption aria-hidden="true">Project Activity on home page (dark mode)</figcaption>
</figure>

## Extended date range

It is also possible to search for activity between dates. Press the "Other..." menu choice to bring up the form.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0217.png" alt="Extended date range search" />
<figcaption aria-hidden="true">Extended date range search</figcaption>
</figure>

## Saving the filter

Filters can be saved to a menu that makes repeating searches more convenient. Click the "save this filter..." link to save the filter configuration.

## Execution listings

Information for each execution contains the command or Job executed, options, success status and a link to a file containing all the output messages.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0213.png" alt="Execution view" />
<figcaption aria-hidden="true">Execution view</figcaption>
</figure>

If any errors occurred, the "Node Failure Count" column will show the number of nodes in red text. A bar chart indicates the percent failed.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0216.png" alt="Execution view" />
<figcaption aria-hidden="true">Execution view</figcaption>
</figure>

You can find below the possible **Execution Status** an Execution can assume in Runbook Automation.

| **Status**        | **Icon**                                                            | **Colour** | **Description**                                                                                                                                                                                                                                                                                                                                                 |
|-------------------|---------------------------------------------------------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SCHEDULED         | ![Clock](https://docs.rundeck.com/docs/assets/img/569667.png)       | Cyan       | Status when a job is scheduled to be executed - [Project Schedules (Commercial)](https://docs.rundeck.com/docs/manual/schedules/project-schedules.html). Project Schedules allow you to define Schedules independently of Jobs. Schedules can apply to any Jobs in the Project. Schedule definitions can be exported into, and imported from, Project Archives. |
| QUEUED            | ![Stack](https://docs.rundeck.com/docs/assets/img/569745.png)       | Blue       | Status when [Job Queue (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-queue.html) is enabled and the job is queued. Job Queuing allow jobs to run a single execution at a time, but accepting new executions and placing them in a queue, to run them sequentially in the order they were created.                                                 |
| SUCCEEDED         | ![Succeed](https://docs.rundeck.com/docs/assets/img/569728.png)     | Green      | Status when the entire runbook was successfully executed on all nodes.                                                                                                                                                                                                                                                                                          |
| RUNNING           | ![Running](https://docs.rundeck.com/docs/assets/img/569935.png)     | Cyan       | Status when the runbook is being executed.                                                                                                                                                                                                                                                                                                                      |
| ABORTED           | ![Aborted](https://docs.rundeck.com/docs/assets/img/569726.png)     | Grey       | Status when the job execution has been aborted manually (GUI or via API)                                                                                                                                                                                                                                                                                        |
| TIMED OUT         | ![Clock](https://docs.rundeck.com/docs/assets/img/569667.png)       | Orange     | The execution of the job has timed out as per [the definition](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html#timeout)                                                                                                                                                                                                                            |
| FAILED            | ![Failed](https://docs.rundeck.com/docs/assets/img/569726.png)      | Red        | Status when the execution of the runbook failed in one or more nodes - Dependent on settings and [definition of failure](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html#node-dispatching-and-filtering)                                                                                                                                           |
| FAILED-WITH-RETRY | ![FailedRetry](https://docs.rundeck.com/docs/assets/img/569674.png) | Orange     | When the [Job Retry Failed Nodes (Commercial)](https://docs.rundeck.com/docs/manual/jobs/job-retry-failed-nodes.html) plugin is enabled for a job, with retry options set, the plugin will review the previous execution's list of succeeded nodes and will just select on the next execution the nodes that either failed or were not started.                 |
| MISSED            | ![Clock](https://docs.rundeck.com/docs/assets/img/569667.png)       | Red        | Status when [Missed Job Fires (Enterprise Only)](https://docs.rundeck.com/docs/manual/schedules/missedjobfires.html) is enabled and one of the jobs doesn't run at the time when it was scheduled to run.                                                                                                                                                       |
| OTHER-INCOMPLETE  | ![Incomplete](https://docs.rundeck.com/docs/assets/img/569911.png)  | Orange     | Status when a job finishes with some nodes where some steps were not started                                                                                                                                                                                                                                                                                    |
| OTHER             | ![Other](https://docs.rundeck.com/docs/assets/img/569744.png)       | ORANGE     | Status when any other issue occurs during runbook execution                                                                                                                                                                                                                                                                                                     |

## RSS link

If configured, an RSS icon provides a link to an RSS view of the events that match the current filtering criteria.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0214.png" alt="RSS link" />
<figcaption aria-hidden="true">RSS link</figcaption>
</figure>

## Bulk Delete Executions

> **Tips**
>
> Old executions can be bound to old workflows stored in database just for information purposes, as a better practice, we recommend to clean periodically old executions in order to avoid slowness in the GUI or other problems related with the excesive amount of old records in the database.

If you have access, you can click the "Bulk Delete" button to enable bulk-edit mode.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig08-activity-bulk-delete.png" alt="Activity page bulk delete" />
<figcaption aria-hidden="true">Activity page bulk delete</figcaption>
</figure>

Select the Executions you want to delete by clicking on them. You can also click on the "Toggle all", "Select All" or "Select None" links to change the selection.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig08-activity-bulk-edit-mode.png" alt="Activity page bulk edit mode" />
<figcaption aria-hidden="true">Activity page bulk edit mode</figcaption>
</figure>

Click the "Delete Selected Executions", and confirm to delete the executions.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig08-activity-bulk-delete-confirm.png" alt="Activity page bulk delete confirm" />
<figcaption aria-hidden="true">Activity page bulk delete confirm</figcaption>
</figure>
