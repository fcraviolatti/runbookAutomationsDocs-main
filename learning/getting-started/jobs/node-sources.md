---
title: "Node Sources and How to Use Them"
source_url: https://docs.rundeck.com/docs/learning/getting-started/jobs/node-sources.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Node Sources and How to Use Them

## Nodes and Node Sources Overview

Generally speaking, nodes are the objects that are being managed within a Rundeck automation project. Typically, nodes are infrastructure such as servers (virtual or physical) or network devices but they could represent anything that might be targeted by a job or command issued from the automation system. This could include something logical like a dataset, if that is what will be manipulated or referenced in the commands or job steps.  
A Rundeck project needs to have a way to know which nodes to address. The definitions of nodes are referred to as node sources (or resource models). Node sources can be thought of as definitions for a set of nodes and most projects will have more than one source and type of source.  
Node sources fall generally into two categories: static and dynamic. A static node source is a file or url that contains definitions but gets updated manually as changes happen in the environment. A dynamic node source is usually an integration that gets node data directly from a third party source through an API, such as AWS or ServiceNow CMDB.  
The collection of nodes that a given project is aware of and can address is a superset of all the nodes from all node sources in that project. Different node sources might provide different metadata about the same nodes, so the nodename is treated as the unique identifier used to group data about the same node that comes from different sources. Whether a user in a project can see all or some of the nodes in a project will depend on what permissions they are granted in ACL policies based on their role/group.  
Though nodes are defined in the context and available only within that context, it is certainly possible that the same nodes and/or node sources might be used in more than one project in the same Rundeck environment. Typically, this happens when more than one team has different responsibilities in relation to common servers.  

## Adding Node Sources

Node sources are largely a setup element and donâ€™t get added or modified very often. With proper planning, this happens during the project setup phase and new sources are only added when new nodes come under management.  

### Adding a Static Source

Static sources come in 4 varieties: file, url, directory and script. File (in .yaml, .xml or .json format) is the most common of these. The other three varieties are alternate ways to access something comparable using those same file formats. A url points at a file effectively, while a directory will contain a set of resource files. A script source executes a script to generate the needed file in the correct format.

#### Edit Nodes

Select the Project Settings gear icon at the bottom left and then select Edit Nodes  
![](https://docs.rundeck.com/docs/assets/img/nodes1-editnodes.png)  
Click the blue Add a New Source button at the bottom  
![](https://docs.rundeck.com/docs/assets/img/nodes2-addnewsource.png)  
Select the preferred Node Source type (such as File)  
![](https://docs.rundeck.com/docs/assets/img/nodes3-selectfilesource.png)  
Provide details on where and how to connect to the new Node Source  
![](https://docs.rundeck.com/docs/assets/img/nodes4-filesourcedetails.png)  
For a file Node Source, the required elements are the File Path (on the Rundeck server) and the Format. If permissions have been set appropriately, select Writable to have the ability to edit the Node Source in the Rundeck interface. Click the green Save button to complete the source.  
![](https://docs.rundeck.com/docs/assets/img/nodes5-savesave.png)  
To commit your node source changes to the database, select the second green Save button at the bottom of the Sources page. There are warning messages at top and bottom to remind you to save here.  

### Adding a Dynamic Source

The details needed for dynamic sources vary greatly based on the wide variety of different source tools. There are many dynamic sources and it is possible to create custom ones as well (as Rundeck plugins) but one of the most common is the Ansible resource model. This model assumes that an Ansible installation is co-resident on the Rundeck server.  

#### Edit Nodes

Select the Project Settings gear icon at the bottom left and then select Edit Nodes  
![](https://docs.rundeck.com/docs/assets/img/nodes1-editnodes.png)  
Click the blue Add a New Source button at the bottom  
![](https://docs.rundeck.com/docs/assets/img/nodes2-addnewsource.png)  
Select the preferred Node Source type (such as Ansible)  
![](https://docs.rundeck.com/docs/assets/img/nodes6-selectansiblesource.png)  
Provide details on where and how to connect to the new Node Source nodes.  
![](https://docs.rundeck.com/docs/assets/img/nodes7-ansiblesourcedetails.png)  
For an Ansible Node Source, the primary settings to be concerned with are paths to the Ansible binaries, the Ansible inventory file and Ansible config file. For more details on integrating with Ansible, look [here](https://docs.rundeck.com/docs/learning/howto/using-ansible.html#how-to-integrate-ansible-with-rundeck). Click the green Save button to complete the source.  
![](https://docs.rundeck.com/docs/assets/img/nodes8-savesave2.png)  
To commit your node source changes to the database, select the second green Save button at the bottom of the Sources page. There are warning messages at top and bottom to remind you to save here.  

## Editing Data in Node Sources

Not all node sources allow for direct modification of the contained data. Where it is possible, access to that data is available under the Edit tab when you go to Edit Sources. There will be a Modify button associated with each source that can be changed. One sort of Source like this would be a File Node Source that has been marked as writable.  
![](https://docs.rundeck.com/docs/assets/img/nodes9-modifysource.png)  
Changing the data for connecting to a source happens in the same area where sources get added, the Sources tab under Edit Nodes.  
Note: Refreshing nodes with updated metadata is controlled by the â€œcache delayâ€? setting under Edit Nodes \| Configuration. By default, that means that the system checks for new content every 30 seconds.  

### Node Enhancers

In cases where it isnâ€™t possible or scalable to edit individual node data directly, it is possible to add additional metadata to nodes in Rundeck using a feature called node enhancers.  
Effectively, enhancers direct the system to look for nodes that match specific criteria and dynamically apply additional tags or attribute values to nodes that match. Using enhancers is a scalable way to fill in missing data where you know what needs to be added based on what is already known.  

#### Adding an Enhancer

To add an Enhancer, Click the blue Add a New Enhancer button at the bottom of the Enhancers tab under Edit Nodes  
![](https://docs.rundeck.com/docs/assets/img/nodes10-addenhancer.png)  

#### Enhancer Example

In the screenshot example, a node with a specific name is being enhanced with two attributes that change how it will be connected to (using SSM) as well as getting a specific tag (ssm).  
![](https://docs.rundeck.com/docs/assets/img/nodes11-enhancerdetails.png)  

## Removing Node Sources

To remove a Node Source, return to the Sources tab under Edit Nodes and use the red delete button associated with the Node Source you want to remove. Note that by deleting the source you arenâ€™t removing the file or other source data. You are simply disconnecting this project from that source data, which will remove the associated nodes from Rundeck and the ability to target those nodes with Jobs or Commands.  
![](https://docs.rundeck.com/docs/assets/img/nodes12-deletesource.png)  

## How is a Node Source Different from a Node Filter?

Node Sources are established at the project level and represent a specific static or dynamic set of nodes available within that project. Node sources are not related directly to a job. A dynamic source is dynamic in the sense that the nodes returned by the source can change over time based on whatâ€™s included in the source database or system.  
Node Filters, on the other hand, are generally established in the context of a job to identify which nodes will be targeted by that job. Node filters are also dynamic but not in the same sense. A node filter is composed of one or more attribute/value pairs that must be matched to be included in the filter and therefore targeted by that job. Which nodes are included in the filter set can change based on which nodes from Node Sources match the Node Filter at the time the job runs.  

## Resources

[Information on the static sources and available file formats](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/builtin.html#file-source)  
[More Information on Node Sources](https://docs.rundeck.com/manual/projects/resource-model-sources/#what-is-a-resource-model-source)  
[Detailed Documentation Related to Ansible Integration](https://github.com/rundeck-plugins/ansible-plugin)  
[Making Custom Node Sources Editable](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/resource-editor.html#resource-model-source)
