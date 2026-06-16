---
title: "tours"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/tours.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# tours

## Automated Diagnostics

### Following the Tours

In addition to the library of prebuilt Automation Jobs, the Automated Diagnostics Solution includes a collection of in-product **Tours** that guide you through integrating these prebuilt, automated-workflows with your infrastructure and tooling - including PagerDutyâ€™s Incident Response.

It's recommended that you follow the included Tours before starting to use this.

> **Tip**
>
> To initiate any Tour, click the Tours icon at the bottom right of your screen (next to the light bulb icon) and select the Tour youâ€™d like.

![Initiate Tours](https://docs.rundeck.com/docs/assets/img/solutions-auto-diag-initiate-tours.png)  

### Included Tours

- Tour numbers are the *recommended* order to follow when using the Tours. This order may not be applicable for all users. See the **Expected Result** column to identify which Tours are relevant for you.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tour</th>
<th>Dependencies or Requirements</th>
<th>Expected Result</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Tour 1: Configure AWS Credentials</td>
<td>- Your AWS Access Key ID<br />
- Your AWS Secret Key</td>
<td>Can run most included AWS Jobs</td>
</tr>
<tr class="even">
<td>Tour 2: Configure EC2 Inventory</td>
<td>- Completed Tour 1<br />
<br />
- Endpoint Region (you will select this during the tour)</td>
<td>EC2 instances added to the Node-Inventory</td>
</tr>
<tr class="odd">
<td>Tour 3a: Configure Systems Manager (SSM)</td>
<td>- Completed Tours 1 and 2</td>
<td>Can connect to AWS instances using SSM for commands and Jobs</td>
</tr>
<tr class="even">
<td>Tour 3b: Configure SSH Connectivity</td>
<td>- Completed Tour 1 and 2<br />
<br />
- Install an Enterprise Runner if you are using Runbook Automation<br />
<br />
- SSH Private Key or Password for connecting to nodes</td>
<td>Can connect to nodes using SSH for commands and Jobs</td>
</tr>
<tr class="odd">
<td>Tour 4: Send Diagnostic Data to PagerDuty</td>
<td>- PagerDuty API Token</td>
<td>Can add diagnostic-data to the Incident Timeline of PagerDuty incidents</td>
</tr>
</tbody>
</table>

  

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/solutions-auto-diag-example-tour.png" alt="Example Tour" />
<figcaption aria-hidden="true">Example Tour</figcaption>
</figure>

### **After following the tours, you can now use the [<u>Prebuilt Automation Jobs!</u>](https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/jobs.html)**
