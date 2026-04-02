# Connectors

This plugin works in two modes:

- Standalone: Claude uses the bundled Zoom skills and reference material included with this plugin.
- Supercharged: Claude can also use the bundled Zoom MCP servers from [`.mcp.json`](./.mcp.json) for live tool access.

## Included MCP Servers

| Connector | Endpoint | Use For |
|---|---|---|
| `zoom-mcp` | `https://mcp-us.zoom.us/mcp/zoom/streamable` | Zoom-hosted MCP workflows for meetings, recordings, summaries, and Zoom Docs |
| `zoom-whiteboard-mcp` | `https://mcp-us.zoom.us/mcp/whiteboard/streamable` | Whiteboard-specific MCP workflows |

## Authentication

The bundled MCP definitions expect bearer tokens in these environment variables:

```bash
export ZOOM_MCP_ACCESS_TOKEN="your_zoom_user_oauth_access_token"
export ZOOM_WHITEBOARD_MCP_ACCESS_TOKEN="your_zoom_user_oauth_access_token"
```

- `ZOOM_MCP_ACCESS_TOKEN` is used for the main Zoom MCP server.
- `ZOOM_WHITEBOARD_MCP_ACCESS_TOKEN` is used for the Whiteboard MCP server.
- If one user OAuth token includes both scope sets, both variables can use the same value.
- After setting or rotating either token, restart Claude Code or re-enable the plugin so the MCP servers restart with the new environment.

## What You Can Do Without Connectors

- Choose the right Zoom surface for a new integration
- Plan SDK, REST API, webhook, OAuth, and MCP implementations
- Compare Meeting SDK vs Video SDK vs Zoom Apps vs REST API
- Debug architecture, auth, event-delivery, and integration mistakes
- Use the deep Zoom reference library bundled in `skills/`

## What Connectors Add

- Live MCP tool discovery and execution against Zoom-hosted MCP servers
- Real meeting-search, recording-resource, and document workflows
- Whiteboard-specific tool access when applicable

## Notes

- If a command or skill mentions connectors and you are not connected, continue in standalone mode using the reference docs.
- If you are unsure which connector is relevant, start with the `design-mcp-workflow` skill or the [`mcp-setup`](./skills/mcp-setup/SKILL.md) skill.
