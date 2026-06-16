---
title: "Bundled Orchestrator Plugins"
source_url: https://docs.rundeck.com/docs/manual/orchestrator-plugins/bundled.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Bundled Orchestrator Plugins

Bundled Orchestrator plugins included in Rundeck.

## Random Subset

Selects a maximum number of the target nodes at random

### Configuration

Count  
Number of nodes to select from the pool

## Rank Tiered

Processes nodes in a tiered manner, ordered by rank.

Will never process the next rank until all nodes in the previous rank are complete. Uses the configured Rank ordering for the Job.

Note: if a Rank Attribute is not set, then the node names are used as the rank attribute, and the behavior of this orchestrator will essentially be single threaded.

## Max Percentage

Processes at maximum a percentage of the target nodes.

Will never process more than the given percentage of nodes per run at one time regardless of how high threads are configured.

### Configuration

Percent  
Max Percentage (e.g. `33` for 33%)

## Highest - Lowest

[See Docs here](https://docs.rundeck.com/docs/manual/orchestrator-plugins/highest-lowest.html)
