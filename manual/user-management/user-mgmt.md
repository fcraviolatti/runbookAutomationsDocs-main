---
title: "User Manager"
source_url: https://docs.rundeck.com/docs/manual/user-management/user-mgmt.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# User Manager

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/usermgr-menu-button.png" alt="User Manager Button" />
<figcaption aria-hidden="true">User Manager Button</figcaption>
</figure>

## User Summary

This is a listing of all the users that have logged in to Rundeck regardless of the source of users.

## Manage Local Users (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

Enterprise users can leverage the built-in GUI based management and centralized storage of local Rundeck user accounts.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/usermgr-manage-users.png" alt="User Manager Screen" />
<figcaption aria-hidden="true">User Manager Screen</figcaption>
</figure>

### Adding Users

Click the **Add User** button in the main window. Fill out the fields.

- ***Username:*** Unique value used to login to the system. This is also the value used to merge with other user sources. (LDAP/Active Directory)
- ***Password:*** By default there are no password policies enforced. It is strongly encouraged to use something secure!
- *First Name:* What you call someone informally.
- *Last Name:* What you use when it's time to get a bit more formal.
- *Email:* How to reach someone.
- *Notes:* A nice description of this person that makes them smile.
- ***Groups:*** Provide at least one role for them to login. See [Groups Section](#manage-local-groups) below

***Bold/Italics*** are minimum required fields.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/usermgr-add-user.png" alt="Add User Screen" />
<figcaption aria-hidden="true">Add User Screen</figcaption>
</figure>

## Manage Local Groups (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

GUI based management of groups (also sometimes referred to as Roles).

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/usermgr-manage-groups.png" alt="Group Manager Screen" />
<figcaption aria-hidden="true">Group Manager Screen</figcaption>
</figure>

### Adding Groups

Click the ***Add Group*** button in the main window. Fill out the fields and select users for the new group.

- ***Group Name:*** Unique name of the group. Reference this value in ACL policies.
- *Description:* A nice description of this group of users.
- *Users:* Click the green plus sign to add the user to the group. Click the red minus sign to remove them from the group.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/usermgr-add-group.png" alt="Group Add Screen" />
<figcaption aria-hidden="true">Group Add Screen</figcaption>
</figure>

## Appendix

### Including Admin Users

By default the Rundeck admin user is not listed in the User Manager. There are some options available in `rundeck-config.properties` to configure whether admin accounts are available in this module. [They are documented here](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#rundeck-config-properties) and prefixed with `rundeck.security.dblogin.`
