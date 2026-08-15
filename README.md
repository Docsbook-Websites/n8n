---
title: n8n Documentation — Build AI Workflows and Automations
description: Learn how to build, deploy, and run n8n workflow automations. Start on n8n Cloud in minutes or self-host the source-available Community Edition.
---

# n8n Documentation

n8n is a workflow automation platform for technical teams. You build automations on a visual canvas, drop into JavaScript or Python whenever the canvas is not enough, and run the result either on n8n Cloud or on your own servers.

Two things make it different from most automation tools. You are billed per full workflow execution rather than per step, so a workflow with 40 nodes costs the same as one with 4. And the source is available under a fair-code license, so self-hosting the Community Edition is free and has almost the complete feature set.

<!-- widget:cards -->

## Start here

- [Get started](./get-started/README.md) — Pick Cloud or self-hosted, then build a working workflow {rocket}
- [Build your first workflow](./get-started/build-your-first-workflow.md) — A schedule trigger, an API call, and a condition, end to end {play}
- [Core concepts](./get-started/core-concepts.md) — Nodes, executions, credentials, and expressions in one pass {lightbulb}

## Build

- [Flow logic](./guides/flow-logic.md) — Branch, loop, merge, and wait inside a workflow {git-branch}
- [Work with data](./guides/work-with-data.md) — Move and reshape data between nodes using expressions {braces}
- [AI agents and chains](./guides/ai-workflows.md) — Give a model tools, memory, and your own data {bot}
- [Handle errors](./guides/error-handling.md) — Retries, error workflows, and what happens when a run fails {shield-alert}

## Run it

- [n8n Cloud](./deploy/cloud.md) — Managed hosting, free trial, no server to operate {cloud}
- [Self-hosting](./deploy/self-hosting.md) — Docker Compose, npm, and cloud providers {server}
- [Security and credentials](./deploy/security.md) — How secrets are stored and shared {lock}

## Reference

- [Public REST API](./reference/api.md) — Drive workflows, executions, and credentials programmatically {code}
- [Pricing and plans](./reference/pricing.md) — What each plan includes and where the limits sit {credit-card}
- [FAQ](./reference/faq.md) — Executions, quotas, licensing, and self-host questions {circle-help}

<!-- /widget -->

## What you can build

n8n covers the same ground as a scripting cron job, an integration platform, and an AI agent framework, which is why the examples look so different from each other:

- **Scheduled data movement.** Pull from an API every morning, reshape the payload, write it to a database or a sheet.
- **Webhook-driven services.** Expose an endpoint, run logic against the request, return a response — an API without a codebase to deploy.
- **AI agents with real tools.** Give a model access to your systems and let it decide which to call, with a human approval step where it matters.
- **Internal glue.** The integrations nobody wants to own as a service: alert routing, onboarding steps, report assembly.

<!-- widget:cta -->

**Two ways to start**

## Run your first workflow today

Start free on n8n Cloud with no credit card, or install the Community Edition on your own machine with a single command.

[Start free trial](https://app.n8n.cloud/register) · [Self-host instead](./deploy/self-hosting.md)

<!-- /widget -->

## Next steps

- New to n8n? Start with [Get started](./get-started/README.md).
- Deciding how to run it? Read [Cloud or self-hosted](./get-started/choose-how-to-use-n8n.md).
- Looking for a specific term? Check the [glossary](./reference/glossary.md).
