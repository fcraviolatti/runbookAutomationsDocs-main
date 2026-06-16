---
title: "Automated Diagnostics"
source_url: https://docs.rundeck.com/docs/learning/solutions/automated-diagnostics/integrating-chat-tools.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Automated Diagnostics

## Sending Diagnostics to Chat Tools

Most teams operate out of a chat tool, like Slack or Microsoft Teams, during an incident.  
This is so that they can collaborate, assign tasks, and update others as they troubleshoot the issue. For this reason, one of the best practices with the Diagnostics Solution is to integrate PagerDuty with your chat tool so that the diagnostic data appears automatically in the incident channel.

Depending on the chat tool you use, you will want to follow the [Slack Integration Guide](https://support.pagerduty.com/docs/slack-integration-guide) or the [Microsoft Teams Integration Guide](https://support.pagerduty.com/docs/microsoft-teams).

Once those integrations are complete and a Channel or Team has been linked to a PagerDuty Service or Incident, the diagnostics from the runbook will appear in the chat tool when they are posted to the Incident Timeline:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/diag_in_slack.png" alt="Diagnostic results displayed in Slack" />
<figcaption aria-hidden="true">Diagnostic results displayed in Slack</figcaption>
</figure>

  

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/auto-actions-ms-teams.png" alt="Automation Actions in Microsoft Teams" />
<figcaption aria-hidden="true">Automation Actions in Microsoft Teams</figcaption>
</figure>

## Invoking Diagnostics from Chat Tools

PagerDutyâ€™s Slack and Microsoft Teams integrations also provide the ability to invoke Automation Actions:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/invoke-actions-from-slack.png" alt="Invoke Automation Actions from Slack" />
<figcaption aria-hidden="true">Invoke Automation Actions from Slack</figcaption>
</figure>

This can be useful for **â€œrefreshingâ€? the diagnostics**, which can assist with providing status updates to stakeholders.

Invoking from chat tools also makes it easy to execute a known-fix remediation - such as a restart, rollback, failover or scaling of resources.
