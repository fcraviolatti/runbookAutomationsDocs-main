---
title: "HashiCorp Consul (Commercial)"
source_url: https://docs.rundeck.com/docs/administration/configuration/hashicorp-consul.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# HashiCorp Consul (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

Runbook Automation Self-Hosted users have the option to use HashiCorp Consul as a method to edit configuration properties. By doing so, it allows users to manage the configuration for all of their services in one place. This feature is very beneficial because it allows users to edit configurations across all of their Runbook Automation instances. So, instead of having to change a configuration for each instance, change it once in Hashicorp and it will apply to all instances.

## Getting Started

To begin, make sure that both Runbook Automation Self-Hosted and HashiCorp Consul are installed. The easiest way to get HashiCorp up and running is using their docker image. The docker image is named "consul." Consul can be found at localhost:8500, but this can also be changed from within Consul. For more information about installing, visit [Consul](https://www.consul.io/docs/install). Next, make sure that Runbook Automation knows to use Consul for configuration. There are a couple of different ways to do that:

### RPM, Debian and Docker Users

For RPM, Debian and Docker users, the best way to specify that Runbook Automation should use Consul, is by defining the environment variable to be true. To do so, add the following to the `/etc/rundeck/profile` file:

<div class="language-text line-numbers-mode">

``` text
RUNDECK_CONSUL_ENABLED=true
```

</div>

### War Users

For customers who use installed Runbook Automation using the .war, there are a couple different options.

1.  Define the environment variable just like RPM, Debian and Docker users by adding the following to the `/etc/rundeck/profile` file:
2.  Pass the property as a flag when starting Runbook Automation. An example of that would look like the following:

<div class="language-text line-numbers-mode">

``` text
java -Xmx4g -Drundeck.consul.enabled=true -jar rundeck-5.20.1-20260518.war
```

</div>

### Setting the Consul server in Runbook Automation

Now that Runbook Automation knows to use Consul, we can shut down Runbook Automation and look at the newly created `bootstrap.yml` file, which is located in the \${rdbase}/server/config directory. In there, it will specify the host of Consul. The host property should be set to the ip address or hostname of your Consul server.

## Services in Consul

In HashiCorp, Runbook Automation may not appear right away as a service. However, once the Runbook Automation service is fully up and running, it will show up in HashiCorp.

## Adding the Runbook Automation Configuration in Consul

To create a new Key/Value pair, click on the key/value tab in the top of Consul. Next, create a folder called "config", with another folder called "rundeck" inside of it. Inside of the Runbook Automation folder is where all the Runbook Automation configuration will be placed. Begin by creating a key/value pair named "data." Now, copy and paste all the contents in the `rundeck-config.properties` file into the value for that key. After that, comment out the entire `rundeck-config.properties` file. Now, when relaunching Runbook Automation, it will pull the configuration settings from Consul.

> **Warning**
>
> If a key/value pair is defined that conflicts with a setting configured in a file on the server (rundeck-config.properties), then the file on the server will always override the Consul configuration.

## Example: Using HashiCorp for a Cluster

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/rundeck-server-id.png" alt="Consul - Dispatching to Specific Instance" />
<figcaption aria-hidden="true">Consul - Dispatching to Specific Instance</figcaption>
</figure>

If using a cluster of Runbook Automation instances, then you can specify the server id when creating the folder for the config key/values. Looking at the example above, there are two different folders created inside of the config directory. One called Runbook Automation and one called Runbook Automation with a long id after it. That is how to specify a server to have all the configuration settings applied to. By just naming the folder Runbook Automation, we apply the configuration to all members of the cluster. So, in order to apply the configuration to just one instance, we need to create a directory called "rundeck,{server_id}"(as shown in image above). To find the the server id, click on the gears icon in the top right hand corner of Runbook Automation and select "System Report." On the next page, you will see the following box containing your server UUID: ![Server ID](https://docs.rundeck.com/docs/assets/img/server-id-location.png)

> **Warning**
>
> If a server ID is specified, those configuration settings will always override the settings specified for all instances in the "rundeck" folder.

### Levels of Precedence for Clusters

1.  A file on the server (rundeck-config.properties)
2.  In Consul, specifying the server to be applied to.
3.  In Consul, not specifying a server.
