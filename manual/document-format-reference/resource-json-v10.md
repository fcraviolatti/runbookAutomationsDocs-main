---
title: "Defining Nodes in JSON Format"
source_url: https://docs.rundeck.com/docs/manual/document-format-reference/resource-json-v10.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Defining Nodes in JSON Format

This docuement describes the Rundeck resource model document JSON format.

The `resource` JSON document declares a resource model used by a Rundeck Project to define the set of Nodes that are available.

See <http://json.org> for more information about JSON.

## Structure

The resource format supports several JSON formats. In all cases a Node is represented by a JSON Map called a [Node Entry](#node-entry). The document structure can be:

- A Map with node names as keys, and Node Entries as values
- An Array of Node Entries

Using Map of Node Entries is the preferred format.

When serializing/exporting Nodes data to this format, the generator will produce a Map of Node Entries keyed by name.

Map example:

<div class="language-json line-numbers-mode">

``` json
{
  "node1": {
    "nodename":"node1",
    ...
  },
  "node2": {
    "nodename":"node2",
    ...
  }
}
```

</div>

Array example:

<div class="language-json line-numbers-mode">

``` json
[
  {
    "nodename":"node1",
    ...
  },
  {
    "nodename":"node2",
    ...
  }
]
```

</div>

## Node Entry

A Node entry is a Map with some required and some optional entries.

Required Entries:

`nodename`  
Name of the node, this must be a unique Identifier across nodes within a project

Optional Entries:

`hostname`  
Hostname of the node. This can be any IP Address or hostname to address the node. Since hostname is used to make SSH connections, it is possible to overload the value to include port number. (eg, hostname:port).

`username`  
User name to connect to the node via SSH.

`description`  
A description of the Node

`tags`  
A literal with comma-separated tag strings, or a List of tag strings. Tags are used for filtering nodes and often represent server role, environment, class, or group.

`osFamily`  
OS Family

`osArch`  
OS Architecture

`osName`  
OS Name

`osVersion`  
OS Version

`editUrl`  
URL to an external resource model service.

`remoteUrl`  
URL to an external resource model editor service.

*Anything*  
Specify any custom attributes about node using a string value.

- For more information about using the `editUrl`/`remoteUrl` see the [Rundeck User Manual](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/resource-editor.html#resource-editor).

## Examples

Here's a document with two nodes, with several of the required and optional attributes discussed above.

<div class="language-json line-numbers-mode">

``` json
{
  "madmartigan.local": {
    "tags": "local,server",
    "osFamily": "unix",
    "username": "greg",
    "osVersion": "10.10.3",
    "osArch": "x86_64",
    "description": "Rundeck server node",
    "hostname": "madmartigan.local",
    "nodename": "madmartigan.local",
    "osName": "Mac OS X"
  },
  "test": {
    "tags": "alphabet, soup",
    "osFamily": "unix",
    "ssh-key-storage-path": "keys/testkey1.pem",
    "username": "vagrant",
    "osVersion": "10.10.3",
    "osArch": "x86_64",
    "description": "Rundeck server node",
    "hostname": "192.168.33.12",
    "nodename": "test",
    "osName": "Mac OS X"
  }
}
```

</div>
