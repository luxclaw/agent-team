# AUTONOMY.md — Agent Operations & Token Strategy

How agents wake up, work, collaborate, and how much it costs.

## Infrastructure

- **Runtime:** OpenClaw (self-hosted, open source)
- **Hardware:** Raspberry Pi 5
- **Communication:** Slack (agents are Slack bots)
- **Scheduling:** OpenClaw cron jobs + heartbeat system

---

## Model Assignments & Rationale

| Agent | Model | $/1M In | $/1M Out | Why This Model |
|-------|-------|---------|----------|----------------|
| Lux �� | Claude Sonnet 4 | $3 | $15 | Strategic reasoning but mostly coordination — doesn't need Opus-level reasoning for weekly summaries and conflict resolution. Sonnet handles nuanced thinking well at 1/5th the output cost. |
| Mercury ⚡ | GPT-5.2 Codex | $1.75 | $14 | Best code generation and review per dollar. Codex is purpose-built for writing, reading, and reviewing code. |
| Quant 📊 | GPT-5.2 Codex | $1.75 | $14 | Same reasoning — algorithm work is code-heavy. Data analysis, backtesting, pipeline work all benefit from Codex optimization. |
| Nova ✨ | Claude Sonnet 4 | $3 | $15 | Market research, content strategy, and product thinking require strong reasoning and writing. Sonnet excels at analysis and prose. |

### Why NOT Opus for Lux?

Opus ($5/$25) is 67% more expensive on output than Sonnet ($3/$15). Lux's job is coordination, prioritization, and conflict resolution — not deep novel reasoning. Sonnet handles this well. Save Opus for if you ever need a "deep think" one-off task.

### Why NOT Sonnet for Mercury/Quant?

Codex ($1.75/$14) is 42% cheaper on input than Sonnet ($3/$15) and optimized specifically for code tasks. Mercury and Quant are code-heavy roles — Codex is purpose-built for their work.

---

## Wake-Up Schedule (Cron Jobs)

The key insight: **agents don't need to be "on" all day.** They wake up for specific tasks, do them, and go back to sleep. This is dramatically cheaper than continuous heartbeats.

### Lux 🔆 (CEO) — 3 wake-ups/day

| Cron | Time (PST) | Task | Est. Tokens |
|------|-----------|------|-------------|
| `0 9 * * 1` | Mon 9am | Weekly priorities: review last week, set this week's focus, post to #general | ~8K in / ~2K out |
| `0 12 * * 2-4` | Tue-Thu noon | Midweek check: scan channels for blockers, unresolved issues. HEARTBEAT_OK if nothing. | ~4K in / ~500 out |
| `0 16 * * 5` | Fri 4pm | Weekly wrap: summarize progress, post to #general, update memory | ~6K in / ~2K out |

**Reactive:** Also wakes on @mention in Slack (conflict, escalation, Tisse question). Budget ~3 reactive wake-ups/week at ~4K in / ~1K out each.

### Mercury ⚡ (CTO) — 2 scheduled + reactive

| Cron | Time (PST) | Task | Est. Tokens |
|------|-----------|------|-------------|
| `0 10 * * 1-5` | Weekdays 10am | Morning check: scan #engineering for PRs to review, check CI status | ~5K in / ~500 out |
| `0 14 * * 1,3,5` | MWF 2pm | Afternoon work session: implement features, respond to design questions | ~8K in / ~4K out |

**Reactive:** Wakes on PR notifications and @mentions. Budget ~5 reactive/week at ~6K in / ~3K out each (code reviews are token-heavy).

### Quant 📊 — 1 scheduled + reactive

| Cron | Time (PST) | Task | Est. Tokens |
|------|-----------|------|-------------|
| `0 6 * * 1-5` | Weekdays 6am | Data check: verify overnight refresh, check data quality, run validation | ~5K in / ~1K out |

**Reactive:** Wakes on @mentions (data requests from Mercury, PR reviews). Budget ~3 reactive/week at ~6K in / ~3K out each.

Quant's heavy work (algorithm development, backtesting) happens in focused sessions when Lux assigns priorities — not on a schedule. These are longer sessions (~15K in / ~8K out) budgeted ~2/week.

### Nova ✨ (CMO) — 2 scheduled/week

| Cron | Time (PST) | Task | Est. Tokens |
|------|-----------|------|-------------|
| `0 11 * * 1` | Mon 11am | Weekly market scan: check competitors, trending topics, user sentiment. Post findings to #product | ~6K in / ~3K out |
| `0 11 * * 4` | Thu 11am | Product research: deeper dive on one topic (competitor feature, user need, go-to-market idea). Post to #product | ~6K in / ~3K out |

**Reactive:** Wakes on @mentions. Budget ~2 reactive/week at ~4K in / ~2K out each.

---

## Weekly Token Budget Estimate

### Lux 🔆 (Claude Sonnet)

| Activity | Frequency | Input Tokens | Output Tokens |
|----------|-----------|-------------|---------------|
| Monday priorities | 1/week | 8,000 | 2,000 |
| Midweek checks | 3/week | 12,000 | 1,500 |
| Friday wrap | 1/week | 6,000 | 2,000 |
| Reactive (mentions) | ~3/week | 12,000 | 3,000 |
| **Weekly Total** | | **38,000** | **8,500** |

**Weekly cost:** (38K × $3 + 8.5K × $15) / 1M = **$0.24/week**
**Monthly cost:** ~**$1.00**

### Mercury ⚡ (GPT-5.2 Codex)

| Activity | Frequency | Input Tokens | Output Tokens |
|----------|-----------|-------------|---------------|
| Morning checks | 5/week | 25,000 | 2,500 |
| Afternoon sessions | 3/week | 24,000 | 12,000 |
| PR reviews (reactive) | ~5/week | 30,000 | 15,000 |
| **Weekly Total** | | **79,000** | **29,500** |

**Weekly cost:** (79K × $1.75 + 29.5K × $14) / 1M = **$0.55/week**
**Monthly cost:** ~**$2.40**

### Quant 📊 (GPT-5.2 Codex)

| Activity | Frequency | Input Tokens | Output Tokens |
|----------|-----------|-------------|---------------|
| Daily data check | 5/week | 25,000 | 5,000 |
| Reactive (mentions/reviews) | ~3/week | 18,000 | 9,000 |
| Deep work sessions | ~2/week | 30,000 | 16,000 |
| **Weekly Total** | | **73,000** | **30,000** |

**Weekly cost:** (73K × $1.75 + 30K × $14) / 1M = **$0.55/week**
**Monthly cost:** ~**$2.40**

### Nova ✨ (Claude Sonnet)

| Activity | Frequency | Input Tokens | Output Tokens |
|----------|-----------|-------------|---------------|
| Monday market scan | 1/week | 6,000 | 3,000 |
| Thursday research | 1/week | 6,000 | 3,000 |
| Reactive (mentions) | ~2/week | 8,000 | 4,000 |
| **Weekly Total** | | **20,000** | **10,000** |

**Weekly cost:** (20K × $3 + 10K × $15) / 1M = **$0.21/week**
**Monthly cost:** ~**$0.90**

---

## Total Monthly Cost Estimate

| Agent | Model | Monthly Tokens (In) | Monthly Tokens (Out) | Monthly Cost |
|-------|-------|--------------------|--------------------|-------------|
| Lux 🔆 | Sonnet | ~152K | ~34K | ~$1.00 |
| Mercury ⚡ | Codex | ~316K | ~118K | ~$2.40 |
| Quant 📊 | Codex | ~292K | ~120K | ~$2.40 |
| Nova ✨ | Sonnet | ~80K | ~40K | ~$0.90 |
| **Total** | | **~840K** | **~312K** | **~$6.70/mo** |

### Cost Scaling Notes

These estimates assume **lean, focused interactions.** Costs increase if:
- Agents have long conversations in Slack threads (context window grows)
- Large files are attached to context (code files, data dumps)
- Agents are triggered more frequently (high PR volume, frequent escalations)
- System prompts are large (keep AGENTS.md + role files + SOUL.md concise)

**Realistic range with growth:** $7–15/month as the team gets busier.

**Hard ceiling strategy:** Set OpenClaw token budget limits per agent to prevent runaway costs.

---

## Collaboration Model (Async Meetings)

### No Synchronous Meetings

Agents don't "meet." They communicate through Slack channels asynchronously. This is cheaper and more natural for AI agents.

### How Collaboration Actually Works

**Example: New Feature**
```
Mon 11am  → Nova posts market insight to #product
Mon 12pm  → Lux reads it during midweek check, validates, posts priority to #general
Tue 10am  → Mercury reads priority during morning check, starts designing
Tue 2pm   → Mercury posts design to #product, @mentions Nova for feedback
Thu 11am  → Nova reads during research session, responds with user perspective
Fri 10am  → Mercury implements on branch, opens PR
Fri 10am  → Quant gets PR notification, reviews code
Sat/Sun   → Tisse reviews when available, approves
Mon       → Merge to main
```

**Example: Algorithm Improvement**
```
Mon 6am   → Quant notices data pattern during daily check, investigates
Mon       → Quant works on improvement (deep work session)
Tue 6am   → Quant runs backtests during daily check
Wed       → Quant opens PR with results, posts to #engineering
Wed 10am  → Mercury reviews during morning check
Thu       → Tisse reviews, approves
```

### Cross-Agent Handoffs

Agents hand off work by posting structured messages to Slack channels. The receiving agent picks it up on their next wake-up.

**Key rule:** Don't @mention unless time-sensitive. Let agents pick up work on their natural schedule. @mentions trigger a reactive wake-up (costs tokens).

---

## Heartbeat Strategy

Use OpenClaw heartbeats sparingly — they're expensive if frequent.

### Recommended: Heartbeat OFF for all agents

Instead of heartbeats (which poll every N minutes), use **cron jobs** (which fire at specific times). This is dramatically cheaper:
- Heartbeat every 30 min = 48 wake-ups/day × 4 agents = 192 API calls/day
- Cron schedule (as above) = ~12 wake-ups/day total across all agents

### Exception: Enable heartbeat only for urgent monitoring

If you later need real-time alerting (production down, etc.), add a single lightweight heartbeat on one agent — not all four.

---

## Token Efficiency Tips

### 1. Keep System Prompts Lean
Every wake-up loads the system prompt. For a ~3K token system prompt, that's 3K input tokens × every invocation. Keep role files and AGENTS.md concise.

### 2. Use Prompt Caching
Both OpenAI and Anthropic offer prompt caching. If the system prompt is identical across invocations (it usually is), cached input tokens cost ~50-90% less. OpenClaw should leverage this automatically.

### 3. Limit Context Window
Don't load full chat history on every wake-up. Use OpenClaw's context management to truncate or summarize old messages.

### 4. Batch Work
Instead of 5 small wake-ups, prefer 2 longer focused sessions. Each wake-up has fixed overhead (system prompt, context loading). Fewer, longer sessions are more efficient.

### 5. HEARTBEAT_OK is Cheap
When an agent wakes up and has nothing to do, a quick "HEARTBEAT_OK" response costs almost nothing (~100 output tokens). Design cron checks so "nothing to do" is the common case.

---

## OpenClaw Configuration Notes

### Per-Agent Setup
Each agent is a separate OpenClaw instance with:
- Its own Slack bot identity
- Its own model provider/API key configuration
- Its own system prompt (AGENTS.md + SOUL.md + role file)
- Its own cron schedule
- Its own memory/workspace

### Cron Configuration
```yaml
# Example: Lux's cron schedule
cron:
  - schedule: "0 9 * * 1"      # Mon 9am PST
    task: "Weekly priorities"
    channel: "#general"
  - schedule: "0 12 * * 2-4"   # Tue-Thu noon
    task: "Midweek check"
    channel: "#general"
  - schedule: "0 16 * * 5"     # Fri 4pm PST
    task: "Weekly wrap"
    channel: "#general"
```

### Token Budget Limits
Set per-agent monthly token limits in OpenClaw to prevent runaway costs:
- Lux: 250K input / 50K output
- Mercury: 500K input / 200K output
- Quant: 500K input / 200K output
- Nova: 150K input / 75K output
