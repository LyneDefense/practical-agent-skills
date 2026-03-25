---
name: agent-evaluation
description: |
  Evaluate an AI agent's quality and identify how to improve it.
  Use when users ask how to measure an agent, discuss accuracy/success rate,
  design an eval set, choose evaluation dimensions, analyze failures, or improve
  agent performance across prompt, tools, state, knowledge, and environment layers.
  Keywords: agent evaluation, accuracy, success rate, eval, benchmark, failure analysis, robustness
---

# Agent Evaluation

Use this skill to evaluate an agent systematically and recommend targeted improvements. Do not reduce evaluation to a single "accuracy" number unless the task genuinely has a single-label answer format.

## Core Principle

For most agents, the right question is not:

- "What is this agent's accuracy?"

The right questions are:

- What tasks is this agent supposed to complete?
- What counts as success?
- Is failure coming from understanding, tool use, planning, knowledge, or environment?

## Main Evaluation Dimensions

Always reason across these dimensions:

| Dimension | Ask this |
|---|---|
| Task success | Did the agent actually complete the job? |
| Final correctness | Is the final result correct? |
| Process quality | Were the intermediate actions sensible and safe? |
| Efficiency | How many turns, tools, tokens, or minutes did it take? |
| Robustness | Does it still work when phrasing, inputs, or conditions change? |

Do not treat these as interchangeable.

## Choose Metrics By Agent Type

### Coding agent

Prefer:

- task success rate
- test pass rate
- regression rate
- patch correctness
- average turns
- average tool calls
- constraint violations

### Analysis or document agent

Prefer:

- factual correctness
- key-point recall
- hallucination rate
- output-structure compliance
- human review score when needed

### Tool-using operations agent

Prefer:

- tool selection correctness
- parameter correctness
- execution success rate
- recovery rate after failures
- wasted tool-call ratio

## Recommended Evaluation Workflow

1. Define the target task distribution.
2. Build a task set with realistic examples.
3. Write acceptance criteria per task.
4. Run the agent and record traces.
5. Score both outcomes and process.
6. Classify failures by layer.
7. Improve the weakest layer, not just the prompt.

## Build a Practical Eval Set

For each task, capture:

- input
- expected outcome or acceptance rule
- tool constraints if relevant
- whether human scoring is needed

Cover at least:

- simple tasks
- medium-complexity tasks
- long tasks
- edge cases
- noisy or partial-information cases

## What To Log

At minimum, record:

- final result
- pass/fail against acceptance criteria
- turn count
- tool call sequence
- error and retry events
- elapsed time
- obvious hallucinations or policy violations

If you only store the final answer, you lose most of the diagnostic value.

## Failure Classification

When an agent fails, first classify the failure:

### 1. Task understanding failure

Examples:

- solved the wrong problem
- ignored constraints
- optimized for style instead of correctness

Typical fixes:

- clarify goals
- clarify constraints
- clarify completion conditions

### 2. Tool-use failure

Examples:

- chose the wrong tool
- passed the wrong arguments
- used a broad tool when a precise tool existed

Typical fixes:

- improve tool names
- improve tool descriptions
- reduce overlapping tools
- make parameters clearer

### 3. Planning or execution-state failure

Examples:

- wrong step order
- skipped validation
- drifted during a long task

Typical fixes:

- add `todo`
- add `task`
- add reminders
- make completion state explicit

### 4. Result-judgment failure

Examples:

- claimed success too early
- kept iterating after success
- misread a tool result

Typical fixes:

- tighten acceptance criteria
- add explicit verification
- improve result reporting from tools

### 5. Knowledge failure

Examples:

- lacked domain method
- missed a checklist
- used generic reasoning where specialized procedure was needed

Typical fixes:

- add a skill
- add retrieval
- inject domain references on demand

### 6. Environment or harness failure

Examples:

- tool output too noisy
- poor error messages
- hidden state made diagnosis difficult

Typical fixes:

- improve tool feedback
- structure outputs
- expose state more clearly

## Improvement Strategy

Do not jump to prompt edits first. Diagnose by layer:

| Layer | Common problem | Typical improvement |
|---|---|---|
| Task definition | Goal is vague | Tighten acceptance criteria |
| Prompt | Priorities are unclear | Clarify role, constraints, workflow |
| Tool schema | Tool choice is poor | Improve names, descriptions, params |
| State | Long tasks drift | Add `todo` or `task` |
| Knowledge | Domain method is missing | Add skill or retrieval |
| Environment | Feedback is weak | Improve tool output and errors |

## Minimal Eval Template

Use this structure when asked to propose an evaluation plan:

### Goal

What the agent is supposed to do.

### Task Set

- representative task types
- edge cases
- failure-prone cases

### Acceptance Rules

How pass/fail is determined for each task.

### Metrics

- success
- correctness
- process quality
- efficiency
- robustness

### Logging

What traces and artifacts must be captured.

### Likely Failure Modes

The top expected failure categories.

### Improvement Priorities

What to change first and why.

## Review Checklist

When reviewing an agent evaluation plan, check:

- Is "success" defined concretely?
- Are metrics matched to the task type?
- Is the eval set representative of real usage?
- Are traces captured, not just final outputs?
- Are failures classified by layer?
- Are improvements targeted to the diagnosed layer?

## Anti-Patterns

Avoid:

- reducing agent quality to one number without context
- evaluating only happy-path tasks
- relying only on human vibes without acceptance criteria
- changing the prompt before diagnosing the failure layer
- measuring final answer only and ignoring process traces

