---
title: Handle Errors in n8n Workflows — Retries and Error Workflows
description: Keep automations reliable with node-level retries, per-node failure branches, and a dedicated error workflow that reports every failed run.
---

# Handle errors

Every workflow that talks to a network will fail eventually. The question is whether it fails loudly, retries, or stops without anyone noticing.

## What happens by default

When a node throws, the execution stops there and is marked failed. Nodes after it do not run. The failure appears under **Executions**, and nowhere else — no email, no alert.

That default is fine while building and dangerous in production. A workflow that has been failing every night for two weeks looks identical to one that is working, until you open the list.

## Retry a flaky call

Transient failures — timeouts, 502s, rate limits — usually succeed on a second attempt. Every node has retry settings under its **Settings** tab:

- **Retry On Fail** — turn it on.
- **Max Tries** — 3 is a sensible default.
- **Wait Between Tries** — 1000 ms or more, higher when the API rate-limits.

Retry only what is idempotent. Retrying a GET is free. Retrying a POST that creates an order can create three orders.

## Continue instead of stopping

Sometimes one bad item should not kill the run. The node's **On Error** setting decides:

| Setting | Behaviour | Use when |
|---|---|---|
| Stop Workflow | Execution fails immediately | The rest is meaningless without this step |
| Continue | Passes the error on as data | You want to handle it downstream |
| Continue (using error output) | Adds a second output for failures | You want a real branch for failed items |

The third option is the one to reach for on batch work: successful items continue down the main path, failed ones go down the error output and get logged, queued, or reported — without stopping the other 199.

## Get told when a run fails

An **error workflow** runs automatically whenever another workflow fails. This is the piece most setups are missing.

<!-- widget:stepper -->

### Create a workflow with an Error Trigger

Add the **Error Trigger** node. It fires only when a workflow that references it fails.

### Send the failure somewhere people look

Add a Slack, email, or PagerDuty node. The trigger's output carries the workflow name, the execution ID, the failing node, and the error message — include all four so the message is actionable on its own.

### Point your workflows at it

In each production workflow, open **Settings > Error Workflow** and select this one. It is per-workflow, so do it as part of shipping rather than as a later cleanup.

<!-- /widget -->

## Fail on purpose

The **Stop and Error** node throws deliberately. Use it when the data is wrong in a way that should not be quietly accepted — a missing customer ID, a negative amount, an empty required field.

A run that stops with "order 4471 has no customer" is far cheaper to diagnose than one that writes a broken record and succeeds.

## A production checklist

Before activating a workflow:

- Retries enabled on every external call that is safe to repeat.
- An error workflow attached, sending somewhere a person reads.
- Batch steps using the error output rather than stopping the whole run.
- Validation on inputs you do not control, with Stop and Error where it matters.

## Related

- [Flow logic](./flow-logic.md) — branching, including error branches
- [Work with data](./work-with-data.md) — defensive expressions for missing fields
- [Self-hosting](../deploy/self-hosting.md) — what fails at the infrastructure level
