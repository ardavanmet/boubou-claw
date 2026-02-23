# Software Engineering Agent Setup - Cody 🛠️

## What's Been Created

✅ **Workspace:** `/home/ardi/.openclaw/workspace-software/`
✅ **Agent ID:** `software`
✅ **Name:** Cody
✅ **Identity:** Tool builder, TypeScript craftsman
✅ **ROLE.md:** Purpose, scope, technical standards, code patterns
✅ **IDENTITY.md:** Name, vibe, emoji

## Configuration Needed

### Add Tool Restrictions to openclaw.json

Find the software agent entry in `openclaw.json` and add the `tools` configuration:

```json
{
  "id": "software",
  "name": "software",
  "workspace": "/home/ardi/.openclaw/workspace-software",
  "agentDir": "/home/ardi/.openclaw/agents/software/agent",
  "model": "openai/gpt-5.1-codex",
  "tools": {
    "profile": "coding",
    "allow": [
      "read",
      "write",
      "edit",
      "apply_patch",
      "exec",
      "bash",
      "web_search",
      "web_fetch"
    ],
    "deny": [
      "sessions_list",
      "sessions_send",
      "sessions_spawn",
      "browser"
    ]
  }
}
```

**Why these tools:**
- ✅ `read`, `write`, `edit`, `apply_patch` - Code editing and file management
- ✅ `exec`, `bash` - Running TypeScript, npm commands, tests
- ✅ `web_search`, `web_fetch` - API documentation, package research
- ❌ `sessions_*` - Cody doesn't orchestrate other agents
- ❌ `browser` - Not needed for tool building

## How to Use Cody

### From Main Agent (Boubou)

Use the `sessions_spawn` tool to delegate software engineering tasks:

```json
{
  "tool": "sessions_spawn",
  "task": "Build a Google Ads API integration skill for Marki. It should fetch campaign metrics (impressions, clicks, conversions, cost) with proper TypeScript types and error handling.",
  "label": "Software",
  "agentId": "software",
  "runTimeoutSeconds": 600,
  "cleanup": true
}
```

### What Cody Returns

Every deliverable includes:
1. **Technical Specification** - Requirements, constraints, success criteria
2. **Architecture Design** - Component structure, data flow, integration points
3. **Implementation** - Clean TypeScript code with types and error handling
4. **Testing Approach** - Unit tests, integration tests, test data
5. **Documentation** - README, usage examples, troubleshooting

### Main Agent's Job After Delegation

1. Evaluate if tool enables Tier 1-2 work (fundraising or revenue impact)
2. Ensure it serves agent needs (not over-engineered)
3. Verify it's maintainable and well-documented
4. Approve for deployment or request refinements

## Technical Standards

### Code Structure
```
workspace-software/skills/skill-name/
├── README.md           # Purpose, setup, usage
├── package.json        # Dependencies, scripts
├── tsconfig.json       # TypeScript config
├── src/
│   ├── index.ts       # Main entry point
│   ├── types.ts       # Type definitions
│   └── utils.ts       # Helper functions
├── tests/
│   └── index.test.ts  # Test suite
└── SKILL.md           # OpenClaw skill metadata
```

### TypeScript Standards
- Strict mode enabled
- Comprehensive type definitions
- Clear naming conventions (camelCase functions, PascalCase types)
- Proper error handling with typed errors
- JSDoc comments for public APIs

### Code Principles
- Easy to read (clarity over cleverness)
- Modular architecture (single responsibility)
- Professional standards (industry best practices)
- Well-documented (README, inline comments, usage examples)
- Testable (unit tests, integration tests)

## Example: Building a Google Ads Skill

### 1. Cody Creates Skill Structure
```
workspace-software/skills/google-ads/
├── README.md
├── package.json
├── tsconfig.json
├── src/
│   ├── index.ts
│   ├── types.ts
│   ├── client.ts
│   └── utils.ts
├── tests/
│   └── client.test.ts
└── SKILL.md
```

### 2. SKILL.md Metadata
```markdown
---
name: google-ads
description: Fetch and analyze Google Ads campaign performance
metadata: {
  "openclaw": {
    "requires": {
      "env": ["GOOGLE_ADS_CLIENT_ID", "GOOGLE_ADS_CLIENT_SECRET", "GOOGLE_ADS_DEVELOPER_TOKEN"]
    }
  }
}
---

# Google Ads Integration

Fetch campaign performance metrics from Google Ads API.

## Usage

```bash
# In workspace-software/skills/google-ads/
npm install
npm run build

# Set environment variables
export GOOGLE_ADS_CLIENT_ID="your-client-id"
export GOOGLE_ADS_CLIENT_SECRET="your-client-secret"
export GOOGLE_ADS_DEVELOPER_TOKEN="your-dev-token"

# Run
node dist/index.js --campaign-id 123456789
```
```

### 3. Marki Uses the Skill
Once deployed, Marki can use the tool to fetch campaign data and optimize ad spend.

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
   Ask Boubou: "Delegate to Cody: Create a simple TypeScript utility that validates email addresses with proper types and error handling."

4. **Check result:**
   Cody should return spec, architecture, implementation, tests, and documentation.

## File Structure

```
workspace-software/
├── IDENTITY.md          # Cody's identity (name, vibe, emoji)
├── ROLE.md              # Purpose, scope, technical standards
├── AGENTS.md            # Operating instructions (updated with ROLE.md)
├── SOUL.md              # Personality (auto-generated)
├── USER.md              # User info (auto-generated)
├── TOOLS.md             # Tool conventions (auto-generated)
├── BOOTSTRAP.md         # First-run instructions (auto-generated)
├── SETUP.md             # This file
└── skills/              # Future: OpenClaw skills built by Cody
    ├── google-ads/
    ├── google-analytics/
    └── stripe-payments/
```

## Integration with Other Agents

### Cody → Marki
Cody builds tools (Google Ads API) → Marki uses tools (optimize campaigns)

### Boubou → Cody → Marki
Boubou identifies need → Delegates to Cody → Cody builds tool → Marki uses tool → Boubou evaluates impact

## Next Steps

1. ✅ Created workspace and files
2. ✅ Updated main agent AGENTS.md with delegation guidelines
3. ⏳ **YOU DO:** Add tool restrictions to `openclaw.json`
4. ⏳ **YOU DO:** Restart gateway (`openclaw gateway restart`)
5. ⏳ **TEST:** Delegate a task from main agent to Cody
6. 🔮 **FUTURE:** Cody builds Google Ads/Analytics skills for Marki

---

**Cody is ready to build! 🛠️**
