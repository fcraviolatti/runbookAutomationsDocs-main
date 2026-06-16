---
title: "Highlight Output"
source_url: https://docs.rundeck.com/docs/manual/log-filters/highlight-output.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Highlight Output

This log filter parses the log output of a workflow step and highlights the output that matches a given regular expression. This filter changes display output in Rundeck, but does not alter the logs themselves.

## Usage

This filter has four options:

- Pattern - regex to test against the log output
- Foreground color - a pulldown list of ANSI colors to apply to the highlighted text
- Background color - a pulldown list of ANSI colors to apply to the background of the highlighted text.
- Mode - a pulldown list of text options (bold, underline, blink, and reverse) to apply to the highlighted text.

The selected text regex has several options. A regex without a capture group will simply highlight any text that matches whatâ€™s in the regex and apply the colors and mode to only the matched phrase. Capture groups in a regex will highlight any and all capture groups in the regex, while leaving out everything else matched by the regular expression.

## Example

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-highlight-example1.png" />
</figure>

This setting will filter the log output looking for an initial â€œ0â€? (zero) in the attached job stepâ€™s log output. If it matches, the result will look like this:

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/logfilter-highlight-example2.png" />
</figure>
