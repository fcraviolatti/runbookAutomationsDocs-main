---
title: "VMWare Operations Node Step Plugin (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/node-steps/vmware.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# VMWare Operations Node Step Plugin (Commercial)

Allows users to Power-Off/Power-On/Restart/Suspend/Stand-By a VM. This plugin is a workflow node step, so you need dispatch this step to the nodes that you want to apply the operation.

Configuration

- **Operation**: "reboot", "poweron","poweroff","standby","suspend"

Authentication Options

- **URL Server**: URL of the Server, eg: https://vmware-server
- **Username**: Login Username
- **Password**: Username Password
- **Ignore SSL certificate**: Connecting with the server ignoring the SSL certificate. If this is false, you will need to add the certificate to the truststore ([see here](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/vmware.html#connecting-using-certificate)).
