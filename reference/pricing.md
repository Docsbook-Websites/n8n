---
title: n8n Pricing and Plans — What Each Tier Includes
description: Compare n8n Cloud plans and self-hosted editions by executions, concurrency, projects, and governance features, and see what counts against your quota.
---

# Pricing and plans

n8n bills Cloud plans by monthly workflow executions. Every plan includes unlimited users, unlimited workflows, and every integration — the tiers differ in volume, concurrency, and governance features.

Figures on this page come from the [n8n pricing page](https://n8n.io/pricing/). Check there for current terms before purchasing.

## Cloud plans

| | Starter | Pro | Business | Enterprise |
|---|---|---|---|---|
| Price | €20/mo billed annually | €50/mo billed annually | €667/mo billed annually | Contact sales |
| Monthly executions | 2.5k | 10k | 40k | Custom |
| Concurrent executions | 5 | 20 | — | 200+ |
| Shared projects | 1 | 3 | 6 | Unlimited |
| Saved executions | 2.5k | 25k | — | 50k |
| Execution log retention | 7 days | 30 days | — | Unlimited |
| Insights history | — | 7 days | 30 days | 365 days |
| AI Assistant credits | 2,300/month | Up to 13,700/month | — | — |
| SSO, SAML, LDAP | — | — | Included | Included |
| Git version control | — | — | Included | Included |
| Separate environments | — | — | Included | Included |
| External secret store | — | — | — | Included |
| Log streaming | — | — | — | Included |
| Support | Forum | Forum | Forum | Dedicated with SLA |

Annual billing saves 17% against monthly. A free trial is available with no credit card required.

## Self-hosted editions

The **Community Edition** is free and source-available, with almost the complete feature set. Paid self-hosted editions (Business and Enterprise) add the governance features above under a licence key.

Some capabilities exist only when you own the machine: running bash scripts from a workflow, and installing custom nodes.

## What counts as an execution

One execution is one workflow running from start to finish, regardless of how many nodes it contains or how complex they are. A four-node workflow and a forty-node workflow each cost one.

This is the substantive difference from tools that bill per step or per task: adding nodes to make a workflow clearer never raises the bill.

Two things to plan around:

- **Sub-workflows count separately.** A parent calling two sub-workflows uses three executions per logical run.
- **Manual test runs count.** Building iteratively consumes quota, which matters most on Starter.

## Choosing a tier

| Situation | Plan |
|---|---|
| Evaluating, or a handful of personal automations | Starter, or self-hosted Community |
| Production workflows for a small team | Pro |
| Multiple teams, SSO required, Git-tracked workflows | Business |
| Compliance requirements, SLA support, high concurrency | Enterprise |
| Full infrastructure control, no licence cost | Self-hosted Community |

Companies under 20 employees may qualify for the Start-up Plan at 50% off Business.

## Estimating your volume

Count triggers, not nodes. A workflow on a five-minute schedule runs about 8,640 times a month on its own — which is already past Starter. A workflow triggered by a webhook runs as often as that event happens.

When the schedule is the dominant cost, widening the interval is usually cheaper than upgrading.

<!-- widget:cta -->

## Try it before choosing a plan

The trial does not ask for a card, and self-hosting the Community Edition costs nothing at all.

[Start free trial](https://app.n8n.cloud/register) · [Self-host instead](../deploy/self-hosting.md)

<!-- /widget -->

## Related

- [Choose how to run n8n](../get-started/choose-how-to-use-n8n.md) — Cloud against self-hosted
- [n8n Cloud](../deploy/cloud.md) — quotas and concurrency in practice
- [FAQ](./faq.md) — what happens when you hit a quota
