---
name: replace-with-skill-name
description: |
  Replace with a clear trigger description.
  Use when users ask for:
  (1) ...
  (2) ...
  (3) ...
  Keywords: keyword-a, keyword-b, keyword-c
---

# Replace With Skill Title

Use this skill when the task has a clear trigger boundary and a reusable workflow.

## Purpose

State what this skill helps the agent accomplish.

## When To Use

Use this skill when:

- the user asks for ...
- the task involves ...
- the agent needs a repeatable method for ...

Do not use this skill when:

- ...
- ...

## Core Workflow

1. Identify the task type.
2. Gather the minimum required context.
3. Apply the domain workflow.
4. Produce the expected output structure.
5. Validate the result if validation is part of the task.

## Decision Rules

Include only the judgment rules that are not already obvious to a strong model.

Examples:

- Prefer X over Y when ...
- Ask for Z only if ...
- Do not do A when B is true.

## Output Format

When using this skill, structure the answer as:

### Goal

What is being solved.

### Approach

What workflow or method is being used.

### Result

The actual output or recommendation.

### Risks or Gaps

Anything uncertain, missing, or requiring follow-up.

## Review Checklist

Use a short checklist only if it materially improves consistency.

- Did the answer stay inside the skill boundary?
- Did it apply the intended workflow?
- Did it avoid unnecessary verbosity?

## Anti-Patterns

Avoid:

- turning this skill into a generic knowledge dump
- copying long notes into the body without a workflow
- adding framework-specific details that belong in `references/`
- mixing multiple unrelated task types into one skill

## Extensions

If this skill grows, split into:

- `references/` for detailed docs or examples
- `scripts/` for deterministic repeated operations
- `assets/` for reusable output resources

