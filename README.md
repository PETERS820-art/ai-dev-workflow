# AI Dev Workflow

A human-controlled Cursor plugin for optional product planning followed by Architect → Builder development, with independent review and repository exploration.

## Workflow

Unclear need / prioritization / human actions
→ Planner
→ Copy approved Feature Brief into a separate Architect conversation
→ Architect
→ Human Gate
→ Builder
→ Reviewer

Clear feature or bug
→ Architect
→ Human Gate
→ Builder
→ Reviewer

Repo Explorer is used by Architect for broad repository investigation when needed.

## Main Agents

### Planner
Acts as an optional product-planning partner. It discusses incomplete ideas, triages and prioritizes work, advises on human-operated actions such as domains or hosting, reads existing Linear issues only when access is guaranteed read-only, and produces a copy-ready Feature Brief. It never reads code or writes to Linear.

### Architect
Accepts either a clear user requirement or a copied, approved Feature Brief. It grounds the requirement in the current repository and Linear state, then produces executable issues and acceptance criteria.

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
Optional long-lived product and delivery planning session. Keep it separate from Architect.

### Architect
Feature-scoped architecture session. Paste an approved Planner handoff when Planner was used.

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

Planner is not required when the user requirement is already clear.

Planner and Architect use separate conversations. Planner outputs a complete handoff block; after approving it, the user manually copies it into a new Architect conversation. The workflow does not default to shared chat context or switching Skills inside one conversation.

Architect stops after Linear/architecture planning and waits for approval.

Builder must invoke a fresh Reviewer after implementation and self-test.

## Freshness and Change Surface

Architect records a full `planned_against` commit SHA plus expected touchpoints, allowed supporting changes and `Do Not Touch` in every Builder-facing issue. Before editing, Builder classifies repository drift as `FRESH`, `SAFE_DRIFT`, `STALE` or `BLOCKED`; only the first two may proceed. Reviewer independently verifies this evidence and the final diff boundary.

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

Use `prepare-architect-handoff` at the end of an approved Planner discussion to produce the final copy-ready block.

## Portability

This plugin contains no project-specific Linear workspace/team/project IDs, no repository memory, and no machine-specific configuration.

When a Linear project is already clear in the conversation, continue using it.

When multiple projects are possible or none is established, ask the user which Linear project to use for that session only.
