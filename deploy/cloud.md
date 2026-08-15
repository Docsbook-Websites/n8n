---
title: n8n Cloud — Managed Hosting for Your Workflows
description: Run n8n as a managed service with a free trial, no installation, and automatic updates, and understand execution quotas and concurrency limits.
---

# n8n Cloud

n8n Cloud is n8n operated for you. There is no server to provision, patch, or scale, and updates arrive without a maintenance window on your side.

## Start a trial

[Sign up](https://app.n8n.cloud/register) and you get a working instance in the browser. No credit card is required for the trial.

Your instance gets its own URL, which matters more than it sounds: webhook nodes need a publicly reachable address, and on Cloud you have one immediately. Self-hosting on a laptop does not give you that without extra work.

## Quotas that shape how you build

Cloud plans are measured in **monthly workflow executions**, and one execution is one workflow running start to finish regardless of how many nodes it contains. Splitting logic across more nodes never costs more.

Two limits are worth designing around:

- **Concurrent executions** — 5 on Starter, 20 on Pro, 200+ on Enterprise. Runs beyond the limit queue rather than fail.
- **Execution history** — from 7 days on Starter up to unlimited on Enterprise. Anything you need to keep longer should be written out to your own store during the run.

Sub-workflows count as separate executions. A parent calling two sub-workflows is three, not one.

Figures come from the [n8n pricing page](https://n8n.io/pricing/) — confirm current terms there before committing to a plan.

## What Cloud does not do

Some things are only possible when you own the machine:

- Running bash scripts from a workflow.
- Installing custom nodes that are not published community nodes.
- Placing the instance inside a private network with no public egress.

If any of those are requirements, read [Self-hosting](./self-hosting.md).

## Moving between Cloud and self-hosted

Workflows are JSON. You can export from one and import into the other, and the workflow itself carries over unchanged.

Credentials do not. They are stored encrypted per instance and have to be recreated on the target — which is the correct behaviour, and worth planning for rather than discovering during a migration.

<!-- widget:cta -->

## Start on Cloud in about a minute

A hosted instance, a public webhook URL, and no infrastructure to run.

[Start free trial](https://app.n8n.cloud/register) · [Compare plans](../reference/pricing.md)

<!-- /widget -->

## Related

- [Self-hosting](./self-hosting.md) — the other deployment path
- [Pricing and plans](../reference/pricing.md) — tier-by-tier limits
- [Security and credentials](./security.md) — where secrets live
