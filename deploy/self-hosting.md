---
title: Self-Host n8n — Docker Compose, npm, and Cloud Providers
description: Install and operate the source-available n8n Community Edition on your own infrastructure, with the environment variables and persistence settings production needs.
---

# Self-hosting n8n

The Community Edition is free, source-available under a fair-code license, and has almost the complete feature set. You run it, you upgrade it, you back it up.

## Try it in one command

With Node.js between 20.19 and 24.x installed:

```bash
npx n8n
```

n8n starts on [http://localhost:5678](http://localhost:5678). Good for evaluating; not a deployment. npm-based installs are deprecated from n8n 3.0, and the AI Assistant is unavailable on them.

## Docker Compose is the recommended path

Docker avoids the operating system and tooling incompatibilities that npm installs run into, and it makes upgrades a matter of changing a tag.

<!-- widget:stepper -->

### Install Docker

Install [Docker Desktop](https://docs.docker.com/get-docker/) on Mac, Windows, or Linux, or Docker Engine plus Docker Compose on a headless Linux server.

### Take a working compose file

n8n publishes configurations for several architectures in the [n8n-hosting repository](https://github.com/n8n-io/n8n-hosting) — single instance, Postgres, and queue mode among them. Start from the one closest to your target rather than writing your own.

### Persist the data

n8n's state lives in `/home/node/.n8n`. Mount a named volume there. Without it, every container restart loses your workflows, credentials, and encryption key.

### Set the environment

At minimum, set the timezone, the public URL, and a database. Details below.

### Start it

```bash
docker compose up -d
```

Check `docker compose logs -f` on first boot — database connection problems surface there and nowhere else.

<!-- /widget -->

## Environment variables that matter

| Variable | Why it matters |
|---|---|
| `N8N_ENCRYPTION_KEY` | Encrypts stored credentials. Set it explicitly and back it up — lose it and every credential must be re-entered |
| `WEBHOOK_URL` | The public URL n8n advertises for webhooks. Wrong value means external services call an address that does not resolve |
| `GENERIC_TIMEZONE` | The timezone schedule triggers use. Defaults to UTC, which is rarely what a cron expression was written for |
| `DB_TYPE` | `postgresdb` for anything real. SQLite is the default and does not survive concurrent load |
| `N8N_HOST`, `N8N_PORT`, `N8N_PROTOCOL` | How n8n builds its own URLs behind a reverse proxy |

The encryption key is the one that ends badly. It is generated on first run and stored in the data directory — if that directory is not persisted, a restart produces a new key and every credential becomes unreadable.

## Use Postgres, not SQLite

SQLite is the default and is fine for a single-user trial. For production use Postgres: it handles concurrent executions, survives larger execution histories, and is required for queue mode.

## Scale with queue mode

A single n8n process runs the editor and the executions together. Under load, workflow runs compete with the interface.

Queue mode splits them: a main instance serves the UI and enqueues work, worker instances consume the queue via Redis. Add workers to add throughput. This is also what makes multiple instances possible behind a load balancer.

## Cloud providers

n8n documents deployments for AWS, Azure, Google Cloud Run, Google Kubernetes Engine, DigitalOcean, Heroku, and others. All follow the same shape: a container, a persistent volume, a Postgres database, and a public HTTPS endpoint for webhooks.

## What you take on

Self-hosting is free of licence cost, not free of work:

- **Upgrades.** You choose when, and you read the breaking-change notes.
- **Backups.** The database and the encryption key. A backup missing the key restores nothing usable.
- **TLS and reverse proxying.** Webhooks need a valid certificate on a public address.
- **Monitoring.** Nobody is paged when your instance stops.

If that list reads as a cost rather than a feature, [n8n Cloud](./cloud.md) does it for you.

## Related

- [n8n Cloud](./cloud.md) — the managed alternative
- [Security and credentials](./security.md) — encryption and secret handling
- [Handle errors](../guides/error-handling.md) — failures above the infrastructure layer
