---
title: n8n Glossary — Platform and AI Terms Explained
description: Definitions of the terms used across n8n documentation, covering workflow building blocks, execution behaviour, and the AI concepts behind agents and RAG.
---

# Glossary

<!-- widget:accordion -->

### Workflow

A set of connected nodes that runs as a unit. The first node is a trigger; the rest transform or act on the data passed along.

### Node

One step in a workflow. It receives items, performs an operation, and outputs items. Nodes are either service-specific (Slack, Postgres) or general (HTTP Request, Code, If).

### Trigger node

The first node, which decides when a workflow runs — on a schedule, on an incoming webhook, on an event in a connected service, or manually.

### Item

One unit of data moving between nodes: a JSON object, optionally with binary data attached. Nodes receiving many items usually run once per item.

### Execution

One run of a workflow from start to finish. Executions are the unit plans are billed in, and each is stored with the data that passed through every node.

### Credential

A stored, encrypted secret for a service — API key, OAuth token, database password — kept separately from the workflows that use it.

### Expression

A snippet in double curly braces that pulls a value from elsewhere in the run, such as `{{ $json.email }}`, usable anywhere a field accepts input.

### Canvas

The editor surface where you add and connect nodes.

### Cluster node

A group of nodes that work together: a root node plus sub-nodes extending its functionality. AI agent nodes with attached models, memory, and tools are the common example.

### Sub-workflow

A workflow called by another workflow. It runs as its own execution and returns its result to the caller.

### Queue mode

A self-hosted configuration where a main instance serves the editor and enqueues work while separate worker instances execute it, coordinated through Redis.

### AI agent

An AI system given a goal and a set of tools that decides for itself which tools to call and in what order. Unlike a chain, it can use persistent memory.

### AI chain

A fixed sequence of calls to a language model and related components. Chains have no persistent memory, so they cannot reference earlier turns of a conversation.

### Tool

A resource an AI agent can call to fetch information or take action — in n8n, usually another node, such as an HTTP request or a database query.

### Memory

Storage that lets an AI agent carry context across interactions. In-memory variants reset on restart; database-backed ones persist.

### Embedding

A numerical vector representing a piece of data, letting AI systems compare meaning rather than exact text. Stored in a vector store.

### Vector store

A database built to store and search embeddings, used to retrieve the passages most relevant to a question.

### RAG (retrieval-augmented generation)

A technique that retrieves relevant documents at question time and passes them to a language model as context, so it can answer about information it was never trained on.

### Hallucination

An AI model producing confident output unsupported by its sources. In RAG systems the usual cause is retrieval that returned the wrong passages, not the model itself.

### Groundedness

How closely a model's response reflects its source material. Grounded answers cite what was retrieved; ungrounded ones speculate past it.

### Fair-code

The licensing model n8n uses. The source is available and self-hosting is free, but the Sustainable Use License restricts reselling n8n as a hosted service to third parties.

<!-- /widget -->

## Related

- [Core concepts](../get-started/core-concepts.md) — the main terms with examples
- [AI agents and chains](../guides/ai-workflows.md) — the AI terms in practice
