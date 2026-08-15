---
title: n8n Public REST API — Endpoints and Authentication
description: Manage n8n workflows, executions, and credentials programmatically over the public REST API, including key creation, headers, and pagination.
---

# Public REST API

The public API lets you drive n8n from outside the editor — activate workflows from a deploy pipeline, pull execution results into a dashboard, or manage instances in bulk.

The API is not available during the Cloud free trial. Self-hosted instances have it from the start.

## Create an API key

1. Log in to n8n.
2. Go to **Settings > n8n API**.
3. Select **Create an API key**.
4. Set a **Label** and an **Expiration**.
5. On Enterprise, choose the **Scopes** the key is allowed to use.
6. Copy the key. It is shown once.

## Authenticate

Send the key in the `X-N8N-API-KEY` header on every request:

```bash
curl -X GET \
  'https://<your-instance>/api/v1/workflows?active=true' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```

Self-hosted instances use `<N8N_HOST>:<N8N_PORT>/<N8N_PATH>/api/v1/...`. Cloud instances use your instance URL.

<!-- widget:api -->

## GET /api/v1/workflows

List workflows on the instance. Use this to find a workflow's ID before acting on it.

| Field | Type | Required | Description |
|---|---|---|---|
| `active` | boolean | no | Return only active or only inactive workflows |
| `tags` | string | no | Comma-separated tag names to filter by |
| `limit` | number | no | Results per page, up to 250 |
| `cursor` | string | no | Cursor from a previous response, for the next page |

### Example

```bash
curl -X GET \
  'https://<your-instance>/api/v1/workflows?active=true&limit=50' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```

## GET /api/v1/executions

List executions, newest first. This is how you monitor runs from outside n8n.

| Field | Type | Required | Description |
|---|---|---|---|
| `status` | string | no | Filter by `error`, `success`, or `waiting` |
| `workflowId` | string | no | Only executions of this workflow |
| `includeData` | boolean | no | Include the data that passed through each node |
| `limit` | number | no | Results per page, up to 250 |

### Example

```bash
curl -X GET \
  'https://<your-instance>/api/v1/executions?status=error&limit=20' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```

## POST /api/v1/workflows/{id}/activate

Activate a workflow so its trigger starts firing. The inverse is `/deactivate`.

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string | yes | The workflow ID |

### Example

```bash
curl -X POST \
  'https://<your-instance>/api/v1/workflows/1234/activate' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```

<!-- /widget -->

## Pagination

List endpoints are cursor-paginated. A response containing `nextCursor` has more results; pass it as `cursor` on the following request. When `nextCursor` is absent, you have reached the end.

Do not build pagination on offsets — executions are being written while you page, and an offset walk will skip records.

## Errors

| Status | Meaning |
|---|---|
| `401` | Missing, invalid, or expired API key |
| `403` | The key lacks the scope for this operation |
| `404` | No such workflow or execution |

## Related

- [Security and credentials](../deploy/security.md) — key scoping and rotation
- [Handle errors](../guides/error-handling.md) — reacting to failed executions
