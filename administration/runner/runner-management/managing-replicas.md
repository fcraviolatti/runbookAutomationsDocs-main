---
title: "Managing Replicas"
source_url: https://docs.rundeck.com/docs/administration/runner/runner-management/managing-replicas.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Managing Replicas

Runners are composed of one or more Replicas. To view the Replicas of a Runner, go to the **Runners** page and select the Runner you want to view. The **Replicas** tab will show you the list of Replicas for that Runner.

![View Replicas of a Runner](https://docs.rundeck.com/docs/assets/img/runner-replicas-list.png)  

For more details on the concept of Replicas and Runners, read through the [Concepts & Architecture](https://docs.rundeck.com/docs/administration/runner/concepts.html).

## Adding Replicas

> **Ephemeral vs Persistent Replicas**
>
> Replicas can only be added via the GUI or API on an ad-hoc basis if the Runner is configured to *not* treat its Replicas as Ephemeral. More details on this are explained in the [**Ephemeral vs. Persistent Replicas**](https://docs.rundeck.com/docs/administration/runner/concepts.html#ephemeral-vs-persistent-replicas) section.

To add a Replica to a Runner, go to the **Replicas** tab of the Runner and click on the **Add Replica** button:

![Add Replica Button](https://docs.rundeck.com/docs/assets/img/add-replica-button.png)  

This will open a popup that provides the various methods for downloading the Replica package:

![Add Replica Popup](https://docs.rundeck.com/docs/assets/img/add-replica-modal.png)  

Follow the instructions in the popup, or for more details see the [**Creating Runners**](https://docs.rundeck.com/docs/administration/runner/runner-installation/creating-runners.html) section.

## Removing Replicas

> **Ephemeral vs Persistent Replicas**
>
> Replicas can only be deleted via the GUI or API on an ad-hoc basis if the Runner is configured to *not* treat its Replicas as Ephemeral. More details on this are explained in the [**Ephemeral vs. Persistent Replicas**](https://docs.rundeck.com/docs/administration/runner/concepts.html#ephemeral-vs-persistent-replicas) section.

To remove a Replica from a Runner, go to the **Replicas** tab of the Runner and click on the **Actions** dropdown. Click on **Delete** and then click on **Ok** to confirm the deletion.

![Delete Replica Button](https://docs.rundeck.com/docs/assets/img/delete-replica.png)
