---
title: n8n FAQ — Executions, Quotas, Licensing, and Hosting
description: Direct answers to the questions that come up when evaluating n8n: how executions are counted, what happens at a quota, licensing terms, and migration.
---

# Frequently asked questions

<!-- widget:accordion -->

### What exactly counts as one execution?

One workflow running from start to finish. Node count and complexity do not change it — four nodes and forty nodes each cost one execution.

Two cases add up faster than people expect: sub-workflows count as their own executions, and manual test runs during building count too.

### Why does n8n bill per execution instead of per step?

Because per-step billing penalises clear workflows. Under it, splitting one dense node into five readable ones raises the bill, so you are paid to write worse automations. Per-execution pricing removes that pressure.

### What happens when I hit my execution quota?

Behaviour depends on plan and billing arrangement. n8n covers this on the [pricing page](https://n8n.io/pricing/) FAQ — check there rather than assuming, since the answer differs between self-serve and contracted plans.

### Is the free trial limited in features?

The trial gives you a working Cloud instance without a credit card. One notable exception: the public REST API is not available during the trial. Everything else needed to evaluate the product is.

### Is n8n open source?

n8n is **fair-code** licensed, not OSI open source. The source is available, self-hosting the Community Edition is free, and you can read and modify the code.

The difference from MIT-style licensing is commercial: the Sustainable Use License restricts reselling n8n as a hosted service to third parties. Internal use, however large, is unrestricted.

### Can I self-host for free, permanently?

Yes. The Community Edition is free with almost the complete feature set. You take on installation, upgrades, backups, TLS, and monitoring in exchange.

Paid self-hosted editions add governance features — SSO, environments, Git version control — under a licence key.

### What can Cloud do that self-hosted cannot, and the reverse?

Cloud gives you a public HTTPS webhook URL immediately, managed updates, and no infrastructure work.

Self-hosting lets you run bash scripts from workflows, install arbitrary custom nodes, and keep the instance on a private network. Those three are not available on Cloud.

### Can I move from Cloud to self-hosted later?

Yes. Workflows are JSON and import cleanly in either direction.

Credentials do not transfer — they are encrypted per instance and must be re-entered on the target. Plan for that as a migration step rather than discovering it mid-move.

### Where is my data stored?

On self-hosted instances, in your database on your infrastructure; nothing transits n8n. On Cloud, execution data is held by n8n under their [legal terms](https://n8n.io/legal/). If data residency is a hard requirement, self-host.

### Do I need to know how to code?

No, and it helps. The canvas covers a great deal without code. When you need more, the Code node runs JavaScript or Python, and the HTTP Request node reaches any REST API. Teams usually mix both in the same workflow.

### Why did my workflow stop running after I edited it?

The usual cause is deactivation: saving certain changes turns **Active** off, and a schedule or webhook trigger does nothing while inactive. Check the toggle at the top right first — it accounts for most "it just stopped" reports.

### How do I get told when a workflow fails?

Attach an error workflow. Failures are otherwise recorded only in the executions list, where nobody looks until they are already looking for a problem. See [Handle errors](../guides/error-handling.md).

<!-- /widget -->

## Related

- [Pricing and plans](./pricing.md) — tier limits in full
- [Choose how to run n8n](../get-started/choose-how-to-use-n8n.md) — the deployment decision
- [Handle errors](../guides/error-handling.md) — failure notification setup
