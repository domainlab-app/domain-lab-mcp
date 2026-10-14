# Domain Lab MCP server

<!-- mcp-name: app.domainlab/domain-lab -->

Connect Claude, ChatGPT, Copilot and other AI assistants to [Domain Lab](https://www.domainlab.app),
so you can ask about your domains in plain English instead of digging through registrar dashboards.

Domain Lab watches domains across every registrar and tells you what changed: expiration dates,
DNS records, security certificates, and email security (SPF, DKIM, DMARC).

**Server URL:** `https://mcp.domainlab.app/mcp`

This is a hosted (remote) server. There is nothing to install. You sign in to your Domain Lab
account and approve the connection; no API keys to copy.

## What you can ask

- "What expires this month?"
- "Did anything change on our client's site this week?"
- "Were we actually alerted when the certificate changed?"
- "Is our SPF and DMARC set up right?"
- "Has my DNS change spread yet?"
- "Is anyone registering lookalikes of our domain?"
- "When could this expiring domain become available?"

## Connect

**Claude** (Claude.ai, Desktop, mobile): Settings → Connectors → Add custom connector →
`https://mcp.domainlab.app/mcp`, then sign in and approve.

**ChatGPT**: Settings → Connectors → Advanced → Developer mode on → Create →
`https://mcp.domainlab.app/mcp`, Authentication: OAuth.

**Claude Code**

```bash
claude mcp add --transport http domainlab https://mcp.domainlab.app/mcp
```

**VS Code (GitHub Copilot)**: `.vscode/mcp.json`

```json
{
  "servers": {
    "domainlab": { "type": "http", "url": "https://mcp.domainlab.app/mcp" }
  }
}
```

**Cursor**: `~/.cursor/mcp.json`

```json
{
  "mcpServers": {
    "domainlab": { "url": "https://mcp.domainlab.app/mcp" }
  }
}
```

**Gemini CLI**

```bash
gemini mcp add --transport http domainlab https://mcp.domainlab.app/mcp
```

Full setup guide, including Windsurf: https://www.domainlab.app/help/articles/mcp-server

## Tools

**Your account**
`get_overview`, `get_digest`, `list_domains`, `get_domain`, `get_domain_history`, `list_events`,
`explain_change`, `list_alerts`, `get_ai_reviews`, `get_account`, `list_event_types`,
`get_notification_rules`, `list_registrar_connections`, `check_inbox`

**Changes** (ask first; can be turned off by connecting read-only)
`add_domain`, `update_domain`, `remove_domain`, `rescan_domain`, `request_ai_review`,
`set_domain_alerts`, `sync_registrar`, `mark_inbox_read`

**Any domain, monitored or not** (public information only)
`check_domain_status`, `email_auth_check`, `dns_lookup`, `dns_propagation_check`, `ssl_check`,
`find_lookalike_domains`, `estimate_release_date`

Read tools are marked read-only. `remove_domain` is marked destructive and asks for confirmation.

## Security and privacy

- Sign-in is OAuth 2.1 with PKCE. You approve each connection on domainlab.app and can
  disconnect it any time from Preferences → API → Connected AI assistants.
- A connection sees only your own account, with the same limits as your plan.
- The server reads only what each tool is asked for. It does not see your chat history.
- Privacy policy: https://www.domainlab.app/privacy

## Support

support@domainlab.app
