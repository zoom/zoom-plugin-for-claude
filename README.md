# Zoom Plugin for Claude

A Claude plugin for planning, building, and debugging Zoom integrations. It helps choose the right Zoom surface, shape implementations, debug failures, and route into the right Zoom references without making the user read the whole doc tree first.

## Installation

Install this directory as a local Claude plugin. The plugin manifest is at [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json) and the bundled Zoom MCP connectors are defined in [`.mcp.json`](.mcp.json).

Before using the bundled MCP servers, export bearer tokens for the Zoom surfaces you want Claude to use:

```bash
export ZOOM_MCP_ACCESS_TOKEN="your_zoom_user_oauth_access_token"
```

## Slash Workflows

Explicit slash workflows implemented as skills under `skills/`:

| Workflow | Description |
|---|---|
| [`/choose-stack`](skills/choose-stack/SKILL.md) | Pick the right Zoom surface for a use case and explain the tradeoffs |
| [`/app-plan`](skills/app-plan/SKILL.md) | Turn an idea into a Zoom architecture and delivery plan |
| [`/debug-integration`](skills/debug-integration/SKILL.md) | Triage a broken Zoom integration and isolate the failing layer |
| [`/mcp-setup`](skills/mcp-setup/SKILL.md) | Decide when Zoom MCP fits and plan a safe Claude workflow |

## Skills

Workflow-oriented skills Claude should pull in automatically when relevant:

| Skill | Description |
|---|---|
| [`start`](skills/start/SKILL.md) | Default router for new Zoom work |
| [`choose-zoom-approach`](skills/choose-zoom-approach/SKILL.md) | Decide between REST API, SDKs, webhooks, apps, or MCP |
| [`implement-oauth`](skills/implement-oauth/SKILL.md) | Choose the auth model and implement it correctly |
| [`build-meeting-integration`](skills/build-meeting-integration/SKILL.md) | Build an embedded or managed Zoom meeting flow |
| [`build-meeting-bot`](skills/build-meeting-bot/SKILL.md) | Build bots, recorders, and real-time meeting processors |
| [`design-mcp-workflow`](skills/design-mcp-workflow/SKILL.md) | Plan Zoom MCP workflows for Claude |
| [`debug-zoom-integration`](skills/debug-zoom-integration/SKILL.md) | Debug auth, API, SDK, webhook, RTMS, or MCP failures |

## Deep References

The plugin also keeps the original Zoom product-specific reference library under `skills/`. These are supporting references, not the primary entry surface:

- [`skills/general/`](skills/general/)
- [`skills/rest-api/`](skills/rest-api/)
- [`skills/meeting-sdk/`](skills/meeting-sdk/)
- [`skills/video-sdk/`](skills/video-sdk/)
- [`skills/webhooks/`](skills/webhooks/)
- [`skills/websockets/`](skills/websockets/)
- [`skills/oauth/`](skills/oauth/)
- [`skills/zoom-mcp/`](skills/zoom-mcp/)

## Example Workflows

### Choosing the right Zoom stack

```text
/choose-stack Build an internal meeting assistant that joins calls, extracts action items, and stores summaries
```

### Planning a new app

```text
/app-plan Build a React app that lets customers schedule and join Zoom meetings from our product
```

### Debugging a broken webhook

```text
/debug-integration My Zoom webhook signature verification fails in production but not locally
```

### Designing an MCP flow

```text
/mcp-setup I want Claude to search meetings, pull recording resources, and create follow-up docs
```

## Connectors

See [CONNECTORS.md](CONNECTORS.md). The plugin works standalone from the bundled skills, and gets supercharged when Claude can use the bundled Zoom MCP server from [`.mcp.json`](.mcp.json).

## Cross-Platform Notes

This repo is packaged first as a Claude plugin, but it also includes [AGENTS.md](AGENTS.md) for agent ecosystems that use a repo-level discovery file. The reusable core remains the `skills/` tree and its `SKILL.md` files.

## Structure

```text
Zoom Plugin for Claude/
├── .claude-plugin/plugin.json
├── .mcp.json
├── CONNECTORS.md
├── skills/
│   ├── choose-stack/
│   ├── app-plan/
│   ├── debug-integration/
│   ├── mcp-setup/
│   ├── start/
│   ├── choose-zoom-approach/
│   ├── implement-oauth/
│   ├── build-meeting-integration/
│   ├── build-meeting-bot/
│   ├── design-mcp-workflow/
│   ├── debug-zoom-integration/
│   └── ... existing Zoom reference skills
└── README.md
```

## License

MIT
