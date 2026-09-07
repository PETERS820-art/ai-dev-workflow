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

Command:
- `prepare-architect-handoff`

If any component is missing, tell the user the plugin is incomplete and stop.

## 2. Verify Linear MCP when needed

If the user intends to use Linear-backed planning or architecture:

- check whether Linear MCP tools are available;
- if unavailable, tell the user to connect Linear MCP before Architect Linear work or before Planner needs read-only issue context;
- do not ask for or store Linear workspace, team, or project identity;
- do not create `project-context.json` or any equivalent project-identity file.

Planner may use only Linear issue-read operations. It must not create or modify any Linear object. If the environment cannot restrict Planner to read-only Linear tools, keep Linear disabled in Planner and ask the user to paste relevant issue summaries.

Builder can still work from a specific Linear issue URL/ID once Linear access is available.

## 3. Main workflow modes

Explain these three user-controlled modes:

### Planner
Optional human discussion, task triage, prioritization and external-action guidance → Feature Brief.

Use for long-lived product/project planning or when the user is unsure what to do next.

Planner never reads the repository and never writes to Linear.

Do not auto-invoke Architect or Builder.

### Architect
Clear user requirement or copied approved Feature Brief + current repository + current Linear state → architecture plan → executable Linear issues.

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

1. Planner — attach/use the `planner` skill in its own conversation
2. Architect — attach/use the `architect` skill
3. Builder — attach/use the `builder` skill

Keep each Builder session issue-scoped and prefer a fresh Reviewer context for every review round.

Configure Planner with no repository search/read, edit or terminal tools. Enable only web research and read-only Linear issue tools. If individual Linear write tools cannot be disabled, disable Linear for Planner entirely.

Planner and Architect must use separate conversations. When a brief is approved, run `prepare-architect-handoff`, copy the complete handoff block, open a new Architect conversation, and paste it there. Do not switch Skills in the Planner conversation and do not default to attaching the old chat as context.

## 6. Stop conditions

Do not:

- create project-specific config files;
- create Linear projects automatically;
- modify repository architecture;
- transfer Planner context implicitly;
- start development;
- chain Planner → Architect → Builder automatically.

End with a short confirmation that the workflow is ready for manual use.
