# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A methodology framework ("Vibe Coding") defining executable, verifiable AI behavior rules and a structured workflow for AI-assisted development. This is not a software application — it contains no buildable code, tests, or deployable artifacts. All content is Markdown and JSON.

## Architecture

**Two-layer system: Rules (global constraints) + Skills (stage-specific actions)**

### Rules (`rules/`)
- `agent.md` — Global AI collaboration rules (always apply). Six categories: Decision, Communication, Information, Risk, Time & Effort, Growth & Evolution. Each has Constraints (hard), Preferences (default), Heuristics (uncertain).
- `coding.md` — Code design rules structured as 7 "change axes" (A1–A7) in JSON format. Each axis has trigger→action→verify rules for detecting and resolving design problems.
- `project.md` — Template for project-specific context (currently a placeholder).
- `document.md` — Placeholder for document rules.
- `quality.md` — Placeholder for quality rules.

**Scenario routing**: `agent.md` §7 defines which rule file loads based on user intent. Only relevant rules load; global Constraints are never overridden.

### Skills (`skills/`)
Five skills form a pipeline matching the workflow stages:

```
intent-compression → structure-cutting → execution-momentum → goal-verification → lightweight-reflection
     (intent)           (design)          (implementation)      (verification)        (reflection)
```

Each skill has: inputs, outputs, stop conditions, self-evaluation criteria. The `review` skill is standalone (code review reporting).

### Workflow (`workflow.md`)
Five-phase closed loop: Intent → Design → Execution → Validate → Reflect → (next task). Phases are sequential — no skipping. Each phase has defined inputs, outputs, and exit criteria.

## Key Conventions

- **Default language is Chinese** (per CR-C01 in `agent.md`). English is used only if explicitly requested.
- **Skill template** at `skills/skill.template.md` — new skills must follow this frontmatter format (name, description, stage, inputs, outputs, stop_conditions).
- Rules use a **Constraint > Preference > Heuristic** priority hierarchy. Constraints are never violated.
- The coding rules in `coding.md` are JSON-structured, not Markdown — maintain this format when editing.
