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

## Install

Repository: https://github.com/PETERS820-art/ai-dev-workflow

This repository is **public**. Cursor installs plugins by cloning with local git; a private repo will silently fail on machines that are not logged into GitHub.

### Option A — Install from GitHub in Cursor

1. Open **Customize → Plugins** (or Marketplace)
2. Choose install / import from GitHub repository
3. Paste: `https://github.com/PETERS820-art/ai-dev-workflow`
4. Install **AI Dev Workflow** / `ai-dev-workflow`
5. Reload the window if components do not appear

If Cursor jumps back to the public Marketplace without installing, use Option B.

### Option B — Local install (most reliable)

Copy the repository contents to:

```text
~/.cursor/plugins/local/ai-dev-workflow/
```

Required layout:

```text
~/.cursor/plugins/local/ai-dev-workflow/
├── .cursor-plugin/plugin.json
├── skills/
├── agents/
├── rules/
└── commands/
```

Then restart Cursor or run **Developer: Reload Window**.

### Option C — Team Marketplace (Teams / Enterprise)

1. Dashboard → Plugins → Team Marketplaces → Import from Repo
2. Import `https://github.com/PETERS820-art/ai-dev-workflow`
3. Install the plugin from your team marketplace in Customize

## Setup

After install, run the `setup-workflow` command.

It only verifies components, checks Linear MCP availability when needed, and explains the modes.

It does not create project identity files or start development.

## Portability

This plugin contains no project-specific Linear workspace/team/project IDs, no repository memory, and no machine-specific configuration.

When a Linear project is already clear in the conversation, continue using it.

When multiple projects are possible or none is established, ask the user which Linear project to use for that session only.
