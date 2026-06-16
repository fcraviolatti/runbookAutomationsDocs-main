---
title: "User Manager Password Security (Commercial)"
source_url: https://docs.rundeck.com/docs/administration/security/password-security.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# User Manager Password Security (Commercial)

> **Available in PagerDuty Runbook Automation Commercial products.**

Runbook Automation includes the [User Manager](https://docs.rundeck.com/docs/manual/user-management/user-mgmt.html) functionality to easily create local Rundeck logins. Rundeck 4.0+ include options to enforce password complexity.

## Password Length

To enable a minimum password length requirement set the following setting in Configuration Management or the `rundeck-config.properties` file. Replace `<integer>` with the required minimum number of characters for user passwords.

<div class="language-text line-numbers-mode">

``` text
rundeck.password.minLength = <integer>
```

</div>

## Password Complexity

To enable password complexity enforcement set the following setting in Configuration Management or the `rundeck-configuration.properties` file.

<div class="language-text line-numbers-mode">

``` text
rundeck.password.strength = <strength setting>
```

</div>

Password strength is scored from 0-4 based on the difficulty of guessing the password. Possible integer values for `<strength-setting>` are listed below with descriptions:

- **0**: Easily guessable: risky password. (guesses \< 10^3)

- **1**: Very guessable: protection from throttled online attacks. (guesses \< 10^6)

- **2**: Somewhat guessable: protection from un-throttled online attacks. (guesses \< 10^8)

- **3**: Safely unguessable: moderate protection from offline slow-hash scenario. (guesses \< 10^10)

- **4**: Very unguessable: strong protection from offline slow-hash scenario. (guesses \>= 10^10)

The complexity check is implemented using the [zxcvbn library](https://github.com/dropbox/zxcvbn).
