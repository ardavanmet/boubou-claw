# OpenClaw Workspace - CarAid Agent Configuration

This workspace contains the configuration and context files for the OpenClaw AI agent system supporting CarAid.

## Architecture Approach

### Multi-Agent Orchestration Model

We use a **main agent as orchestrator** pattern:

- **Main Agent** (this workspace) - Strategic orchestrator with full business context
- **Specialized Agents** (future workspaces) - Domain-specific executors with narrow focus

The main agent:
- Maintains full CarAid mission and business context
- Applies strategic frameworks to all decisions
- Delegates technical/specialized work to other agents
- Synthesizes results through investor and revenue lens
- Acts as single point of contact for the founder

Specialized agents (when created):
- Execute specific technical tasks
- Have limited, role-specific context
- Return results to main agent for synthesis
- Don't need full business context

### Why This Approach?

1. **Single conversation partner** - Founder interacts only with main agent
2. **Context preservation** - Main agent maintains continuity across all work
3. **Leverage OpenClaw tools** - Uses `sessions_send` and `sessions_spawn` for delegation
4. **Scalable** - Easy to add new specialists without changing workflow
5. **Strategic focus** - Main agent always applies fundraising/revenue lens

---

## File Structure

### Core Configuration Files

**SOUL.md** - Personality, tone, boundaries
- Strategic, founder-level mindset
- Orchestrator role definition
- Communication style

**USER.md** - Information about the founder
- Name, timezone, preferences
- Context about what they care about
- Evolves over time

**CARAID.md** - Business mission and context
- What CarAid is and why it exists
- Current state and constraints
- Primary bottleneck (fundraising + revenue)
- Dual strategic tracks
- Near-term objectives

**PLAYBOOK.md** - Decision frameworks and methods
- Leverage tier prioritization (Tier 1-4)
- Structured output format (Context → Implications → Risks → Recommendation → Next Step)
- Industry outreach methodology
- Investor-lens filter
- Orchestrator role guidelines

**AGENTS.md** - Operating instructions
- Session reading list (what to read each session)
- Memory conventions
- File organization

**TOOLS.md** - Tool usage notes and conventions
- User-specific tool preferences
- Custom workflows

**IDENTITY.md** - Agent name, emoji, vibe
- How the agent identifies itself

### Memory Files

**MEMORY.md** - Long-term curated memory
- Only loaded in main session (direct chats)
- Persistent context across sessions
- Key decisions, learnings, patterns

**memory/YYYY-MM-DD.md** - Daily session logs
- Raw logs of what happened each day
- Agent reads today + yesterday for recent context
- Auto-created as needed

---

## Session Bootstrap Process

Every session, the agent automatically:

1. Reads `SOUL.md` - Understands who it is
2. Reads `USER.md` - Understands who it's helping
3. Reads `CARAID.md` - Loads business mission and context
4. Reads `PLAYBOOK.md` - Loads decision frameworks
5. Reads `memory/YYYY-MM-DD.md` - Gets recent context (today + yesterday)
6. Reads `MEMORY.md` - Loads long-term memory (main session only)

This ensures the agent has full context before responding to any request.

---

## Decision Framework Summary

All work is evaluated through:

### Leverage Tiers
- **Tier 1** - Fundraising critical
- **Tier 2** - Revenue impact
- **Tier 3** - Defensibility
- **Tier 4** - Nice-to-have

### Investor Lens (5 Questions)
1. Traction signal?
2. Scalability signal?
3. Founder capability signal?
4. Market timing signal?
5. Competitive moat signal?

### Structured Output
Every recommendation includes:
1. Context
2. Implications
3. Risks
4. Recommendation
5. Next Step

---

## Current Focus (Feb 2026)

**Primary Bottleneck:** Preparing for angel round while increasing revenue and conversion rate

**Dual Strategic Tracks:**
1. Fundraising readiness (pitch, metrics, narrative)
2. Revenue & conversion acceleration (traction signals)

**Stage:** Validation (solo founder, lean operation, proving the model)

---

## Future Agent Workspaces

When creating specialized agents:

### Workspace Structure
```
/home/ardi/.openclaw/workspace/          # Main agent (this)
/home/ardi/.openclaw/workspace-work/     # Work agent (technical execution)
/home/ardi/.openclaw/workspace-support/  # Support agent (customer-facing)
```

### Recommended Approach
- **Main agent** keeps full context (CARAID.md, PLAYBOOK.md)
- **Specialized agents** get lightweight ROLE.md files
- Main agent delegates via `sessions_send` or `sessions_spawn`
- Specialists return results, main agent synthesizes with strategic context

### Example Delegation Flow
```
Founder → Main Agent: "Analyze this estimate for accuracy"
Main Agent → Work Agent: "Check damage detection accuracy on this estimate"
Work Agent → Main Agent: [technical analysis results]
Main Agent → Founder: [synthesis with business implications, investor lens]
```

---

## Git Repository

This workspace is tracked at: `https://github.com/ardavanmet/boubou-claw`

**What's tracked:**
- All workspace files (SOUL.md, CARAID.md, PLAYBOOK.md, etc.)
- .windsurf/workflows/ (OpenClaw context documentation)
- Future workspace-* folders (when created)

**What's excluded (.gitignore):**
- openclaw.json (contains tokens)
- credentials/, devices/, identity/ (auth data)
- logs/, agents/, telegram/ (runtime data)

---

## Maintenance

### When to Update Files

**CARAID.md** - When business context changes
- New strategic priorities
- Market learnings
- Pivot or focus shift

**PLAYBOOK.md** - When decision frameworks evolve
- New prioritization methods
- Refined investor lens
- Updated operating procedures

**SOUL.md** - When agent personality/role changes
- Tone adjustments
- Role clarification
- Boundary updates

**MEMORY.md** - Continuously
- Key decisions made
- Important patterns learned
- Context worth preserving

### Version Control
Commit changes with clear messages:
```bash
git add workspace/
git commit -m "Update CARAID.md with Q2 priorities"
git push origin main
```

---

## Contact

This workspace is maintained by Ardavan (Ardav) for CarAid.

For OpenClaw documentation, see: `.windsurf/workflows/openclaw-context.md`
