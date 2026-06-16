---
title: "Progress Badge (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/log-filters/progress-badge.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Progress Badge (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

This log filter changes the log output of the steps in a jobâ€™s activity logs by displaying user-specified text and "Status Symbols" (emoticons), as well as optionally not displaying log returns. The chosen text and status-symbol can be dependent on the "raw" log-output of the given job step.

One of the most common use-cases for the Progress Badge is to simplify the verbose output of diagnostics - such as application logs - into content that is consumable by first-responders of incidents.

![PG Output](https://docs.rundeck.com/docs/assets/img/progress-badge-output.png)  

## Usage

To add the Progress Badge to a job step:

1.  Click the **gear** icon in the upper-right of the job step: ![Select Log Filter](https://docs.rundeck.com/docs/assets/img/add-log-filter.png)
2.  Click on **Progress Badge** and fill in the fields outlined below:

**Regex**: Optional regex to search the log returns for. If this field is set, the badge will only appear if the regex finds a match.

**Text**: The text to be placed in the log-output.

**Status Symbol**: Optional emoticon to append to the text in the log-output.

> **Status Symbol Support**
>
> For users that are self-hosting Runbook Automation, in order for Job definitions to support the Status Symbols, the database must support 4-Byte characters. As noted [here](https://docs.rundeck.com/administration/configuration/database/mysql), MySQL 5.7 does not enable 4-Byte character support by default.  
> This can be enabled by adding the following to `my.cnf` (Linux) or `my.ini` (Windows):
>
> <div class="language-text line-numbers-mode">
>
> ``` text
> [mysqld]
> character_set_server = utf8mb4
> ```
>
> </div>
>
> Without 4-Byte character support, an error will appear when attempting to save the Job definition that has a Status Symbol selected:  
> `Hibernate operation: could not execute statement; SQL [n/a]; (conn=74878) Incorrect string value: '\xE2\x9C\x85"`

**Context Variable**: The name of a context-variable that can be referenced in subsequent steps. For example, if `http_status` placed here, then the text plus emoticon will be referencable as `${data.http_status}` in subsequent job steps.

### Optional advanced configuration settings:

**Mute**: True/False with Conditional Disable option. If true, log output will be replaced by the badge.

**Conditional**: Disable option will only show the badge if the String regex matches. (Useful when configuring multiple Progress Badges for the same result for â€œRed/Greenâ€? style notifications.)

**Typeface**: Specify font for the badge - uses typical HTML/CSS typeface rules.

**Font Size**: Font size of the text on the badge. All standard CSS options are available - â€œ%â€?, â€œpxâ€?, â€œptâ€?, or â€œem.â€?

**Background Color**: Select from the predefined pulldown list, or enter a valid CSS value in the text box - either standard colors, or hex values.

### Custom Emoticon Support

To use custom emoticons inside the text field, input the alias of the emoticon between two colons: `:smile: Successfull job! :100:` Display as:

`ðŸ˜„ Successfull job! ðŸ’¯`

A full list of supported emoji are listed here: [vdurmont/emoji-java](https://github.com/vdurmont/emoji-java)

## Example: Simplified HTTP Diagnostics

In this scenario, Runbook Automation is used to check on an HTTP endpoint and inform the user whether the HTTP response is "healthy" or "unhealthy." The Progress Badge is used to simplify the output of the HTTP diagnostics.

1.  Add a Job Option `endpoint-to-check`. This will be the URL that is queried for an HTTP response.
2.  Add a **Remote Command** job step and use the command:
    <div class="language-text line-numbers-mode">

    ``` text
    curl -I ${option.endpoint-to-check}
    ```

    </div>
3.  Add the **Progress Badge** Log Filter, as described [above](#usage).
4.  Insert the following into the **Regex** field: **`HTTP/.*(200).*`**
5.  Insert "Healthy" into the **Text** field.
6.  Select the green check-mark emoticon for the **Status Symbol**.
7.  Insert the following into the **Context Variable** field **`simplified-response`**:

![](https://docs.rundeck.com/docs/assets/img/completed-progress-badge.png)

1.  Add *another* **Progress Badge** Log Filter to the same step.
2.  Insert the following into the **Regex** field: **`HTTP/.*(400|404|500|504|301).*`**
3.  Insert "Unhealthy" into the **Text** field.
4.  Select the red **X** emoticon for the **Status Symbol**.
5.  Insert the following into the **Context Variable** field: **`simplified-response`**.

![](https://docs.rundeck.com/docs/assets/img/progress-badge-unhealthy.png)

Now, when a URL returns a **`200`**, the simplified message will be displayed alongside the verbose HTTP response: ![PG Output](https://docs.rundeck.com/docs/assets/img/progress-badge-output.png)

This simplified output can then be sent to other tools, such as PagerDuty Incident Response. First, add the **PagerDuty / Incident / Note** job step: ![PagerDuty Step](https://docs.rundeck.com/docs/assets/img/progress-badge-pd-step.png)  
  
Then, when the job is invoked, the **Text** plus **Status Symbol** will appear on the Incident Timeline: ![PD Timeline](https://docs.rundeck.com/docs/assets/img/progress-badge-pd-timeline.png)
