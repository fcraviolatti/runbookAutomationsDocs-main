---
title: "Configure ServiceNow CMDB as a Node Source"
source_url: https://docs.rundeck.com/docs/learning/howto/config-sn-nodesource.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Configure ServiceNow CMDB as a Node Source

The ServiceNowÂ® Node Source brings CMDB entries into Rundeck as Nodes. This exercise shows how to configure and use some key features of that Node Source.

## PreRequisites

- ServiceNowÂ® login with access to the CMDB data
- (If possible) Add two entries to the Servers CI Class as "node1" and "node2" with other data assigned to that CI.

## Exercise

This exercise configures the [ServiceNowÂ® Node Source](https://docs.rundeck.com/docs/manual/projects/resource-model-sources/servicenow.html) with a Custom Filter from the ServiceNowÂ® CMDB.

Basic Exercise

Additional Exercises

Basic Exercise

**ServiceNowÂ® Steps**

1.  Login to your ServiceNowÂ® instance
2.  In the Module Explorer navigate to *Configuration \> Servers \> All*  
    or type `cmdb_ci.list` in the Filter Navigator box.
3.  Filter the CMDB entries as needed for your Node Source.  
    In our example we have filtered for entries names that start with *node*.  
      
    ![Example Filtered Results](https://docs.rundeck.com/docs/assets/img/howto-sn-nodelist.png)  
      
4.  In the filter bar right click the last entry in the filter breadcrumbs list and choose **Copy Query**  
      
    ![Copy CMDB Query](https://docs.rundeck.com/docs/assets/img/howto-sn-copyquery.png)  
      

**Rundeck Steps**

1.  Open **Welcome Project \> Project Settings \> Edit Nodes**
2.  Click **Add a new Node Source +** button
3.  Choose **ServiceNow Resource Model Source**
4.  Enter values for **Sever URL**, **Username**, **Password** (or supply Password Path to Key Store entry)
5.  Paste the Query string from the ServiceNowÂ® steps above.  
    Our example uses `nameSTARTSWITHnode`
6.  Click **Save**
7.  Use the arrow buttons to put the ServiceNowÂ® Node Source above the Node Wizard.  
      
    ![Move Node Source](https://docs.rundeck.com/docs/assets/img/howto-sn-movenodesource.png)  
      
8.  Navigate to the **Nodes** area and search `.*` to show the SN nodes.

Since we previously completed the [Creating Nodes Tutorial](https://docs.rundeck.com/docs/learning/tutorial/creatingnodes.html) to add `node1` and `node2` and were able to add corresponding entries to our demo ServiceNowÂ® Instance the nodes were merged. Moving the ServiceNowÂ® entry to the top allowed our settings from the Node Wizard entry to drive the settings.

Additional Exercises

**Field Mappings**

1.  Add some values to the Asset Tag fields on your ServiceNowÂ® entries.
2.  Add the following text to the ServiceNowÂ® Node Source **Mapping Params**: `asset-tag.selector=asset_tag`
3.  Refresh the Nodes List.

The Asset Tag (asset-tag) entry is now an attribute on the Node.

## Additional Information

ServiceNow'sÂ®Developer program allows anyone to sign up and get access to a ServiceNowÂ® instance for testing/learning purposes. Sign Up at: <https://developer.servicenow.com/>
