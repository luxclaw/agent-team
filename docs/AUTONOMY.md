# AUTONOMY.md — Agent Operations & Token Strategy

How agents wake up, work, and keep the pipeline full.

## Design Philosophy

**Tisse should check in and find a queue of polished, reviewed PRs waiting for approval.** The system runs continuously — agents research, scope Issues, Copilot writes code, agents review and iterate. By the time Tisse looks, the work is done and ready for sign-off.

### Pipeline Model

Multiple features and improvements flow through the system simultaneously:

```
BACKLOG          IN PROGRESS       IN REVIEW         READY FOR TISSE
┌──────────┐    ┌──────────┐     ┌──────────┐      ┌──────────┐
│ Feature A │    │ Feature C │     │ Feature E │      │ Feature G │ ← approve
│ Feature B │    │ Feature D │     │ Feature F │      │ Feature H │ ← approve
│ Algo fix  │    │ Bug fix   │     │           │      │ Algo v2   │ ← approve
│ ...       │    │           │     │           │      │           │
└──────────┘    └──────────┘     └──────────┘      └──────────┘
   Nova +           Copilot          Mercury           Tisse
   Mercury          coding           reviewing         approving
   scoping                           + iterating
```

**Target: 3-5 Issues in Copilot's queue at all times.** Mercury reviews PRs within hours, not days. Copilot iterates on feedback. Tisse gets polished PRs.

---

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
│  Review PRs → Iterate → Queue for Tisse     │
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

---

## Model Assignments

| Agent | Model | $/1M In | $/1M Out | Why |
|-------|-------|---------|----------|-----|
| Lux 🔆 | Claude Sonnet | $3 | $15 | Coordination and strategic reasoning |
| Mercury ⚡ | Claude Sonnet | $3 | $15 | Technical reasoning, code review, architecture |
| Nova ✨ | Claude Sonnet | $3 | $15 | Market analysis, content strategy, product thinking |
| Copilot | GitHub-managed | $0 | $0 | Free unlimited via Enterprise subscription |

---

## Wake-Up Schedules

### Mercury ⚡ (CTO) — The Engine

Mercury is the highest-activity agent. He keeps the pipeline flowing.

| Cron | Time (PST) | Task |
|------|-----------|------|
| `0 8 * * 1-5` | Weekdays 8am | **Morning review:** Review all open Copilot PRs. Approve good ones (label `ready-for-tisse`). Request changes on bad ones with specific feedback. Check CI status. |
| `0 11 * * 1-5` | Weekdays 11am | **Issue creation:** Scope and create 1-3 new Issues for Copilot from the backlog. Prioritize by Lux's weekly priorities. Deep technical design for complex features. |
| `0 15 * * 1-5` | Weekdays 3pm | **Afternoon follow-up:** Review PRs from morning Issues. Check if Copilot iterated on requested changes. Create follow-up Issues for next steps. Review any PRs Nova created Issues for. |
| `0 19 * * 1-5` | Weekdays 7pm | **Evening pipeline check:** Final PR review pass. Ensure Issue queue has work for overnight/next morning. Post daily summary to #engineering. Queue tomorrow's priorities. |
| `0 11 * * 6` | Sat 11am | **Weekend check:** Light review of any open PRs. Create Issues if backlog is low. Keep pipeline moving. |

**Reactive:** Wakes on @mentions and PR notifications. ~5/week.

**Per-session estimates:**
- Morning review: ~10K in / ~4K out (reading PR diffs, writing review comments)
- Issue creation: ~12K in / ~6K out (deep technical scoping, writing detailed Issues)
- Afternoon follow-up: ~10K in / ~4K out
- Evening check: ~8K in / ~3K out
- Weekend check: ~6K in / ~2K out
- Reactive: ~6K in / ~3K out

### Nova ✨ (CMO) — The Researcher

Nova runs a continuous research pipeline feeding Mercury with product direction.

| Cron | Time (PST) | Task |
|------|-----------|------|
| `0 9 * * 1-5` | Weekdays 9am | **Daily research:** Rotate through research areas (see schedule below). Post findings to #product. Create Issues for product-related code if needed. |
| `0 14 * * 2,4` | Tue/Thu 2pm | **Deep dive:** Extended research session on one high-priority topic. Competitive teardown, user persona analysis, or go-to-market experiment design. |
| `0 10 * * 6` | Sat 10am | **Weekly synthesis:** Combine the week's research into actionable recommendations for Lux. Update product strategy notes. |

**Daily research rotation:**
- **Monday:** Competitor scan (what shipped, pricing changes, new features)
- **Tuesday:** User sentiment (Reddit, Twitter/X, investing forums — what are people asking for?)
- **Wednesday:** Content strategy (what content would attract our target users?)
- **Thursday:** Product-market fit check (are we building the right thing? gaps?)
- **Friday:** Growth channels (which channels are working? what to try next?)

**Reactive:** Wakes on @mentions. ~3/week.

**Per-session estimates:**
- Daily research: ~8K in / ~4K out
- Deep dive: ~12K in / ~6K out
- Weekly synthesis: ~10K in / ~5K out
- Reactive: ~5K in / ~3K out

### Lux 🔆 (CEO) — The Coordinator

Lux keeps everything aligned and moving. Daily presence, not just weekly.

| Cron | Time (PST) | Task |
|------|-----------|------|
| `0 9 * * 1` | Mon 9am | **Weekly planning:** Review last week (merged PRs, closed Issues, Nova's research). Set this week's priorities. Assign features to Mercury/Nova. Post to #general. |
| `0 9 * * 2-5` | Tue-Fri 9am | **Daily check-in:** Scan all channels. Check pipeline status (Issues in queue, PRs in review, PRs ready for Tisse). Unblock agents. Post brief update to #general if needed. HEARTBEAT_OK if all clear. |
| `0 17 * * 5` | Fri 5pm | **Weekly wrap:** Summarize the week's progress. List PRs ready for Tisse. Flag anything that needs founder input. Post to #general. Update memory. |
| `0 20 * * 0` | Sun 8pm | **Week-ahead prep:** Review Nova's weekly synthesis. Draft Monday's priorities. Ensure Issue backlog is healthy for the week. |

**Reactive:** Wakes on @mentions (conflicts, escalations, Tisse messages). ~3/week.

**Per-session estimates:**
- Weekly planning: ~12K in / ~4K out
- Daily check-in: ~6K in / ~1.5K out
- Weekly wrap: ~10K in / ~3K out
- Week-ahead prep: ~8K in / ~3K out
- Reactive: ~5K in / ~2K out

---

## Weekly Token Budget

### Mercury ⚡

| Activity | Frequency | Input | Output |
|----------|-----------|-------|--------|
| Morning review | 5/week | 50K | 20K |
| Issue creation | 5/week | 60K | 30K |
| Afternoon follow-up | 5/week | 50K | 20K |
| Evening check | 5/week | 40K | 15K |
| Weekend check | 1/week | 6K | 2K |
| Reactive | ~5/week | 30K | 15K |
| **Weekly Total** | | **236K** | **102K** |

**Monthly cost:** (944K × $3 + 408K × $15) / 1M = **$8.95/mo**

### Nova ✨

| Activity | Frequency | Input | Output |
|----------|-----------|-------|--------|
| Daily research | 5/week | 40K | 20K |
| Deep dive | 2/week | 24K | 12K |
| Weekly synthesis | 1/week | 10K | 5K |
| Reactive | ~3/week | 15K | 9K |
| **Weekly Total** | | **89K** | **46K** |

**Monthly cost:** (356K × $3 + 184K × $15) / 1M = **$3.83/mo**

### Lux 🔆

| Activity | Frequency | Input | Output |
|----------|-----------|-------|--------|
| Weekly planning | 1/week | 12K | 4K |
| Daily check-in | 4/week | 24K | 6K |
| Weekly wrap | 1/week | 10K | 3K |
| Week-ahead prep | 1/week | 8K | 3K |
| Reactive | ~3/week | 15K | 6K |
| **Weekly Total** | | **69K** | **22K** |

**Monthly cost:** (276K × $3 + 88K × $15) / 1M = **$2.15/mo**

---

## Total Monthly Cost

| Agent | Wake-ups/Week | Monthly Cost |
|-------|--------------|-------------|
| Mercury ⚡ | ~21 scheduled + ~5 reactive | ~$8.95 |
| Nova ✨ | ~8 scheduled + ~3 reactive | ~$3.83 |
| Lux 🔆 | ~7 scheduled + ~3 reactive | ~$2.15 |
| Copilot | Unlimited (free) | $0.00 |
| **Total** | **~47/week** | **~$14.93/mo** |

**Budget: $50/mo. Current estimate: ~$15/mo.** This leaves ~$35/mo headroom for:
- Longer sessions when agents need deeper research or complex Issue scoping
- More reactive wake-ups during busy periods
- Scaling up if the product takes off and needs more velocity

---

## Pipeline Management

### Issue Lifecycle

```
DRAFT → READY → ASSIGNED → IN PROGRESS → PR OPEN → REVIEW → READY FOR TISSE → MERGED
```

**Labels:**
- `draft` — Mercury is still scoping
- `ready` — Fully scoped, ready to assign to Copilot
- `in-progress` — Copilot is working on it
- `in-review` — PR open, Mercury reviewing
- `changes-requested` — Mercury sent feedback, Copilot iterating
- `ready-for-tisse` — Mercury approved, waiting for Tisse's final sign-off
- `urgent` — Skip the queue, immediate attention

### Parallel Work Streams

Mercury should maintain **3-5 Issues assigned to Copilot at any time** across different areas:

```
Stream 1: Algorithm (Engine Power improvements, new metrics, backtesting)
Stream 2: App feature (dashboard, UX, new endpoint)
Stream 3: Data pipeline (refresh, quality, optimization)
Stream 4: Bug fixes / maintenance (as needed)
```

This means when Tisse checks in, there are multiple PRs at different stages — some ready to approve, some in review, some in progress. The system never stalls waiting for one person.

### Mercury's Review Loop

Mercury doesn't just approve/reject — he iterates:

1. **Copilot opens PR** → Mercury reviews
2. **If good:** Label `ready-for-tisse`, post summary to #engineering
3. **If needs work:** Request specific changes in PR comments → Copilot iterates → Mercury re-reviews
4. **If fundamentally wrong:** Close PR, rewrite the Issue with better specs, re-assign to Copilot

Goal: PRs labeled `ready-for-tisse` should be high quality. Tisse's review is a final check, not a debugging session.

### When Tisse Checks In

Tisse should see a clear picture:
- **#general** — Lux's latest update with pipeline status
- **GitHub PRs** — Filter by `ready-for-tisse` label for quick approval queue
- **#engineering** — Mercury's summaries of what each PR does

Approve in batch, merge, move on. The team keeps shipping while you're away.

---

## Copilot Execution Guidelines

### Maximizing Throughput
- **One task per Issue** — don't bundle multiple features
- **Include acceptance criteria** — testable, specific
- **Reference relevant files** — "see `src/screener/engine.js`"
- **Include constraints** — "don't modify the grading scale"
- **Label appropriately** — `feature`, `bugfix`, `refactor`, `maintenance`
- **Scope small** — 2-3 hour tasks, not week-long epics. Break big features into multiple Issues.
- **Chain Issues** — "After Issue #12 merges, implement Issue #13 which builds on it"

### When Copilot Fails
- If Copilot produces bad output, Mercury rewrites the Issue with more detail
- If it fails twice on the same Issue, Mercury simplifies the scope or writes the code directly
- Track failure patterns — if Copilot consistently struggles with a type of task, adjust Issue templates

---

## Automated Maintenance (GitHub Actions Cron)

Skip the brain layer for recurring tasks:

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

---

## Heartbeat Strategy

**Heartbeats OFF.** Cron schedules provide sufficient coverage:
- Mercury checks in 4x/day on weekdays
- Lux checks in daily
- Nova checks in daily

If real-time alerting is needed later, add a lightweight heartbeat on Mercury only.

---

## Token Efficiency Tips

1. **Prompt caching** — all 3 agents use Sonnet; identical system prompts get cached at 50-90% discount
2. **Batch work** — Mercury creates multiple Issues per session, not one per wake-up
3. **HEARTBEAT_OK is cheap** — Lux's daily check-ins should often be "all clear" (~100 output tokens)
4. **Let Copilot do the heavy lifting** — agents think, Copilot types
5. **Small Issues** — smaller scope = higher Copilot success rate = less iteration = fewer Mercury review cycles
