---
title: "ROI Metrics Data (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/roi-metrics.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# ROI Metrics Data (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

> **Incubating: This feature or API is new! We may still have a few bugs or change some functionality in the future.**

Automation provides value with each execution of a job. A job can save time, dollars, and most likely a combination of both. The ROI (return on investment) Metrics integration will help track the user-defined value of each job execution. **ROI Metrics Data** stores arbitrary key value pairs against your job to help understand your ROI per job execution. The metrics will be stored against the each execution of the job, and accessible via API for further analysis. There is also relevant default execution data to help you further understand your savings.

> **Configuration Tip**
>
> Currently, the data for this feature is stored as file based logs. To ensure resiliency please be sure that a [LogStore](https://docs.rundeck.com/docs/administration/cluster/logstore/) is configured to backup the files.

## Configuring ROI Metrics

The values stored are unique entries chosen by the user. The values are abstracted from a specific metric type (hours, dollars, etc.) to allow customers to define their own ROI metrics. Follow these steps when editing a job to configure ROI Metrics:

1.  Choose the *Execution Plugins* tab.

2.  Check the box for **ROI Metrics Data**.  
      
    ![ROI Metrics Plugin](https://docs.rundeck.com/docs/assets/img/roi-metrics-data.png)

3.  Click **Add Custom Field**.  
      
    ![Add Custom Field](https://docs.rundeck.com/docs/assets/img/roi-metrics-customfield.png)

4.  Enter a value for:

    - ***Field Label***: This is the friendly name of the field that will be shown when picking a value
    - ***Field Key***: This is the name of the field used in the programmatic output.
    - ***Description***: (Optional) A description of the field value.

    > **Heads Up**
    >
    > *For simplified gathering later we suggest no spaces or special characters in the "Field Key".*

5.  Click **Add**.

6.  Enter a value for the metric as an integer or decimal in the field shown.

7.  Save the job.

## Gathering ROI Metrics

When the Job is Executed a new Log Output screen called *ROI Metrics Data* will be shown when the job is complete.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/roi-metrics-log-listing.png" alt="ROI Metrics New Log Entry" />
<figcaption aria-hidden="true">ROI Metrics New Log Entry</figcaption>
</figure>

Selecting that tab will show a table view of the ROI Metrics. In the example shown we can see the value provided along with the following metrics included by default:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/roi-metrics-output.png" alt="ROI Metrics Output" />
<figcaption aria-hidden="true">ROI Metrics Output</figcaption>
</figure>

- Job Duration (in seconds)
- Job Execution Time (UTC)
- Job ID
- Execution ID

The data is also available in JSON format both in the UI and from an API endpoint. Use our [API Guide](https://docs.rundeck.com/docs/api/) to access the data.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/roi-metrics-json.png" alt="ROI Metrics JSON" />
<figcaption aria-hidden="true">ROI Metrics JSON</figcaption>
</figure>

For a walk-through of how the ROI Metrics Data may be used and an example job that will help in gathering ROI metric data check out this [Learning Article](https://docs.rundeck.com/docs/learning/howto/use-roi-metrics.html).
