---
title: n8n Cloud or Self-Hosted — How to Choose
description: Compare n8n Cloud against self-hosting the Community Edition on your own infrastructure, and pick the plan that matches your workload and compliance needs.
---

# Choose how to run n8n

n8n offers two deployment options: **n8n Cloud**, which n8n operates for you, and **self-hosted**, which you run on your own infrastructure. Both are production-ready. The choice comes down to who operates the server and which features you need.

![Decision flowchart comparing n8n Cloud plans against self-hosted editions](https://raw.githubusercontent.com/n8n-io/n8n-docs/main/docs/get-started/.gitbook/assets/choose-your-n8n-diag-light.png)

## Decision one: who runs the server

| Your situation | Choose | Why |
|---|---|---|
| You want to start now | n8n Cloud | Nothing to install |
| You do not want to operate infrastructure | n8n Cloud | Hosting, updates, and scaling are handled |
| You need full control of the environment | Self-hosted | You own the configuration |
| Data cannot leave your network | Self-hosted | The instance runs where you put it |
| You want to run n8n for free | Self-hosted Community Edition | Free, with almost the complete feature set |
| You need SSO, environments, or Git version control | Either | Paid tiers exist for both |

Self-hosting is a real commitment: you handle installation, upgrades, backups, and scaling. Choose it because you want the control, not because it looks cheaper on paper.

## Decision two: which plan

On Cloud, plans are sized by monthly workflow executions. On self-hosted, the Community Edition is free and paid editions add governance features.

| | Starter | Pro | Business | Enterprise |
|---|---|---|---|---|
| Price | €20/mo billed annually | €50/mo billed annually | €667/mo billed annually | Contact sales |
| Monthly executions | 2.5k | 10k | 40k | Custom |
| Concurrent executions | 5 | 20 | — | 200+ |
| Shared projects | 1 | 3 | 6 | Unlimited |
| Insights history | — | 7 days | 30 days | 365 days |
| SSO, SAML, LDAP | — | — | Included | Included |
| Git version control | — | — | Included | Included |
| Support | Forum | Forum | Forum | Dedicated with SLA |

Every plan includes unlimited users, unlimited workflows, and every integration. Figures come from the [n8n pricing page](https://n8n.io/pricing/); check it for the current terms before you commit.

## What counts as an execution

One execution is one workflow running from start to finish, whatever happens inside it. A workflow with four nodes and a workflow with forty nodes each consume one execution. This is the main reason n8n bills differently from tools that charge per step or per task.

Sub-workflows are the exception worth knowing: a workflow called by another workflow counts as its own execution.

## If you are under 20 employees

n8n runs a Start-up Plan offering 50% off Business for companies under 20 employees. Eligibility is assessed by n8n — see the [pricing page](https://n8n.io/pricing/) for the current criteria.

## Next steps

- Going with Cloud: [Set up n8n Cloud](../deploy/cloud.md)
- Going with self-hosted: [Self-hosting guide](../deploy/self-hosting.md)
- Want the full breakdown: [Pricing and plans](../reference/pricing.md)
