# AI Dev Workflow

A human-controlled Cursor plugin for Planner → Architect → Builder development, with independent review and repository exploration.

## Workflow

Planner
→ Architect
→ Human Gate
→ Builder
→ Reviewer

Repo Explorer is used by Architect for broad repository investigation when needed.

## Main Agents

### Planner
Translates real user needs into product scope, delivery strategy, priorities, and Feature Briefs.

### Architect
Grounds an approved Feature Brief in the current repository and Linear state, then produces executable issues and acceptance criteria.

### Builder
Implements one approved Linear issue, self-tests, then requires an independent Reviewer PASS before completion.

## Subagents

### Reviewer
Independent, preferably read-only acceptance verification against the Linear issue, acceptance criteria, git diff, relevant code, and test evidence.

Returns: `PASS` / `FAIL` / `BLOCKED`

### Repo Explorer
Read-only repository investigation for Architect. Returns concise evidence only. Does not implement code, create Linear issues, or make final architecture decisions.

## Recommended Usage

### Planner
Long-lived project/product planning session.

### Architect
Feature-scoped architecture session.

### Builder
Fresh issue-scoped implementation session.

### Reviewer
Fresh review context for every review round.

### Repo Explorer
Temporary repository exploration context.

## Human Gates

This workflow intentionally requires user control between:

- Planner → Architect
- Architect → Builder

No automatic end-to-end execution should occur.

Architect stops after Linear/architecture planning and waits for approval.

Builder must invoke a fresh Reviewer after implementation and self-test.

## Setup

Run the `setup-workflow` command after installing the plugin.

It only verifies components, checks Linear MCP availability when needed, and explains the modes.

It does not create project identity files or start development.

## Portability

This plugin contains no project-specific Linear workspace/team/project IDs, no repository memory, and no machine-specific configuration.

When a Linear project is already clear in the conversation, continue using it.

When multiple projects are possible or none is established, ask the user which Linear project to use for that session only.
