---
title: n8n Security — Credentials, Secrets, and Access Control
description: Understand how n8n encrypts and shares credentials, which controls exist on paid tiers, and what self-hosting changes about where your data lives.
---

# Security and credentials

Automation platforms hold the keys to everything they automate. This page covers where those keys live and who can reach them.

## How credentials are stored

A credential holds a secret — an API key, an OAuth token, a database password — encrypted at rest and stored separately from the workflows that use it.

The separation has a practical consequence: exporting a workflow as JSON exports the reference to a credential, not the secret. You can share a workflow, commit it, or move it between instances without leaking what it authenticates with.

On self-hosted instances, encryption uses `N8N_ENCRYPTION_KEY`. Back it up with the database — a restore without the key leaves every credential unreadable.

## Sharing and access

On a single-user instance, credentials are yours. Beyond that, the controls depend on tier:

- **Sharing with projects.** Credentials are scoped to a project rather than the whole instance, so a contractor working in one project cannot reach production secrets.
- **Roles.** Instance admins, project admins, editors, and viewers separate who can change a workflow from who can only watch it run.
- **SSO with SAML or LDAP.** Available on Business and Enterprise, so access follows your identity provider and revoking there revokes here.
- **Enforced two-factor authentication** across the instance.

## External secret stores

On Enterprise, credentials can be backed by an external secret store rather than n8n's own storage, which keeps rotation in the system that already owns it.

## What self-hosting changes

Self-hosting moves the trust boundary rather than removing it:

- Workflow data stays in your database, on your network. Nothing transits n8n's infrastructure.
- The instance can run with no public egress except the services you allow.
- Every control above — TLS, patching, backups, network isolation — becomes yours to implement.

Cloud reverses that trade: n8n operates the platform, and you accept that execution data is held there under their [privacy terms](https://n8n.io/legal/).

## Sensible defaults

- Give each integration its own credential rather than one key reused everywhere — rotation stays local.
- Never paste a secret into a node parameter or a Code node; that value is stored in plain text with the workflow and appears in execution logs.
- Scope API keys to the narrowest permission the workflow needs.
- Set an expiry on API keys and rotate on a schedule you actually keep.

## Related

- [Self-hosting](./self-hosting.md) — the encryption key and backups
- [Public REST API](../reference/api.md) — API key scopes and expiry
- [FAQ](../reference/faq.md) — data residency questions
