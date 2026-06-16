---
title: "Job Execution with Enterprise Runners"
source_url: https://docs.rundeck.com/docs/administration/runner/using-runners/runner-using.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Using Enterprise Runners in Jobs

## Automatic Runner Selection for Job Execution

When a Project is configured to use **Automatic** for the [**Project Dispatch Configuration**](https://docs.rundeck.com/docs/administration/runner/runner-management/project-dispatch-configuration.html), the system will automatically select the Runners to use for Job execution based on the mapping of nodes to Runners as configured in the [Node Dispatch](https://docs.rundeck.com/docs/administration/runner/runner-management/node-dispatch.html) settings. This means that the Job definition does not require selecting a Runner, as the system will automatically choose the Runner based on the nodes that are targeted by the Job.

For example, if the Node Filter for a Job is defined as `region: "us-west-1,us-east-1"` and there are two Runners within this Project, one with a Node Filter of `region: "us-west-1"` and the other with a Node Filter of `region: "us-east-1"`, the system will automatically select the Runner with the `us-west-1` Node Filter for nodes that are targeted within US-WEST-1 and similarly for US-EAST-1.

## Manual Runner Selection for Job Execution

When a Project is configured to use **Manual** for the [**Project Dispatch Configuration**](https://docs.rundeck.com/docs/administration/runner/runner-management/project-dispatch-configuration.html), users must explicitly specify the Runners that can be used for the Job within the Job definition.

> **Single Environment per Execution Constraint**
>
> When **Manual** is selected, only a single Runner will be utilized for a given Job execution. This can be prohibitive when attempting to target multiple environments where those environments can only be accessed by using a Runner deployed in each environment.

#### Creating jobs with Manual Runner Selection

When the **Manual** is selected within the **Project Dispatch Configuration**, the Job edit menu will display a â€œNodes & Runnersâ€? tab where Node and Runner selection is configured for the job. When creating a job or editing a job, Runners can be selected based on tags with the following options:

![Options to select runners by tags](https://docs.rundeck.com/docs/assets/img/runner-use-options.png)  

- Selecting Runners with â€œChoose Tagsâ€? option from the drop-down list: ![Selecting runners by tags selection](https://docs.rundeck.com/docs/assets/img/runner-use-options-checkbox.png)
- Selecting Runners by â€œEnter a Tag Filterâ€? option and typing the Runner Tag name: ![Selecting remote runners with tag search ](https://docs.rundeck.com/docs/assets/img/runner-use-options-textinput.png)
- Selecting the â€œLocal Runnerâ€? option and choosing the Local runner: ![Select the local runner](https://docs.rundeck.com/docs/assets/img/runner-use-options-local.png)

#### Running Jobs with Manual Runner Selection

The â€œRunnerset Can be Changed at Runtimeâ€? option controls if the Runnerset selection can be changed when running a Job. If selected, a list of Runnersets will be presented in the Job invocation screen otherwise the Runnerset selected in the job definition during edit time will be used for job execution.  
![Allow runner selection at runtime](https://docs.rundeck.com/docs/assets/img/runner-use-options-changeatruntime.png)

A user can change which Runner will execute the job with the â€œChange the Target Runnerâ€?. This option is useful if you want to target different environments with the same job, for example running the same job in Dev or Staging environments that are setup with different Runners. This is possible only If the â€œRunnerset Can be Changed at Runtimeâ€? option was picked for this Job definition. If you check â€œChange the Target Runnerâ€? the same Runner selection UI as in the â€œEditing Jobâ€? will let you pick the Runner set.  
![Run job and pick a runner](https://docs.rundeck.com/docs/assets/img/runner-use-run-changeatruntime.png)

#### Dispatching to Nodes with Manual Runner Selection

Once you have picked a Runnerset for the Job, you can choose how the Runner should behave by selecting a Dispatch mode: â€œRun on Runnerâ€? or â€œDispatch to Nodes through Runnerâ€?. If you select â€œDispatch to Nodes through Runnerâ€?, the nodes related options will display and those are identical to previous versions of Runbook Automation.  
![Dispatching jobs through runners](https://docs.rundeck.com/docs/assets/img/runner-use-dispatch-nodes.png)

#### Manual Runner Selection through Job options

Runner matching and filtering supports Job Options - `${option.NAME}`, which allows changing the Runners for the job based on dynamic input through API calls or the rundeck-cli. The Job Options behavior is the same for Runner selection as with using it with commands or other workflow steps. For example:

- A job is configured with a Runner filter value set to `${option.runnerTagParameter}`
- At runtime (through cli or API calls) we are providing a job option named `runnerTagParameter=myRunnerXYZ`, which will parameterize the Job Option with `myRunnerZYZ` for that job execution.
- The job will be effectively executed with the Runner that is tagged with `myRunnerZYZ`

Here's an example of a job option and runner filter configurations:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/dynamic_runner_selection_jobOption.png" alt="Job Option" />
<figcaption aria-hidden="true">Job Option</figcaption>
</figure>

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/Dynamic_runner_selection_runnerFilter.png" alt="Runner Filter" />
<figcaption aria-hidden="true">Runner Filter</figcaption>
</figure>

#### Migrating Jobs to use Runners with Manual Runner Selection

When **Manual** is selected in [**Project Dispatch Configuration**](https://docs.rundeck.com/docs/administration/runner/runner-management/project-dispatch-configuration.html), existing jobs will default to the Local Runner even if no Runner selection is made in the job definition. The Local Runner operates with an execution context equivalent to that of the Runbook Automation service.

## Job Output with Manual Runner Selection

The runner carrying out the job execution is displayed at the top of the Job execution activity. Example below: The job below was executed through the â€œAnsible-Runnerâ€?  
![View runner in a job execution](https://docs.rundeck.com/docs/assets/img/runner-use-view-activity.png)
