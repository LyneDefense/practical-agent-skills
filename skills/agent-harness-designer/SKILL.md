---
name: agent-harness-designer
description: |
  Design or review a single-agent harness using the Learn Claude Code s01-s07 mental model.
  Use when users want to build an agent, choose between todo/task/subagent/skill/compact,
  reason about prompt vs tool schema vs skill, or review an agent architecture before adding
  collaboration. Focus on loop, tools, planning, skills, context compaction, and external task state.
  Keywords: agent harness, todo, task, subagent, skill loading, context compact, tool schema, prompt
---

# Agent Harness Designer

Use this skill to design or critique a **single-agent** system. Stay within the `s01-s07` scope unless the user explicitly asks for collaboration or multi-agent orchestration.

## Core View

Treat the agent as:

```text
agent = model + loop + tools + state + optional on-demand knowledge
```

The model decides. The harness supplies:

- tools
- short-term execution state
- external task state when needed
- context hygiene
- optional domain knowledge

## What Each Mechanism Is For

| Mechanism | Use it when | Avoid it when |
|---|---|---|
| Minimal loop | You need a base agent that can act | You are trying to solve planning/state problems with prompt only |
| Tool schema | The model needs clear action affordances | Tool names/descriptions are vague or overlapping |
| `todo` | A multi-step task needs visible short-term execution steps | You need durable dependency graphs |
| `subagent` | A subproblem is noisy, exploratory, or would pollute the main context | You only need another tool call, not an isolated context |
| `skill` | A task needs domain method, checklist, or specialized procedure | The knowledge should always be in the system prompt |
| `compact` | Context is growing and old details no longer need verbatim retention | The real problem is missing external state |
| `task` | Work items must survive compression, restart, or dependency tracking | The task is purely local and short-lived |

## Distinguish These Clearly

### System prompt

Use for:

- role
- priorities
- high-level operating rules

Do not stuff large domain manuals here.

### Tool schema

Use for:

- action names
- action purpose
- parameters and constraints

Treat tool schema as the model's executable interface definition.

### Skill body

Use for:

- domain procedure
- review checklist
- output structure
- task-specific heuristics

Treat it as an on-demand professional prompt module.

## Decision Workflow

When designing an agent, answer these questions in order:

1. What is the job-to-be-done?
2. What are the minimum tools required?
3. Does the agent need visible short-term execution state?
4. Does any state need to live outside the conversation?
5. Will some subtasks generate too much local noise?
6. Does the task need domain-specific method or checklist?
7. Will context growth become a bottleneck?

Then map answers to mechanisms:

- short-term execution visibility -> `todo`
- durable or dependency-aware work items -> `task`
- noisy isolated investigation -> `subagent`
- domain procedure -> `skill`
- long-running sessions -> `compact`

## Recommended Design Pattern

```text
1. Start with the smallest useful loop.
2. Add only the tools the job really needs.
3. Add `todo` if multi-step work drifts.
4. Add `subagent` if exploratory work pollutes the main thread.
5. Add `skill` if the task has reusable domain method.
6. Add `compact` when message growth becomes a real constraint.
7. Add `task` when important work state must survive the conversation.
```

## Short Decision Rules

### When to choose `todo` vs `task`

- Choose `todo` for current-session execution steps.
- Choose `task` for durable work items, dependency tracking, or resumability.
- If both are needed: `task` is the outer work object, `todo` is the current execution expansion.

### When to choose `subagent`

Use a subagent when:

- the subproblem is exploratory
- the main thread only needs a summary
- intermediate reads/searches would clutter the parent context

Do not use a subagent just because a task is long. Use it because the context should be isolated.

### When to choose `skill`

Use a skill when the task benefits from a reusable professional method, such as:

- code review
- contract review
- PDF extraction
- testing workflow

If the knowledge is broad but rarely needed, do not preload it. Make it loadable.

### When to choose `compact`

Use compaction when:

- tool results are accumulating
- older raw outputs no longer need verbatim retention
- sessions are long enough that context length becomes a real cost or failure mode

Remember: compaction manages conversation memory; it does not replace external task state.

## Review Checklist

When reviewing an agent design, check:

- Is the loop simple and intact?
- Are tools atomic and clearly described?
- Is the system overusing prompt where state should be structured?
- Is `todo` being used for short-term execution, not long-term work tracking?
- Is `task` being used only when external state is justified?
- Is `subagent` solving context isolation rather than pretending to be a team?
- Is domain knowledge loaded on demand instead of bloating the base prompt?
- Is there a plan for context growth?

## Output Format

When helping a user design or review an agent, structure the answer as:

### Goal

What the agent is supposed to accomplish.

### Recommended Harness

- loop
- tools
- execution state
- external state
- knowledge loading
- context strategy

### Why

Explain why each mechanism is or is not needed.

### Minimal Version

Describe the smallest design that should work first.

### Later Upgrades

List only upgrades justified by failure modes or growth.

## Anti-Patterns

Avoid these mistakes:

- solving everything with a bigger prompt
- adding `task` when `todo` is enough
- adding `subagent` when a normal tool call is enough
- treating `skill` as a dump for all documentation
- keeping long raw tool outputs forever
- using two overlapping state systems without defining which one is authoritative

## Boundary

This skill is for single-agent harness design up through:

- loop
- tools
- todo
- subagent
- skill loading
- context compaction
- task system

Do not proactively expand into background jobs, mailboxes, or multi-agent teamwork unless the user asks for those explicitly.

