---
name: app-plan
description: Turn a Zoom integration idea into an implementation plan with architecture, auth, and delivery milestones. Use when you need a practical build plan, phased delivery sequence, risk list, and next-step recommendation.
argument-hint: "<what you want to build>"
---

# /app-plan

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../../CONNECTORS.md).

Create a practical build plan for a Zoom integration or app.

## Usage

```text
/app-plan $ARGUMENTS
```

## Workflow

1. Capture the target user flow and success criteria.
2. Choose the correct Zoom surface and supporting services.
3. Define auth requirements, scopes, and account assumptions.
4. Break implementation into phases: prototype, core integration, reliability, and launch.
5. Call out hard risks early: OAuth setup, webhook verification, SDK environment limits, marketplace review, or MCP client constraints.
6. End with the smallest deliverable that proves the architecture.

## Output

- Architecture summary
- Zoom products and APIs required
- Auth and scope checklist
- Delivery phases
- Risks, open questions, and immediate next action

## Related Skills

- [start](../start/SKILL.md)
- [implement-oauth](../implement-oauth/SKILL.md)
- [build-meeting-integration](../build-meeting-integration/SKILL.md)
- [build-meeting-bot](../build-meeting-bot/SKILL.md)
