---
title: "Mask Passwords"
source_url: https://docs.rundeck.com/docs/manual/log-filters/mask-passwords.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Mask Passwords

This log filter masks output of option values for the job that are marked as SECURE, such as passwords or other similar data. If a job is configured with an option that uses Secure or Secure Remote Authentication as the Input Type, then this filter will mask the output of that option field in logs.

## Usage

This filter has two options:

- Replacement - this value replaces the value of the option input. By default, it displays as â€œ\[SECURE\]â€?
- Color - pulldown of ANSI color values for the replacement.

If the job has Secure options, it is recommended to always apply this filter to job steps that may output the values of those options.
