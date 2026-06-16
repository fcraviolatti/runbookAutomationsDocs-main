---
title: "Getting Started with Solutions"
source_url: https://docs.rundeck.com/docs/learning/solutions/getting-started.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Getting Started with Solutions

> **Prerequisites**
>
> To use any the Example Solutions, you must have a **PagerDuty Runbook Automation** (Self-Hosted or SaaS) instance available.
>
> If you do not have a license for either of these products, [contact us](https://www.pagerduty.com/contact-us/runbook-automation/) to learn more.
>
> **You must be running a [currently supported product version](https://docs.rundeck.com/docs/history/release-calendar.html) at a minimum.** Specific jobs may require specific product versions due to newer plugin releases. Those will be captured in the job's descriptions.
>
> New instances of Runbook Automation Cloud have the Solution installed and included by default. [Request a Trial here](https://www.pagerduty.com/sign-up/runbook-automation/)  

## Setup

For existing Runbook Automation environments, follow the steps below to download and import the Example Content:

### Download the **Automated Diagnostics Solution package**.

1.  [**Download the latest release of the Solution here**](https://github.com/rundeckpro/automated-diagnostics-project/releases/).
2.  Save the `automated-diagnostics.jar` file to your local machine for use in the next steps.

### Create a project in your Runbook Automation environment:

1.  Click the **P** in the upper left corner to navigate to the Main Dashboard  
      

2.  Click the blue **New Project+** button:  
    ![Add Project](https://docs.rundeck.com/docs/assets/img/solutions-auto-diag-add-project.png)  
      

3.  Copy the following into the **Project Name** field: **`automated-diagnostics`**  
    ![Name Project](https://docs.rundeck.com/docs/assets/img/solutions-name-project.png)

    > **Heads Up**
    >
    > Be sure to name the project **`automated-diagnostics`**. Otherwise, some of the prebuilt Jobs and Tours will not function properly.

4.  Provide a Label for a more "user-friendly" name - such as *Containers Solution*  
      

5.  Click the green **Create** button

### Import the archive file into your new project:

1.  In your new project, click the **gears** in the lower left corner for **Project Settings**  
      

2.  Choose **Import Archive** from the menu: ![Import Archive](https://docs.rundeck.com/docs/assets/img/solutions-auto-diag-import-archive.png)  
      

3.  For the **Choose a Rundeck archive**, select the **`automated-diagnostics.jar`** from the downloaded resources.  
      

4.  Leave all of the import settings as their defaults  
      

5.  Click the green **Import** button

    > **Note**
    >
    > The Tours in the Solution will help you prepare the project for the jobs included. Be sure to start there and name your project properly using the instructions above.  
    > If you are looking for a more general introduction to PagerDutyâ€™s Automation products, it is recommended to review the contents of the [Welcome Project](https://docs.rundeck.com/docs/learning/howto/welcome-project-starter.html).
