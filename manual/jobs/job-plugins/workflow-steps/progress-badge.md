---
title: "Progress Badge Workflow Step (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/jobs/job-plugins/workflow-steps/progress-badge.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Progress Badge Workflow Step (Commercial)

The Progress Badge Plugin included with Runbook Automation can create graphic badges to be rendered on the Log Output tab.

See also: [Log Filter Progress Badge (Commercial)](https://docs.rundeck.com/docs/manual/log-filters/progress-badge.html)

Render a single badge using input options:

- Text to be displayed inside the badge. Supports emoticons (see below).
- Status of the Badge, ok (green badge), error (red badge) or neutral (grey badge). Can be a variable from option o key-value data.

## Emoji Support

To use some emoji inside the text, must input the alias of the emoji between colon: `:smile: Successfull job! :100:` Display as:

`ðŸ˜„ Successfull job! ðŸ’¯`

A full list of supported emoji are listed here: [vdurmont/emoji-java](https://github.com/vdurmont/emoji-java)

## Advanced render options

- Specify typeface and font size
- Select for background color of the badge. O can enter a hexadecimal color value in the format \#ffff00
