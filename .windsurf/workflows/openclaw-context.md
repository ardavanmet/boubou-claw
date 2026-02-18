---
description: OpenClaw platform context and architecture reference
---

# OpenClaw Platform Context

OpenClaw is a personal AI assistant platform that runs locally on your devices and connects to messaging channels you already use—WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, and more. It operates as a Gateway-based control plane that manages sessions, channels, tools, and events, providing a unified interface for AI-powered conversations across multiple platforms.

## Architecture

The architecture centers around a WebSocket-based Gateway that serves as the single control plane for all client interactions. OpenClaw embeds an agent runtime derived from pi-mono, with OpenClaw-owned session management, tool wiring, and workspace bootstrap. It supports multi-agent routing for isolated workspaces, sandboxed execution for security, and a skills system for teaching the agent how to use tools.

## Key Configuration Files

- **Main config**: `~/.openclaw/openclaw.json` (JSON5 format)
- **Workspace**: `~/.openclaw/workspace/` (AGENTS.md, SOUL.md, TOOLS.md, etc.)
- **Cron jobs**: `~/.openclaw/cron/jobs.json`
- **Skills**: `~/.openclaw/workspace/skills/`

## Core Components

### Gateway
- WebSocket-based control plane on port 18789 (default)
- Token-based authentication
- OpenAI-compatible HTTP API at `/v1/chat/completions`
- Webhook endpoints at `/hooks/*`

### Channels
Supported messaging platforms:
- WhatsApp, Telegram, Discord, Slack
- Google Chat, Signal, iMessage, Microsoft Teams
- Each with configurable `dmPolicy` (pairing | allowlist | open | disabled)

### Agent System
- Multi-agent routing with isolated workspaces
- Model configuration with primary + fallbacks
- Tool profiles: minimal | coding | messaging | full
- Sandboxed execution via Docker containers

### Tools
First-class agent tools:
- **group:runtime**: exec, bash, process
- **group:fs**: read, write, edit, apply_patch
- **group:sessions**: sessions_list, sessions_history, sessions_send, sessions_spawn
- **group:web**: web_search, web_fetch
- **group:ui**: browser, canvas
- **group:automation**: cron, gateway
- **group:messaging**: message
- **group:nodes**: nodes (device pairing)

### Skills System
- ClawHub for skill installation
- Workspace-specific skills in `workspace/skills/`
- SKILL.md format with metadata and instructions

## Common CLI Commands

```bash
# Gateway management
openclaw gateway status
openclaw gateway start/stop/restart
openclaw logs --follow

# Configuration
openclaw configure
openclaw config get <path>
openclaw config set <path> <value>

# Channels
openclaw channels login --channel whatsapp
openclaw channels status
openclaw pairing list/approve

# Cron jobs
openclaw cron add --name "Job" --cron "0 7 * * *" --message "Task"
openclaw cron list
openclaw cron run <job-id>

# System events
openclaw system event --mode now --text "Message"

# Health
openclaw doctor
openclaw health
```

## Integration Patterns

1. **Gateway setup** with desired channels and authentication
2. **Workspace configuration** with custom prompts and skills
3. **OpenAI-compatible API** for programmatic access
4. **Webhooks** for event-driven automation
5. **Cron jobs** for scheduled/proactive behavior

## Environment Variables

Key environment variables:
- `OPENCLAW_HOME` - Home directory
- `OPENCLAW_STATE_DIR` - State directory (default: `~/.openclaw`)
- `OPENCLAW_CONFIG_PATH` - Config file path
- `OPENCLAW_GATEWAY_TOKEN` - Gateway auth token
- Channel tokens: `TELEGRAM_BOT_TOKEN`, `DISCORD_BOT_TOKEN`, `SLACK_BOT_TOKEN`, etc.
- API keys: `BRAVE_API_KEY`, `GEMINI_API_KEY`

## Use Cases

- Personal productivity assistance via messaging channels
- Automated workflows through cron jobs and webhooks
- Browser automation for web tasks
- Multi-device coordination via connected nodes
- Persistent conversation context across platforms
- Tool-augmented AI interactions
