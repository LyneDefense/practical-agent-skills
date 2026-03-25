# practical-agent-skills

Personal skill library for designing, evaluating, and iterating on AI agents.

This repo is a curated set of reusable skills rather than a single framework. Each skill is a small, self-contained knowledge module with a clear trigger boundary and a practical workflow.

## Current Focus

This repo currently focuses on **single-agent design and evaluation**, especially:

- harness design
- tool and state selection
- skill-loading strategy
- context management
- evaluation and failure analysis

## Skills

### Architecture

- `agent-harness-designer`
  Design or review a single-agent harness using the `s01-s07` mental model from Learn Claude Code.
  Best for deciding between:
  - loop
  - tool schema
  - `todo`
  - `task`
  - `subagent`
  - `skill`
  - `compact`

### Evaluation

- `agent-evaluation`
  Evaluate an agent systematically across success, correctness, process quality, efficiency, and robustness.
  Best for:
  - defining eval dimensions
  - building a task set
  - writing acceptance criteria
  - classifying failures by layer
  - choosing targeted improvements

## Repo Structure

```text
skills/
  agent-harness-designer/
    SKILL.md
  agent-evaluation/
    SKILL.md
templates/
  skill-template/
    SKILL.md
```

## Naming Convention

Use these rules for new skills:

- use lowercase letters, digits, and hyphens only
- keep names short and action- or domain-oriented
- prefer names that describe the reusable capability, not a temporary project
- avoid vague names like `general-helper` or `notes-skill`

Good examples:

- `agent-evaluation`
- `agent-harness-designer`
- `pdf-contract-review`
- `repo-architecture-analysis`

Bad examples:

- `misc`
- `agent-stuff`
- `my-notes`
- `new-skill-v2-final`

## Skill Template

Start new skills from:

- `templates/skill-template/SKILL.md`

The template is intentionally small. A good first version of a skill should usually contain:

- a precise trigger description in frontmatter
- a clear task boundary
- a reusable workflow
- a compact output structure

Add `references/`, `scripts/`, or `assets/` only when the skill clearly needs them.

## Design Principles

- Keep each skill self-contained.
- Prefer concise `SKILL.md` bodies with clear trigger descriptions.
- Put only reusable workflow and judgment guidance into the skill body.
- Add `references/`, `scripts/`, or `assets/` only when they materially improve reuse.
- Avoid turning raw notes into skills without first identifying their trigger boundary and decision value.

## How To Grow This Repo

Good candidates for new skills are:

- repeated decision frameworks
- repeated review workflows
- repeated domain procedures
- repeated evaluation methods

Poor candidates are:

- one-off notes
- large undifferentiated documentation dumps
- content without a clear usage trigger

## Adding a New Skill

Recommended workflow:

1. Copy `templates/skill-template/` to `skills/<new-skill-name>/`
2. Replace the placeholder `name` and `description`
3. Tighten the "When To Use" boundary
4. Keep only reusable workflow and decision rules
5. Move bulky detail into `references/` if the body starts to bloat
6. Update this README with the new skill and its category
