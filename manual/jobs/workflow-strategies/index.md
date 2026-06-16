---
title: "Workflow Strategies"
source_url: https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Workflow Strategies

Workflow execution is controlled by two important settings: *Handling a step failure* and *Strategy*.

<figure>
<img src="https://docs.rundeck.com/docs/assets/img/fig0401.png" alt="Workflow controls" />
<figcaption aria-hidden="true">Workflow controls</figcaption>
</figure>

*If a step fails*: This manages what to do if a step incurs an error:

- Stop at the failed step: Fail immediately (default).
- Run remaining steps before failing: Continue to next steps and fail the job at the end.

The default is to fail immediately but depending on the procedure at hand it is possible to choose to have the execution continue.

*Strategy*: Controls the order of execution of steps and command dispatch to nodes: *Node-oriented* and *Step-oriented*.

- *Node First*: Executes the full workflow on each node before the next node. (default)
- *Sequential*: Executes each step on all nodes before the next step.
- *Parallel*: Run all steps in parallel.

The following illustrations contrast the strategies showing how three steps proceed across two nodes.

Node First flow illustrated:

<div class="language-text line-numbers-mode">

``` text
1.   NodeA    step#1
2.   NodeA    step#2
3.   NodeA    step#3
4.   NodeB    step#1
5.   NodeB    step#2
6.   NodeB    step#3
```

</div>

Sequential flow illustrated:

<div class="language-text line-numbers-mode">

``` text
1.   NodeA    step#1
2.   NodeB    step#1
3.   NodeA    step#2
4.   NodeB    step#2
5.   NodeA    step#3
6.   NodeB    step#3  
```

</div>

The process being automated will determine which strategy is correct, though the node-oriented flow is more commonplace.

For more complex workflow strategy rules, see [Ruleset Workflow Strategy Plugin](https://docs.rundeck.com/docs/manual/jobs/workflow-strategies/ruleset.html)
