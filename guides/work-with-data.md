---
title: Work With Data in n8n — Expressions and Transformations
description: Move and reshape data between n8n nodes using expressions, the Set and Code nodes, and the item structure that every node reads and writes.
---

# Work with data

Most of the work in a workflow is not calling services. It is getting the output of one node into the shape the next node expects.

## The item structure

Data between nodes is an array of items, each holding a `json` object and optionally binary data:

```json
[
  { "json": { "id": 1, "email": "ada@example.com" } },
  { "json": { "id": 2, "email": "grace@example.com" } }
]
```

A node receiving this runs twice, once per item. Understanding that single fact explains most surprising behaviour in n8n — including why a node sometimes appears to run more times than you expected.

## Read values with expressions

An expression reaches data from anywhere earlier in the run:

```javascript
{{ $json.email }}                        // field on the current item
{{ $node["HTTP Request"].json.id }}      // output of a named node
{{ $json.items[0].price }}               // nested value
{{ $now.minus(1, 'day').toISO() }}       // a timestamp, via Luxon
{{ $json.name?.toUpperCase() ?? 'N/A' }} // optional chaining and a fallback
```

That last line is worth copying as a habit. Data from real APIs has missing fields, and `?.` with `??` turns a failed run into a sensible default.

## Reshape with the Set node

**Edit Fields (Set)** builds a clean output object. Use it right after any node whose response is larger than what you need — a 60-field API response passed downstream becomes 60 fields you have to read past every time you debug.

Enable **Include Other Input Fields** only when you actually want the rest carried along.

## Drop into code

When an expression stops fitting on one line, use the **Code** node. It runs JavaScript or Python over the items.

```javascript
// Run Once for All Items
const byDomain = {};

for (const item of $input.all()) {
  const domain = item.json.email.split('@')[1];
  byDomain[domain] ??= [];
  byDomain[domain].push(item.json.email);
}

return Object.entries(byDomain).map(([domain, emails]) => ({
  json: { domain, count: emails.length, emails },
}));
```

Two modes, and the choice matters:

- **Run Once for All Items** — the code runs once and sees the whole set through `$input.all()`. Required for grouping, sorting, or aggregating.
- **Run Once for Each Item** — the code runs per item and sees `$json`. Simpler when each item is independent.

Whatever you return must be a list of objects with a `json` key. Returning a bare array of values is the most common Code node error.

## Binary data

Files — downloads, uploads, generated PDFs — travel on the item's `binary` property, separate from `json`. Nodes that produce files write there, nodes that consume them read from there, and the field name (`data` by default) has to match on both sides.

Binary data is held in memory during a run. Moving large files through many nodes is the usual cause of memory pressure on small self-hosted instances.

## Related

- [Flow logic](./flow-logic.md) — routing the data you just reshaped
- [Core concepts](../get-started/core-concepts.md) — items and expressions, from the top
- [Handle errors](./error-handling.md) — when a transformation hits a missing field
