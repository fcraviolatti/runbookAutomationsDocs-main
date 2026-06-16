---
title: "ServiceNow Node Source (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/projects/resource-model-sources/servicenow.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# ServiceNow Node Source (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

This is a Node Source plugin that provides node information from ServiceNow'sÂ®CMDB.

There is a [How To article in the Learning section](https://docs.rundeck.com/docs/learning/howto/config-sn-nodesource.html) with an example setup.

## Authentication

To configure authentication with ServiceNow for the Node Source plugin, follow the steps outlined in [ServiceNow Plugins Overview](https://docs.rundeck.com/docs/manual/plugins/servicenow-plugins-overview.html) to configure authentication of the ServiceNow plugins. Alternatively, place credentials directly into the Node Source plugin.

## Paging limit

Default value: 500

This parameter is used to reduce the query time for nodes per page on the ServiceNow API and avoid timeouts. For example, if there are 2000 nodes in the ServiceNow instance, the plugin will fetch them in small groups of 500 (default value), therefore 4 calls will be made to the API until the total number of nodes is complete. Some ServiceNow instances are faster than others, therefore this parameter may be increased to shorten the time it takes to bring up the total number of nodes. On the other hand, if this number increases too much, the API may take too long and return a time-out.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/servicenow-paging-limit.png" alt="Limit by page" />
<figcaption aria-hidden="true">Limit by page</figcaption>
</figure>

## Filters

The plugin offers some **Quick Filters** to gather specific server types from the CMDB.

- all : Retrieve all types of servers
- linux : Retrieve only linux machines
- win : Retrieve only Windows machines
- unix : Retrieve only unix machines
- esx: Retrieve only ESX machines
- solaris: Retrieve Solaris Linux machines
- aix: Retrieve only AIX machines
- hpux: Retrieve only HPUX machines
- osx: Retrieve only OSX machines
- netware: Retrieve only Netware machines
- comma separated list : as example 'linux,win'

> The Quick Filters above are equivalent to a filter of `sys_class_name=cmdb_ci_linux_server` where the "linux" is replaced with the value above.

The **Custom Filter** field will use any custom CMDB filter provided to gather the nodes. *Note: If a Custom Filter is specified, all Quick Filter selections are ignored*

## Mapping and default values

- `mappingParams`: A set of ";" separated mapping entries. This values are going to override the default mapping one by one. The minimal mapping needed is the `username`, because ServiceNowÂ® servers lacks a username field to map:

<div class="language-text line-numbers-mode">

``` text
username.default=root
```

</div>

### Default Mapping

<div class="language-text line-numbers-mode">

``` text
nodename.selector=name
hostname.selector=host_name,ip_address,dns_domain
sshport.default=22
description.default=ServiceNow node instance
description.selector=short_description
osFamily.default=unix
osName.selector=os
osName.default=Linux
osVersion.selector=os_version
ipAddress.selector=ip_address
cpuCoreCount.selector=cpu_core_count
cpuCount.selector=cpu_count
cpuCpeed.selector=cpu_speed
cpuType.selector=cpu_type
osDomain.selector=os_domain
tags.selector=asset_tag
tags.default=servicenow
```

</div>

> **Tips**
>
> All nodes require at least the *nodename*, *hostname* and *user* values. If entries in the ServiceNowÂ® query (Quick or Custom) do not have these values they will not show up in the Nodes list.

### Configuration of the Mapping

A selector with a list like this:

<div class="language-text line-numbers-mode">

``` text
hostname.selector=host_name,ip_address,dns_domain
```

</div>

Are going to search on the result of the query the value of `host_name`, if is not set, the `ip_address` or the `dns_domain`.

A selector with a default value like this example:

<div class="language-text line-numbers-mode">

``` text
osName.selector=os
osName.default=Linux
```

</div>

Are going to search the `os` value, if not set, are going to use the default value `Linux`.

The special case of the tags, if multiple tags are set using comma, all are going to be searched and used.

<div class="language-text line-numbers-mode">

``` text
tags.selector=asset_tag,os
tags.default=servicenow
```

</div>

If is none of the `asset_tag` or `os` exists, the default tag are going to be used `servicenow`.

In the case only the default value exists, this fixed value are going to be set.

<div class="language-text line-numbers-mode">

``` text
osFamily.default=unix
```

</div>

## Notes

The ServiceNow API sometimes returns incomplete or malformed JSON data due to timeouts caused by processing large amounts of information. This can be indicated by an error message within the JSON response. To fix this, you can adjust a setting in ServiceNow to increase the timeout duration.

The ServiceNow default is 60 seconds. Increasing the value may help address this timeout issue.

<div class="language-text line-numbers-mode">

``` text
System Definition > Transaction Quota Rules > REST Table API request timeout
```

</div>
