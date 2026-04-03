# Development-Focused Plugin Plan

## Goal

Make this repository behave like a **Zoom developer workflow plugin** for Claude:

- choose the right Zoom surface quickly
- move from architecture to implementation without wandering
- help Claude scaffold and build real Zoom projects
- keep deep Zoom references available, but secondary

This plan intentionally prioritizes **development workflows** over:

- live Zoom admin operations
- generic account management
- broad operator-style CRUD actions
- expanding the MCP surface as the primary value proposition

## Current Assessment

### What Already Works

- The top-level workflow skills are directionally correct:
  - `skills/start/SKILL.md`
  - `skills/which-zoom-product/SKILL.md`
  - `skills/build-zoom-plan/SKILL.md`
  - `skills/setup-zoom-oauth/SKILL.md`
  - `skills/build-zoom-meeting-app/SKILL.md`
  - `skills/build-zoom-bot/SKILL.md`
  - `skills/debug-zoom-integration/SKILL.md`
- The plugin is already positioned around planning, building, and debugging Zoom integrations.
- The repo has strong Zoom domain coverage across REST, SDKs, webhooks, OAuth, RTMS, and MCP.
- The current plugin structure fits Claude's modern `skills/`-first model.

### Main Problems

1. The plugin is still too reference-heavy.
2. Claude can usually choose the correct Zoom surface, but it is less reliable at pushing directly into concrete implementation work.
3. Many deep `SKILL.md` files are too large to serve as sharp execution guidance.
4. There are not enough narrow, code-oriented implementation skills.
5. The repo lacks starter templates or starter-file patterns for common Zoom app types.

## Evidence

Large `SKILL.md` files indicate that too much detailed reference material still lives in primary skill files instead of being pushed into supporting references:

- `skills/meeting-sdk/windows/SKILL.md` — 1193 lines
- `skills/meeting-sdk/web/SKILL.md` — 1127 lines
- `skills/video-sdk/windows/SKILL.md` — 1019 lines
- `skills/oauth/SKILL.md` — 901 lines
- `skills/cobrowse-sdk/SKILL.md` — 894 lines
- `skills/video-sdk/web/SKILL.md` — 821 lines
- `skills/rest-api/SKILL.md` — 595 lines
- `skills/rtms/SKILL.md` — 580 lines

These files are valuable references, but they are not ideal as front-line execution skills.

## Product Direction

### Desired Plugin Identity

This plugin should feel like:

- a Zoom-specific developer copilot
- a Zoom project scaffolding assistant
- a Zoom integration architecture and debugging workflow plugin
- a Zoom implementation guide that produces files, structure, and next steps

This plugin should not primarily feel like:

- a Zoom admin console
- a live Zoom operator plugin
- a broad CRUD surface for arbitrary account actions

## Design Principles

1. Workflow skills first, reference skills second.
2. Prefer narrow implementation skills over broad catalog skills.
3. Push detail into `references/`, `examples/`, and templates.
4. Every top-level workflow should end in a concrete deliverable.
5. Default to project-building outcomes, not just architectural explanation.

## Plan

## Phase 1: Tighten the Front Door

### Objective

Make the plugin consistently route Claude into build-oriented outcomes.

### Changes

- Refine the top-level workflow skills so they produce concrete deliverables:
  - recommended stack
  - required auth model
  - first files to create
  - implementation sequence
  - known risks
- Make `start`, `which-zoom-product`, and `build-zoom-plan` more explicit about when to stop routing and start building.
- Add stronger "do not use X when Y is needed" language where ambiguity is common:
  - Meeting SDK vs Video SDK
  - REST API vs MCP
  - Webhooks vs WebSockets

### Acceptance Criteria

- Claude gives fewer catalog-style answers.
- Claude more often proposes a concrete first implementation step.
- Top-level responses more often contain file or module recommendations.

## Phase 2: Add Narrow Implementation Skills

### Objective

Convert broad Zoom knowledge into concrete project-building workflows.

### New Skills to Add First

- `build-express-webhook-service`
- `build-nextjs-user-oauth-app`
- `build-server-to-server-meeting-backend`
- `build-recording-download-worker`
- `build-meeting-sdk-web-app`
- `build-team-chat-bot`
- `implement-webhook-verification`
- `implement-oauth-callback`
- `implement-token-refresh`
- `implement-meeting-create-endpoint`

### Shape of Each Skill

Each new implementation skill should:

- focus on one concrete developer job
- define the recommended stack assumptions
- list required Zoom auth/scopes
- specify likely files to create
- provide a step-by-step build order
- link to deeper references only as needed

### Acceptance Criteria

- Claude can respond to "build X" with a concrete implementation path rather than a generic product recommendation.
- Users can ask for a common Zoom project type and get a scaffold-oriented answer.

## Phase 3: Add Starter Templates and File Patterns

### Objective

Reduce ambiguity when Claude begins writing code.

### Changes

- Add starter templates or starter layout references for common Zoom project types:
  - Express webhook service
  - Next.js OAuth app
  - Meeting scheduling backend
  - Meeting SDK web embed app
  - Recording pipeline worker
- Store templates in a clearly separate location such as:
  - `templates/`
  - `examples/starters/`

### Acceptance Criteria

- Claude can point to a starter structure for common Zoom app types.
- Claude can generate file trees with less improvisation.

## Phase 4: Slim Reference Skills

### Objective

Keep the deep references, but stop using them as oversized front-line skills.

### Changes

- Reduce oversized `SKILL.md` files to a concise front section:
  - what the skill is for
  - when to use it
  - key guardrails
  - routing links
- Move detailed material into:
  - `references/`
  - `examples/`
  - `troubleshooting/`
- Prioritize this cleanup for:
  - `skills/meeting-sdk/web/SKILL.md`
  - `skills/meeting-sdk/windows/SKILL.md`
  - `skills/video-sdk/windows/SKILL.md`
  - `skills/oauth/SKILL.md`
  - `skills/rest-api/SKILL.md`

### Acceptance Criteria

- Major skills are faster for Claude to consume.
- Routing becomes clearer.
- Reference depth is preserved without dominating the front-door experience.

## Phase 5: Add Selective Tool Constraints

### Objective

Make workflow behavior more predictable without over-constraining the repo.

### Changes

- Add `allowed-tools` only where it clearly improves skill behavior.
- Start with workflow skills that should stay mostly analytical or file-oriented.
- Avoid blanket restrictions until real usage patterns show where Claude wanders.

### Acceptance Criteria

- Workflow behavior becomes more consistent.
- Tool restrictions do not block legitimate implementation work.

## Explicit Non-Goals for Now

- Do not turn this into a general Zoom admin/operator plugin.
- Do not prioritize live user/account CRUD workflows as the core value.
- Do not add a broad REST execution layer before the development workflow is strong.
- Do not expand MCP as the main product identity.

These may become useful later, but they should not define the next iteration.

## Optional Later Phase

If the development-focused version becomes strong, consider a later operational layer for selected safe developer actions such as:

- validating OAuth credentials
- listing the current user's meetings
- checking webhook subscriptions
- verifying recording access

That should be additive, not the primary identity of the plugin.

## Priority Order

1. Tighten front-door workflow outputs.
2. Add narrow implementation skills.
3. Add starter templates.
4. Slim oversized reference skills.
5. Add selective `allowed-tools`.

## Success Criteria

The plugin should be considered successful when Claude can reliably help a user do all of the following:

- choose the correct Zoom surface for a new idea
- turn that choice into a concrete implementation plan
- begin creating the right files and modules
- implement common Zoom patterns without wandering through the whole reference tree
- debug broken Zoom integrations quickly

## Short Version

The current plugin is already good at **making the right Zoom decision**.

The next job is to make it much better at **turning that decision into working code and project structure**.
