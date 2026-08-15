---
title: n8n Flow Logic — Branch, Loop, Merge, and Wait
description: Control how data moves through an n8n workflow using conditional branching, loops over items, merging parallel paths, and waits between steps.
---

# Flow logic

A workflow that runs top to bottom covers surprisingly little. Real automations branch on conditions, process batches, wait for something, and recombine paths. These are the nodes that do it.

## Branch on a condition

Two nodes split a flow, and picking the wrong one produces workflows nobody can read later.

**If** takes one condition and gives you two outputs, true and false. Use it when the question is genuinely binary.

**Switch** takes one value and routes to many outputs. Use it when you are dispatching on a category — an order status, a country, an event type. Four chained If nodes is a Switch that has not been noticed yet.

```javascript
// If node condition, expression mode
{{ $json.status === 'active' && $json.credits > 0 }}
```

An output with nothing connected to it ends that branch. That is a legitimate way to drop items you do not want.

## Loop over items

Most of the time you do not need a loop. When a node receives 200 items it runs 200 times on its own — iteration is the default, not something you request.

You need **Loop Over Items (Split in Batches)** when:

- An API rate-limits you and you must send 10 at a time rather than 200 at once.
- Each iteration depends on the result of the previous one.
- Memory matters and you would rather not hold the whole set at once.

Set **Batch Size**, connect the loop output back into the node, and take the **done** output when the set is exhausted.

## Merge parallel paths

**Merge** recombines two inputs. The mode decides what "recombine" means, and this is where most confusion lives:

| Mode | What it does | Use it when |
|---|---|---|
| Append | Stacks input 2 after input 1 | You want one combined list |
| Combine by matching fields | Joins on a key, like a SQL join | Each side holds part of the same record |
| Combine by position | Pairs item 1 with item 1, and so on | Two lists in a known, identical order |
| Choose branch | Passes one input, waits for both | You need synchronisation, not data |

Combine by position is the one that quietly breaks: it assumes an ordering guarantee that APIs rarely make. Match on a field whenever a field exists.

## Wait

**Wait** pauses execution — for a fixed interval, until a specific time, or until a webhook is called.

The third variant is what makes human approval possible: the workflow parks, someone clicks a link in the message you sent them, the webhook fires, and the run continues from exactly where it stopped. That pattern is covered in [AI agents and chains](./ai-workflows.md), where letting a model act unsupervised is often the wrong call.

## Split work into sub-workflows

When a canvas stops fitting on a screen, extract part of it into its own workflow and call it with **Execute Sub-workflow**. You get reuse and a smaller surface to reason about.

One billing consequence to keep in mind: a sub-workflow run counts as its own execution. Splitting a workflow in three means three executions per logical run.

## Related

- [Work with data](./work-with-data.md) — reshape what flows between these nodes
- [Handle errors](./error-handling.md) — what happens when a branch fails
- [Core concepts](../get-started/core-concepts.md) — items and executions
