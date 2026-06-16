---
title: "Rundeck 4.8 Upgrade Notes"
source_url: https://docs.rundeck.com/docs/upgrading/upgrading-to-4.8.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Rundeck 4.8 Upgrade Notes

To enhance the Security of Rundeck and Runbook Automation in version 4.8 we added some new behavior to the Login Process. In order to prevent certain types of attacks the session cookie will change after the first request after authentication. If you have any processes using the API with Password Authentication, it is important to ensure you update those scripts using the guidance below.

## Usage Scenario

Using Password Authentication against the API as described [in the documentation here](https://docs.rundeck.com/api/#password-authentication).

## Changes required

The `JSESSIONID` cookie will change after the first request after authentication. You will have to update your client code to follow redirects for subsequent requests.

For example, when using `curl` you would have to useÂ `-b`Â andÂ `-c`Â options to update the session cookie in your next request after authentication. Alternately, you could add theÂ `-L`Â option to the initial login POST, which will follow the redirect after login and update the session cookie.
