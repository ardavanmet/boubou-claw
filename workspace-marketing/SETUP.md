# Marketing Agent Setup - Marki 📈

## What's Been Created

✅ **Workspace:** `/home/ardi/.openclaw/workspace-marketing/`
✅ **Agent ID:** `marketing`
✅ **Name:** Marki
✅ **Identity:** Growth strategist, data-driven, conversion-obsessed
✅ **ROLE.md:** Purpose, scope, output style, guardrails
✅ **IDENTITY.md:** Name, vibe, emoji

## Configuration Needed

### Add Tool Restrictions to openclaw.json

Find the marketing agent entry in `openclaw.json` (around line 44) and add the `tools` configuration:

```json
{
  "id": "marketing",
  "name": "marketing",
  "workspace": "/home/ardi/.openclaw/workspace-marketing",
  "agentDir": "/home/ardi/.openclaw/agents/marketing/agent",
  "model": "openai/gpt-5.1-codex",
  "tools": {
    "profile": "minimal",
    "allow": [
      "web_search",
      "web_fetch",
      "read",
      "write",
      "edit"
    ],
    "deny": [
      "exec",
      "bash",
      "apply_patch",
      "browser",
      "sessions_list",
      "sessions_send",
      "sessions_spawn"
    ]
  }
}
```

**Why these restrictions:**
- ✅ `web_search`, `web_fetch` - For research, competitor analysis, SEO
- ✅ `read`, `write`, `edit` - For drafting copy and content
- ❌ `exec`, `bash` - No command execution (security)
- ❌ `apply_patch` - No code changes (guardrail: no product architecture changes)
- ❌ `browser` - Not needed yet (can add later for Google Ads UI)
- ❌ `sessions_*` - Marketing agent doesn't orchestrate other agents

## How to Use Marki

### From Main Agent (Boubou)

Use the `sessions_spawn` tool to delegate marketing tasks:

```json
{
  "tool": "sessions_spawn",
  "task": "Create 3 landing page headline variants focused on speed and trust. Include hypothesis, test design, and expected lift for each.",
  "label": "Marketing",
  "agentId": "marketing",
  "runTimeoutSeconds": 300,
  "cleanup": true
}
```

### What Marki Returns

Every response includes:
1. **Hypothesis** - What we're testing and why
2. **Test Design** - How to validate
3. **Copy Draft** - Actual content/variants
4. **KPI Targets** - Baseline → target metrics
5. **Expected Lift** - Predicted impact

### Main Agent's Job After Delegation

1. Apply leverage tier framework (Tier 1-4)
2. Apply investor-lens filter (5 questions)
3. Synthesize with strategic context
4. Present to Ardav with implications

## Future Integrations

### Google Ads API
When ready to integrate:
- Create custom skill in `workspace-marketing/skills/google-ads/`
- Add API credentials to environment
- Update ROLE.md with new capabilities

### Google Analytics
When ready to integrate:
- Create custom skill in `workspace-marketing/skills/google-analytics/`
- Add API credentials to environment
- Enable funnel analysis and conversion tracking

## Testing the Setup

After updating `openclaw.json`:

1. **Restart gateway:**
   ```bash
   openclaw gateway restart
   ```

2. **Verify agents:**
   ```bash
   openclaw agents list
   ```

3. **Test delegation from main agent:**
   Ask Boubou (main agent): "Delegate to Marki: Analyze our current landing page messaging and suggest 2 improvements for conversion rate."

4. **Check result:**
   Marki should return structured output with hypothesis, test design, copy, KPIs, and expected lift.

## File Structure

```
workspace-marketing/
├── IDENTITY.md          # Marki's identity (name, vibe, emoji)
├── ROLE.md              # Purpose, scope, output style, guardrails
├── AGENTS.md            # Operating instructions (auto-generated)
├── SOUL.md              # Personality (auto-generated)
├── USER.md              # User info (auto-generated)
├── TOOLS.md             # Tool conventions (auto-generated)
├── BOOTSTRAP.md         # First-run instructions (auto-generated)
└── SETUP.md             # This file
```

## Next Steps

1. ✅ Created workspace and files
2. ✅ Updated main agent AGENTS.md with delegation guidelines
3. ⏳ **YOU DO:** Add tool restrictions to `openclaw.json`
4. ⏳ **YOU DO:** Restart gateway (`openclaw gateway restart`)
5. ⏳ **TEST:** Delegate a task from main agent to Marki
6. 🔮 **FUTURE:** Add Google Ads/Analytics skills when ready

---

**Marki is ready to drive growth! 📈**
