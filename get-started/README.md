---
title: Get Started With n8n — From Zero to a Running Workflow
description: Choose between n8n Cloud and self-hosting, learn the core concepts, and build your first working automation in about fifteen minutes.
---

# Get started

This section takes you from nothing to a workflow that runs on a schedule and does real work. Budget about fifteen minutes.

The order matters: decide where n8n runs, learn the four concepts everything else is built on, then build something.

<!-- widget:cards -->

- [Choose how to run n8n](./choose-how-to-use-n8n.md) — Cloud or self-hosted, and which plan fits {git-fork}
- [Core concepts](./core-concepts.md) — Nodes, executions, credentials, expressions {lightbulb}
- [Build your first workflow](./build-your-first-workflow.md) — A full tutorial with a trigger, an API call, and a condition {play}

<!-- /widget -->

## The shortest possible start

If you want to skip the reading, this gets you a running n8n on your own machine. You need Node.js between 20.19 and 24.x:

```bash
npx n8n
```

Open [http://localhost:5678](http://localhost:5678) and the editor is there. Nothing is saved to a server you do not control, and nothing is billed.

For anything beyond trying it out, use Docker Compose instead — see [Self-hosting](../deploy/self-hosting.md). npm-based installs are deprecated from n8n 3.0.

## What a workflow actually is

A workflow is a set of **nodes** connected on a canvas. The first node is a **trigger**: a schedule, an incoming webhook, a message in a queue, or a manual click. Every node after it receives the items the previous node produced, does something to them, and passes the result on.

When a workflow runs from start to finish, that is one **execution**. Your plan is measured in executions, not in nodes or steps, which is why splitting logic across more nodes never costs more.

![The n8n editor showing a completed workflow on the canvas](https://raw.githubusercontent.com/n8n-io/n8n-docs/main/docs/get-started/.gitbook/assets/tutorial-first.png)

## Next steps

- Decide where it runs: [Choose how to run n8n](./choose-how-to-use-n8n.md)
- Understand the vocabulary: [Core concepts](./core-concepts.md)
- Build something: [Build your first workflow](./build-your-first-workflow.md)
