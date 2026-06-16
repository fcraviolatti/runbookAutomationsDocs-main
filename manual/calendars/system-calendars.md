---
title: "System Calendars"
source_url: https://docs.rundeck.com/docs/manual/calendars/system-calendars.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# System Calendars

Go to the system menu and select the option `Calendars`

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-system-menu.png" alt="System Menu" />
<figcaption aria-hidden="true">System Menu</figcaption>
</figure>

You will see a list of existing calendars and you will have the option to add calendars.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-system-home.png" alt="Calendars System Home" />
<figcaption aria-hidden="true">Calendars System Home</figcaption>
</figure>

### Create Calendar

Click on `+ Add Calendar` button and you will see form to add a new calendar

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-create-form.png" alt="Create Calendar" />
<figcaption aria-hidden="true">Create Calendar</figcaption>
</figure>

- **Name**: Name of the calendar
- **Description**: (Optional) Description of the calendar
- **Enabled**: define if the calendar is enabled
- **Mode**: Blackout, Allowed
- **Type**: Date, Daily, Monthly, Range

If the required fields are not set, the form will display the errors.

#### Types

There are different types of calendars to define how to set the target days/hours that the calendar will cover.

**Calendar Dates**  
Pick up a list of days where the calendar will be used, eg: 12/25/2020, 12/31/2020

**Repeat dates yearly**: if this box is checked, the calendar will be triggered every year on the selected dates. If the box is *not* checked, the selected dates will apply only to the selected year.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-date-type.png" alt="Calendar Dates" />
<figcaption aria-hidden="true">Calendar Dates</figcaption>
</figure>

**Times of Day**  
Defines the times of day when the calendar will be applied, eg: `08:00 - 17:00`

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-date-daily.png" alt="Times of Day" />
<figcaption aria-hidden="true">Times of Day</figcaption>
</figure>

**Days of the Month**  
List of days of the month where the calendar will be applied, eg: 30,31

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-date-monthly.png" alt="Days of the Month" />
<figcaption aria-hidden="true">Days of the Month</figcaption>
</figure>

**Date Range**  
Range of days where the calendar will be applied: `24/11/2020 - 26/11/2020`

**Repeat dates yearly**: if this box is checked, the calendar will be triggered every year on the selected dates. If the box is *not* checked, the selected dates will apply only to the selected year.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-date-range.png" alt="Date Range" />
<figcaption aria-hidden="true">Date Range</figcaption>
</figure>

**Days of the Week**  
Choose multiple days of the week

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-days-of-the-week.png" alt="Days of the Week" />
<figcaption aria-hidden="true">Days of the Week</figcaption>
</figure>

#### Related projects

In the **Projects** section you can define if the calendar will be used for all Projects or specific Project. By default, the calendar will not be assigned to any projects.

Select a project from the list and click the "Add Project" button.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-system-project-selector.png" alt="Project Selector" />
<figcaption aria-hidden="true">Project Selector</figcaption>
</figure>

Or, check the "Apply this Calendar to all Projects" checkbox, and it will be assigned to all Projects.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-system-selector.png" alt="Projects Section" />
<figcaption aria-hidden="true">Projects Section</figcaption>
</figure>

Finally, click "Save", and the Calendar will be created and shown in the list.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-create-form-saved.png" alt="Calendar Saved" />
<figcaption aria-hidden="true">Calendar Saved</figcaption>
</figure>

Now, on the jobs page inside a project, new icons will be displayed for the scheduled jobs that has been modified for a calendar.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-job-list.png" alt="Job List" />
<figcaption aria-hidden="true">Job List</figcaption>
</figure>

For each job you can review the list of calendars that are related with it.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/calendars-job-detail.png" alt="Job Detail" />
<figcaption aria-hidden="true">Job Detail</figcaption>
</figure>
