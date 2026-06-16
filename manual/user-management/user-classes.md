---
title: "User Class Management"
source_url: https://docs.rundeck.com/docs/manual/user-management/user-classes.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# User Class Management

## Overview

User Class Management allows Runbook Automation customers to assign users to User Classes which act as a super-set of ACL enforcement and licensing seat management. Each class enforces a pre-set collection of restrictions across all customer defined projects. The Class Management module included as part of the User Management features will allow customers to assign users to classes to fit their use cases.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/user-classes.png" alt="User Class Screen" />
<figcaption aria-hidden="true">User Class Screen</figcaption>
</figure>

## User Classes

User Classes act as a super set of ACLs. Rundeck uses a lowest privilege model. These ACLs will allow a certain level of access â€œat the mostâ€?, and customers can apply [customized ACLs](https://docs.rundeck.com/docs/learning/tutorial/acls.html) to further refine access.

### Full User

This User Class allows full access to the Runbook Automation environment.

### Job Runner

This User Class, when assigned, will allow a user to run jobs and view output on all projects. They can not modify jobs or other resources.

> Note: Not all licenses include the Job Runner. Please contact your customer support manager for information.

### Default Class Assignment

By default users are assigned to the Full User class. This is configurable for OnPrem installations if customers would like to assign a different class by adding the following entry to the Configuration Management UI.

<div class="language-text line-numbers-mode">

``` text
rundeck.license.entitlements.userClass.autoAssignUserClass
```

</div>

Possible values are: `[FullUser | JobRunner | None]`

If the setting is not present `FullUser` is used for OnPrem installations, `AppAdmin` is used for Cloud.

> *Note: â€œNoneâ€? would represent no access to anything in Runbook Automation. The user could login but would have access to nothing. This is not an assignable class today and will not show up in the management UI. It is only available for default assignment.*

> **Warning**
>
> This is not available in the Cloud offering.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/user-classes-config.png" alt="User Class Screen" />
<figcaption aria-hidden="true">User Class Screen</figcaption>
</figure>

## Assigning Classes

To assign a class to a user:

1.  Login to Runbook Automation as an admin equivalent account.
2.  Open the System Menu (gear icon) and select **User Manager**
3.  Select the User Classes Tab
4.  Click **Assign a New User**
5.  Type in the username and select the Class from the **Choose User Class** button.

Note: It is possible to assign users to classes before they have been created as a user or logged in. The initial release is a free form text field. There is no validation on the user name field in the initial release.

The â€œBulk Assignâ€? button can be used on any existing users by selecting them with the check box next to the accounts and choosing the role to assign.

## Reporting

There is also a new section in the [System Report](https://docs.rundeck.com/docs/manual/system-report.html) (OnPrem Only) Diagnostics page called â€œ**User Class Usage Audit**â€?.

### Metrics included are as follows:

- *FullUser.login.count:* Count of User Logins for class FullUser in the time period.
- *JobRunner.login.count:* Count of User Logins for class JobRunner in the time period.
- *JobRunner.login.unique.count:* Count of Unique User Logins for class JobRunner in the time period.
- *FullUser.login.unique.count:* Count of Unique User Logins for class FullUser in the time period.
- *FullUser.assigned.current:* Current Count of User Class assignments for FullUser.
- *JobRunner.assigned.current:* Current Count of User Class assignments for JobRunner.
- *JobRunner.assigned.max:* Max Count of User Class assignments for JobRunner.
- *FullUser.assigned.max:* Max Count of User Class assignments for FullUser.
- *FullUser.mapping.current:* Current Mappings for FullUser. (shown as array of usernames)

This section is also included in the Export Report and may be asked for as part of licensing validation.

## Licensing

The User Classes are enabled on and entitled through an updated license model that includes â€œentitlementsâ€?. In the graphic shown above the license has been generated with entitlements for (10) Full Users, (10) Job Runners.
