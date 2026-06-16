---
title: "Runbook Automation Licensing"
source_url: https://docs.rundeck.com/docs/administration/license.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Runbook Automation Licensing

## Overview

While Rundeck is an open source project maintained by PagerDuty, Runbook Automation is commercial software for which you can purchase a license from PagerDuty. Runbook Automation provides a tested, supported, and enterprise-ready distribution of Rundeck with additional features and capabilities for enterprise scale use. Also, a Runbook Automation subscription license is the only way to receive professional support from PagerDuty and the core Rundeck team.

[Contact the PagerDuty sales team to get started with Runbook Automation today.](https://www.pagerduty.com/contact-us/)

## License Key Installation

> Note: this is only required on Self-Hosted version. Runbook Automation (SaaS) will come pre-installed with your license.

Ask for the license key to the support team. Then install the license key via the GUI or on the filesystem directly.

### Via GUI

Upload the license key using the GUI:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/license-key-gui-1.png" alt="Upload the license key using the GUI" />
<figcaption aria-hidden="true">Upload the license key using the GUI</figcaption>
</figure>

Click on "No License Key File is installed"

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/license-key-gui-2.png" alt="Click on &quot;No License Key File is installed&quot;" />
<figcaption aria-hidden="true">Click on "No License Key File is installed"</figcaption>
</figure>

Click on "Upload License File"

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/license-key-gui-3.png" alt="Click on &quot;Upload License File&quot;" />
<figcaption aria-hidden="true">Click on "Upload License File"</figcaption>
</figure>

Select the license key file and press "Upload License File"

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/license-key-gui-3-a.png" alt="Agree to the Rundeck Master Software License Agreement" />
<figcaption aria-hidden="true">Agree to the Rundeck Master Software License Agreement</figcaption>
</figure>

Agree to the Rundeck Master Software License Agreement and Rundeck Support Policy then click "Confirm"

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/license-key-gui-4.png" alt="View of installed license" />
<figcaption aria-hidden="true">View of installed license</figcaption>
</figure>

### Via filesystem

Copy the license file to the correct directory depending of the kind of installation.

License file name : `rundeckpro-license.key` ( don't change to a different name )

File location:

Rundeck package RPM (Redhat/centos) or DEB (debian/ubuntu):

<div class="language-text line-numbers-mode">

``` text
/etc/rundeck/
```

</div>

Rundeck Launcher:

<div class="language-text line-numbers-mode">

``` text
$RDECK_BASE/etc/
```

</div>

### Store license in database

If you would like to store your license in your database rather than your filesystem, turn on the following setting:

`rundeck.license.useStorageTree=true`

If you have a license file installed in your Rundeck server it will be migrated automatically into the database.

When Rundeck boots it will check the license file on the filesystem if it exists, and if the issue date of that license is more recent than the license in the database, the database will be updated with the license on the filesystem.

### Store the license using a custom storage tree

If you would like to store your license in a storage tree, you can configure a storage tree using the standard storage tree config options.

Turn on license storage tree usage then provide your configuration using the prefix: `rundeck.license.storage`

Example storing the license on Amazon S3 root folder

<div class="language-text line-numbers-mode">

``` text
rundeck.license.useStorageTree=true
rundeck.license.storage.provider.1.type=object
rundeck.license.storage.provider.1.path=/
rundeck.license.storage.provider.1.config.bucket=rundeck
rundeck.license.storage.provider.1.config.objectStoreUrl=https://s3.amazonaws.com
rundeck.license.storage.provider.1.config.accessKey=YOUR_ACCESS_KEY
rundeck.license.storage.provider.1.config.secretKey=YOUR_SECRET_KEY
```

</div>

Example storing the license on Amazon S3 using a specific folder

Use the property `rundeck.license.file` to declare the specific path, and the license name.

Use the property `rundeck.license.storage.provider.1.path` to declare the license path.

Both properties must be used as show below.

<div class="language-text line-numbers-mode">

``` text
rundeck.license.useStorageTree=true
rundeck.license.storage.provider.1.type=object
rundeck.license.storage.provider.1.config.bucket=rundeck
rundeck.license.storage.provider.1.config.objectStoreUrl=https://s3.amazonaws.com
rundeck.license.storage.provider.1.config.accessKey=YOUR_ACCESS_KEY
rundeck.license.storage.provider.1.config.secretKey=YOUR_SECRET_KEY

rundeck.license.storage.provider.1.path=/FOLDER_NAME/SUB_FOLDER_NAME/
rundeck.license.file=/FOLDER_NAME/SUB_FOLDER_NAME/rundeckpro-license.key
```

</div>
