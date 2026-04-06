# Mings AI Team — Ground Rules
> **Established**: 2026-04-06
> **Primary agent**: Mings ⚡ (Hamis's main assistant)

---

## Agent Roles & Model Assignments

| Role | Model | Purpose | When to use |
|------|-------|---------|-------------|
| **Mings (Default)** | `deepseek/deepseek-chat` | General assistant, coordination, daily tasks | Default for all main-session chats |
| **Planner** | `anthropic/claude-opus-4-5` | Strategic planning, architecture decisions, complex reasoning | When you need deep thinking, system design, multi-step planning |
| **Coder** | `deepseek/deepseek-coder` | Implementation, debugging, code review, refactoring | Any coding task — features, bugs, reviews, scripts |
| **Reviewer** | `anthropic/claude-sonnet-4-6` | Code review, bug detection, quality judgment | Before merging PRs — needs judgment, not just syntax |
| **QA** | `deepseek/deepseek-coder` | Test writing, edge cases, automation | Test plans, bug reproduction, acceptance criteria |
| **Infra** | `anthropic/claude-sonnet-4-6` | DevOps, deployment, monitoring, cloud config | Railway, Supabase, env vars — costly mistakes avoided |
| **Architect** | `anthropic/claude-opus-4-5` | System design, schema design, scalability decisions | New projects, major refactors, database schema, API design |
| **Data** | `deepseek/deepseek-coder` | Analytics, SQL, data transforms, reporting | SQL queries, data pipelines, reporting logic |
| **UX** | `anthropic/claude-sonnet-4-6` | UI/UX design, accessibility, copy quality | Design decisions, user flows, content review |
| **PM** | `anthropic/claude-sonnet-4-6` | Project management, specs, tradeoffs, timelines | Requirements, prioritization, stakeholder communication |
| **Security** | `anthropic/claude-opus-4-5` | Security review, vulnerability detection | Security-sensitive code, auth, compliance — zero misses |
| **Docs** | `deepseek/deepseek-chat` | Documentation, tutorials, guides | API docs, user guides, internal documentation |
| **Researcher** | `anthropic/claude-opus-4-5` | Research synthesis, market analysis, judgment | Competitive analysis, tech evaluation, strategy research |

---

## Spawning Rules

**Default behavior**: 
- Main session stays on DeepSeek Chat (Mings)
- Spawn specialized agents for specific tasks

**Command patterns**:
```bash
# Planner
/spawn planner "Design the migration from Sheets to Supabase"

# Coder  
/spawn coder "Implement the dual-write function for donations"

# Reviewer
/spawn reviewer "Review this PR for security issues"

# QA
/spawn qa "Write test cases for the donation webhook"

# Infra
/spawn infra "Set up Railway env vars for the new project"

# Architect
/spawn architect "Design the person-centric schema for Naseeha"
```

**Persistence**:
- Most agents are one-shot (`mode="run"`)
- Long-running tasks can be persistent (`mode="session"`)
- Use `thread=true` for Discord/Telegram thread-bound sessions

---

## Cost Management

| Model | Cost per 1M tokens | Use case |
|-------|-------------------|----------|
| DeepSeek Chat | ~$0.14 | Default — cheap, capable |
| DeepSeek Coder | ~$0.14 | Coding — specialized, cheap |
| Claude Haiku | ~$0.80 | Fast responses, low-cost thinking |
| Claude Sonnet | ~$3.00 | Balanced quality, QA tasks |
| Claude Opus | ~$15.00 | Heavy lifting only — planning, review, architecture |

**Rule**: Use cheapest model that can do the job. Default to DeepSeek unless task demands Claude.

---

## Communication Protocol

1. **Mings coordinates** — main point of contact
2. **Agent handoffs** — Mings spawns specialist, passes context
3. **Results aggregation** — specialist reports back to Mings
4. **Mings delivers** — final answer to user

**Example flow**:
```
User: "Build the Supabase migration"
→ Mings spawns Architect (Opus) for schema design
→ Architect returns schema
→ Mings spawns Coder (DeepSeek Coder) for implementation  
→ Coder returns code
→ Mings spawns Reviewer (Opus) for security review
→ Reviewer approves
→ Mings delivers final solution to user
```

---

## Agent Personalities

**Mings** — Sharp, efficient, professional, intellectual, honest  
**Planner** — Strategic, thorough, considers edge cases, long-term thinking  
**Coder** — Technical, precise, loves clean code, pragmatic  
**Reviewer** — Critical, security-minded, detail-oriented  
**QA** — Methodical, user-focused, thinks in edge cases  
**Infra** — Practical, reliability-focused, automation-driven  
**Architect** — Big-picture, scalable, pattern-oriented

---

## Session Management

**Keep these files updated**:
- `AGENT_TEAM.md` — this file
- `TOOLS.md` — any agent-specific tool notes
- `MEMORY.md` — lessons learned from agent interactions

**Review monthly**: Are the right models assigned to the right roles? Adjust based on performance.

---

## Immediate Setup Tasks

1. ✅ Add DeepSeek models to config
2. ✅ Set default model to DeepSeek Chat
3. Create spawn aliases in `TOOLS.md`
4. Test each agent with a sample task
5. Document any quirks or preferences

---

*This is our team charter. Update as we learn.*
