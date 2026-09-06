---
name: setup-workflow
description: Verify AI Dev Workflow plugin components and explain how to use Planner, Architect, and Builder modes.
---

# Setup AI Dev Workflow

Lightweight setup only. Do not start planning, architecture, or implementation.

## 1. Verify plugin components

Confirm these components are available in this environment:

Skills:
- `planner`
- `architect`
- `builder`

Subagents:
- `reviewer`
- `repo-explorer`

Rule:
- shared workflow rule

If any component is missing, tell the user the plugin is incomplete and stop.

## 2. Verify Linear MCP when needed

If the user intends to use Linear-backed planning or architecture:

- check whether Linear MCP tools are available;
- if unavailable, tell the user to connect Linear MCP before Planner/Architect Linear work;
- do not ask for or store Linear workspace, team, or project identity;
- do not create `project-context.json` or any equivalent project-identity file.

Builder can still work from a specific Linear issue URL/ID once Linear access is available.

## 3. Main workflow modes

Explain these three user-controlled modes:

### Planner
Real user need → product/delivery strategy → Feature Brief.

Use for long-lived product/project planning.

Do not auto-invoke Architect or Builder.

### Architect
Feature Brief + current repository + current Linear state → architecture plan → executable Linear issues.

May use `repo-explorer` for broad repository investigation.

Stop after planning and wait for user approval.

Do not auto-invoke Builder.

### Builder
Approved Linear issue → implementation → self-test → mandatory fresh `reviewer` subagent.

Review loop: FAIL → fix → new fresh Reviewer; PASS → complete; BLOCKED → surface to user.

## 4. Subagents

Explain briefly:

- `reviewer` — independent acceptance verification; invoked by Builder
- `repo-explorer` — read-only repository investigation; used mainly by Architect

Users should not run these as primary workflow modes.

## 5. Custom Modes guidance

If the current Cursor UI requires Custom Modes / Agent sessions for stable role use, guide the user to create or reuse three main sessions:

1. Planner — attach/use the `planner` skill
2. Architect — attach/use the `architect` skill
3. Builder — attach/use the `builder` skill

Keep each Builder session issue-scoped and prefer a fresh Reviewer context for every review round.

## 6. Stop conditions

Do not:

- create project-specific config files;
- create Linear projects automatically;
- modify repository architecture;
- start development;
- chain Planner → Architect → Builder automatically.

End with a short confirmation that the workflow is ready for manual use.
