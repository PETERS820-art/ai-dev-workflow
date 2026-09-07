---
name: prepare-architect-handoff
description: Finalize an approved Planner brief as a self-contained block for manual copy into a separate Architect conversation.
---

# Prepare Architect Handoff

Use only in Planner. Do not inspect the repository, write Linear, invoke Architect or continue into engineering.

Before finalizing, confirm the project, feature, outcome, user flow, scope, constraints, recommendation, human blockers and technical unknowns are captured; open product decisions are `None`; and the user explicitly approved the content.

Without explicit approval, output `Status: DRAFT` and ask for approval or revision. Never infer approval.

After approval, output one complete block:

```markdown
BEGIN ARCHITECT HANDOFF

Role: PLANNER
Brief ID: <stable identifier>
Revision: <number>
Status: USER_APPROVED
Project: <user-confirmed project>
Feature: <short name>

## Problem
...

## Desired Outcome
...

## User Flow
...

## Priority
<Critical | High | Normal | Low, with reason>

## Delivery Recommendation
<Build Now | Thin Slice | Enabler First | Spike | Human Action First | Backlog | Drop>

## In Scope
- ...

## Out of Scope
- ...

## Product Constraints
- ...

## Success Conditions
- <observable product or operational outcome>

## Existing Linear Context
- <read-only issue references, or None>

## Human / External Actions
- <user action, expected result and blocking status, or None>

## Architect Must Verify
- <implementation, feasibility, dependency or effort question, or None>

## Open Product Decisions
- None

END ARCHITECT HANDOFF
```

Keep it product-focused and independent of earlier chat. Do not include files, APIs, schemas, implementation instructions or engineering Acceptance Criteria.

After the block, output exactly:

`Copy the complete block above into a new Architect conversation. Do not switch Skills in this Planner conversation.`
