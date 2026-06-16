---
title: "AI-Generated Runbooks (Beta)"
source_url: https://docs.rundeck.com/docs/manual/jobs/ai-generated-runbooks.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# AI-Generated Runbooks (Beta)

> **Beta Feature**
>
> This feature is still in beta and therefore the behavior and performance of this feature is not guaranteed.

**AI-Generated Runbooks** provides an AI-enhanced approach to creating new automation Jobs. Through natural-language prompts, users can generate the baseline starting-point for the Job definition.

![Job Preview](https://docs.rundeck.com/docs/assets/img/ai-gen-rba-job-preview.png)  

The AI-Generated Runbooks feature helps new users get started with Runbook Automation. Through example prompts, new users quickly learn the types of use-cases that Runbook Automation is suited to address.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/ai-gen-rba-example-prompt.png" alt="Example Prompts Provide Context to New Users" />
<figcaption aria-hidden="true">Example Prompts Provide Context to New Users</figcaption>
</figure>

  
AI-Generated Runbooks also helps experienced authors of Jobs by reducing the time spent creating the Job definition and searching through third-party technical documentation.

## How to Enable AI-Generated Runbooks

> **Product Availability**
>
> The *AI-Generated Runbooks* feature is only available in Runbook Automation SaaS. It is not available in Runbook Automation Self-Hosted. New users and current Runbook Automation customers are encouraged to [start a trial](https://www.pagerduty.com/sign-up/runbook-automation/) of Runbook Automation to try out the *AI-Generated Runbooks* feature.

To enable *AI-Generated Runbooks*:  

1.  Navigate to the AI Manager through the System Menu (gear icon in the upper-right): ![AI Manager Menu](https://docs.rundeck.com/docs/assets/img/ai-manager-menu.png)
2.  Click the checkbox to `**Enable AI Generated Runbooks**`
3.  Select the projects where the feature should be enabled: ![Enable in Projects](https://docs.rundeck.com/docs/assets/img/enable-ai-in-project.png)
4.  Click **Save**.

> **First Time Configuration**
>
> While the feature is still in beta, users will be asked to review and agree to the beta feature Terms & Conditions. Only **App Admins** users are allowed to agree to the beta Terms & Conditions.

## Using AI-Generated Runbooks

To use *AI-Generated Runbooks*:  

1.  Navigate to the **Jobs** tab.
2.  Click on **Generate Job**: ![Generate Job](https://docs.rundeck.com/docs/assets/img/jobs-page-generate-job.png)
3.  Select from the example prompts, or type in a custom prompt for a task to be automated through Runbook Automation: ![Typing in Prompt](https://docs.rundeck.com/docs/assets/img/ai-gen-rba-example-prompt.png)
4.  Click on **Generate Job**. This will generate a Job Preview: ![Job Preview](https://docs.rundeck.com/docs/assets/img/ai-gen-rba-job-preview.png)
5.  Review the Job Preview. If the generated Job is insufficient, either click **Discard** or type in a new prompt. Otherwise, click on **Continue to Job Editor**.
6.  From the Job editor, modify the Job definition as needed and then click **Create**.

> **Error Messages**
>
> Users may encounter the following error message:
>
> 1.  **`The result data had a problem. You may need to retry your request shortly.`**
>
> In this circumstance, it is ok to retry the same prompt again and with minimal wait time after the error message appears.

### Job Review Best Practices

Since the content of the Job is generated using a large-language model, it is best-practice to review the generated content for accuracy. Once reviewed and adjusted, it is also best-practice to test the Job in a non-production environment. These best practices are presented to the user when the Job is created using *AI-Generated Runbooks*: ![Generated Job Best Practices](https://docs.rundeck.com/docs/assets/img/ai-gen-rba-created-job.png)  

## AI Model and Security

*AI-Generated Runbooks* is powered by a combination of a large-language generative AI model and [prompt-engineering](https://en.wikipedia.org/wiki/Prompt_engineering).

Through this configuration, **the only data sent to the generative AI model is the text entered into the prompt field.** No other data about your environment, existing Jobs or the source of the prompt is sent to the AI model. Furthermore, **the AI model is not trained on the text entered into the prompt.**

For further questions about the AI Model and security, please [contact support](https://docs.rundeck.com/docs/about/getting-help.html).

## Current Limitations

The current *AI-Generated Runbooks* feature is trained to generate a full, multi-step Job - including Job Options and Secret Job Options.

However, the generated content does not yet produce:

1.  Node Filter
2.  Runner configuration
3.  Log Filters (and passing data between steps)
4.  Schedules
5.  Notification Plugins
6.  ROI Metric configuration

These features will be produced by *AI-Generated Runbooks* in future releases.
