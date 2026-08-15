---
title: Build AI Agents and Chains in n8n Workflows
description: Give a language model real tools, memory, and your own documents inside an n8n workflow, and keep a human in the loop where the cost of a wrong action is high.
---

# AI agents and chains

n8n runs language models as nodes on the same canvas as everything else. That matters because a model on its own can only produce text — the value comes from what it is allowed to call, and n8n already speaks to those systems.

## Chains or agents

Two shapes, and picking the wrong one is the most common mistake.

**A chain** runs a fixed sequence of model calls. You decide the steps; the model fills in the text. It has no persistent memory, so it cannot reference earlier turns of a conversation. Use it for classification, summarisation, extraction — anything where the path is known in advance.

**An agent** is given a goal and a set of tools, and decides for itself which tools to call and in what order. It can use memory, so it can hold a conversation. Use it when the path genuinely depends on what it finds.

Agents are slower, cost more tokens, and are harder to predict. Reach for a chain first, and move to an agent only when the branching is real.

## What a tool is

A tool is a node the agent can decide to call. Most n8n nodes can be attached to an agent as a tool: an HTTP Request against your internal API, a database query, a search over your own documents, another workflow entirely.

The tool's description is not documentation — it is the instruction the model reads when choosing. "Search customer orders by email address; returns the five most recent" produces sane calls. "Order tool" produces guesswork.

## Memory

Memory lets an agent see earlier turns. Without it, every message starts from nothing.

- **Simple memory** keeps the conversation in the instance's memory. Fine for testing; lost on restart.
- **Database-backed memory** (Postgres, Redis, and others) survives restarts and works when several instances share the load.

Memory grows with the conversation, and long histories cost tokens on every call. Window sizes exist for that reason.

## Answer from your own documents

Retrieval-augmented generation — RAG — is how a model answers about content it was never trained on. The shape is always the same:

<!-- widget:stepper -->

### Split the documents

Break source files into chunks small enough to retrieve precisely, large enough to keep meaning. A chunk that cuts a sentence in half retrieves badly.

### Embed and store

Run the chunks through an embedding model and write the vectors to a vector store. n8n has nodes for the common ones.

### Retrieve at question time

Embed the incoming question, pull the nearest chunks from the store, and pass them to the model as context.

### Answer from what was retrieved

Instruct the model to answer from the supplied context and to say when the context does not contain the answer. Without that instruction it will fill the gap confidently.

<!-- /widget -->

Retrieval quality is what makes or breaks a RAG system. When answers are wrong, inspect the chunks that were retrieved before you change the prompt — the model usually answered the context it was given faithfully.

## Keep a human in the loop

An agent that can send email, move money, or delete records should not act unsupervised.

The pattern uses [Wait](./flow-logic.md): the workflow prepares the action, sends it to a person for review, and pauses until a webhook is called. Approve and it continues; ignore it and nothing happens. The cost of that step is one message; the cost of skipping it is whatever the agent did.

## Related

- [Flow logic](./flow-logic.md) — the Wait node behind human approval
- [Handle errors](./error-handling.md) — models fail differently from APIs
- [Glossary](../reference/glossary.md) — agents, chains, embeddings, RAG
