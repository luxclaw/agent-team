# AUTONOMY.md — Agent Operations & Token Strategy

How agents wake up, work, collaborate, and how much it costs.

## Architecture: Brain + Hands

```
┌─────────────────────────────────────────────┐
│  BRAIN LAYER (OpenClaw on rPi 5)            │
│  Autonomous, proactive, persistent memory   │
│                                             │
│  Lux 🔆    Mercury ⚡    Nova ✨              │
│  (Sonnet)  (Sonnet)     (Sonnet)            │
│                                             │
│  Think → Plan → Research → Create Issues    │
└──────────────────┬──────────────────────────┘
                   │ GitHub Issues assigned
                   │ to @copilot
                   ▼
┌─────────────────────────────────────────────┐
│  HANDS LAYER (GitHub Copilot - FREE)        │
│  Reactive, executes code, opens PRs         │
│                                             │
│  Coding Agent        Code Review Agent      │
│  (writes code)       (reviews PRs)          │
└─────────────────────────────────────────────┘
```

- **Brain agents** (OpenClaw) do the thinking: strategy, research, planning, coordination, code review, Issue scoping
- **Hands agent** (Copilot) does the typing: writes code, runs tests, opens PRs — **for free** via Copilot Enterprise

---

## Model Assignments

| Agent | Model | $/1M In | $/1M Out | Why |
|-------|-------|---------|----------|-----|
| Lux 🔆 | Claude Sonnet | $3 | $15 | Coordination and strategic reasoning |
| Mercury ⚡ | Claude Sonnet | $3 | $15 | Technical reasoning, code review, architecture — delegates code writing to Copilot |
| Nova ✨ | Claude Sonnet | $3 | $15 | Market analysis, content strategy, product thinking |
| Copilot | GitHub-managed | $0 | $0 | Free unlimited via Enterprise subscription |

---

## Wake-Up Schedule (Cron Jobs)

Agents wake for specific tasks, do them, go back to sleep. Copilot only wakes when assigned an Issue.

### Lux 🔆 (CEO) — 3-4 wake-ups/week

| Cron | Time (PST) | Task | Est. Tokens |
|------|-----------|------|-------------|
| `0 9 * * 1` | Mon 9am | Weekly priorities: review last week, assign features to Mercury/Nova, post to #general | ~8K in / ~2K out |
| `0 12 * * 3` | Wed noon | Midweek check: scan channels for blockers, check PR/Issue status. HEARTBEAT_OK if nothing. | ~4K in / ~500 out |
| `0 16 * * 5` | Fri 4pm | Weekly wrap: summarize progress, post to #general, update memory | ~6K in / ~2K out |

**Reactive:** Wakes on @mention (conflict, escalation, Tisse question). ~2 reactive/week at ~4K in / ~1K out each.

### Mercury ⚡ (CTO) — 5-7 wake-ups/week

| Cron | Time (PST) | Task | Est. Tokens |
|------|-----------|------|-------------|
| `0 10 * * 1-5` | Weekdays 10am | Morning check: review Copilot PRs, check CI, scan #engineering. Create new Issues if work is ready. | ~6K in / ~2K out |
| `0 14 * * 1,3` | Mon/Wed 2pm | Deep work: algo research, architecture planning, technical design. Scope Issues for Copilot. | ~10K in / ~4K out |

**Reactive:** Wakes on @mentions and PR notifications. ~3 reactive/week at ~5K in / ~2K out each.

### Nova ✨ (CMO) — 2-3 wake-ups/week

| Cron | Time (PST) | Task | Est. Tokens |
|------|-----------|------|-------------|
| `0 11 * * 1` | Mon 11am | Weekly market scan: competitors, trending topics, user sentiment. Post to #product. | ~6K in / ~3K out |
| `0 11 * * 4` | Thu 11am | Product research: deeper dive on one topic. Post to #product. Create Issues if code work needed. | ~6K in / ~3K out |

**Reactive:** Wakes on @mentions. ~1 reactive/week at ~4K in / ~2K out.

---

## Weekly Token Budget

### Lux 🔆 (Claude Sonnet)

| Activity | Frequency | Input | Output |
|----------|-----------|-------|--------|
| Monday priorities | 1/week | 8K | 2K |
| Midweek check | 1/week | 4K | 500 |
| Friday wrap | 1/week | 6K | 2K |
| Reactive | ~2/week | 8K | 2K |
| **Weekly Total** | | **26K** | **6.5K** |

**Monthly cost:** (104K × $3 + 26K × $15) / 1M = **$0.70/mo**

### Mercury ⚡ (Claude Sonnet)

| Activity | Frequency | Input | Output |
|----------|-----------|-------|--------|
| Morning checks | 5/week | 30K | 10K |
| Deep work sessions | 2/week | 20K | 8K |
| Reactive (PRs, mentions) | ~3/week | 15K | 6K |
| **Weekly Total** | | **65K** | **24K** |

**Monthly cost:** (260K × $3 + 96K × $15) / 1M = **$2.22/mo**

### Nova ✨ (Claude Sonnet)

| Activity | Frequency | Input | Output |
|----------|-----------|-------|--------|
| Monday market scan | 1/week | 6K | 3K |
| Thursday research | 1/week | 6K | 3K |
| Reactive | ~1/week | 4K | 2K |
| **Weekly Total** | | **16K** | **8K** |

**Monthly cost:** (64K × $3 + 32K × $15) / 1M = **$0.67/mo**

---

## Total Monthly Cost

| Agent | Platform | Monthly Cost |
|-------|----------|-------------|
| Lux 🔆 | OpenClaw (Sonnet) | ~$0.70 |
| Mercury ⚡ | OpenClaw (Sonnet) | ~$2.22 |
| Nova ✨ | OpenClaw (Sonnet) | ~$0.67 |
| Copilot | GitHub Enterprise | $0.00 |
| **Total** | | **~$3.59/mo** |

**Realistic range with growth:** $4–10/mo as agents get busier and create more Issues.

---

## Copilot Execution Guidelines

### When to Create an Issue for Copilot
- Feature implementation (new endpoints, UI components, data flows)
- Bug fixes with clear reproduction steps
- Refactoring with well-defined scope
- Test coverage improvements
- Documentation updates
- Dependency updates

### When NOT to Use Copilot
- Ambiguous tasks that need human judgment
- Architecture decisions (Mercury decides, then scopes the Issue)
- Research or analysis (agents do this themselves)
- Tasks requiring external API exploration or experimentation

### Maximizing Copilot Quality
- **One task per Issue** — don't bundle
- **Include acceptance criteria** — testable, specific
- **Reference relevant files** — "see `src/screener/engine.js`"
- **Include constraints** — "don't modify the grading scale"
- **Label appropriately** — `feature`, `bugfix`, `refactor`, `maintenance`

---

## Automated Maintenance (GitHub Actions Cron)

For recurring tasks that don't need agent judgment, skip the brain layer entirely:

```yaml
# .github/workflows/weekly-maintenance.yml
name: Weekly Maintenance
on:
  schedule:
    - cron: '0 14 * * 1'  # Monday 6am PST
jobs:
  create-maintenance-issue:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/github-script@v7
        with:
          script: |
            await github.rest.issues.create({
              owner: context.repo.owner,
              repo: context.repo.repo,
              title: `Weekly: Dependency audit and update (${new Date().toISOString().slice(0,10)})`,
              body: 'Run npm audit, update non-breaking dependencies, ensure all tests pass.',
              assignees: ['copilot'],
              labels: ['maintenance']
            });
```

This gives you free automated maintenance without burning any OpenClaw tokens.

---

## Heartbeat Strategy

**Heartbeats OFF for all agents.** Use cron jobs instead.

- Cron schedule (above) = ~10-12 wake-ups/week total across all agents
- Heartbeat every 30 min would = 48/day × 3 agents = 1,008/week

If you later need real-time alerting, add a single lightweight heartbeat on Mercury only.

---

## Token Efficiency Tips

1. **Keep system prompts lean** — every wake-up loads AGENTS.md + SOUL.md + role file
2. **Prompt caching** — both providers cache identical system prompts at 50-90% discount
3. **HEARTBEAT_OK is cheap** — design checks so "nothing to do" is the common path
4. **Let Copilot do the heavy lifting** — agents think, Copilot types
5. **Batch Issue creation** — Mercury creates multiple Issues in one session rather than one per wake-up
