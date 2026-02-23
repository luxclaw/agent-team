# COMMUNICATION_MAP.md — Agent Communication Patterns

## Slack Channels

```
#general       — Weekly priorities, summaries, cross-team coordination
#engineering   — PRs, code reviews, technical discussions, architecture
#product       — Feature planning, market research, user insights, go-to-market
#data          — Algorithm updates, data pipeline, backtesting results
```

## Who Posts Where

| Channel | Primary Posters | Purpose |
|---------|----------------|---------|
| #general | Lux (lead), all agents | Priorities, summaries, announcements |
| #engineering | Mercury | PRs, code reviews, technical decisions, Copilot Issue updates |
| #product | Nova, Lux | Features, market research, user research, product strategy |
| #data | Mercury | Algorithm updates, data pipeline status, backtesting results |

## Agent Interaction Map

```
Lux 🔆 (CEO)
  ├── → Mercury ⚡  (assigns features, technical priorities)
  ├── → Nova ✨     (assigns product/market research tasks)
  ├── ← Mercury     (technical updates, PR status, blockers)
  └── ← Nova        (market insights, product recommendations)

Mercury ⚡ (CTO)
  ├── → Copilot     (creates GitHub Issues for code execution)
  ├── ← Copilot     (reviews PRs opened by Copilot)
  └── ↔ Nova        (product needs ↔ technical feasibility)

Nova ✨ (CMO)
  ├── → Copilot     (creates Issues for product-related code tasks)
  └── ↔ Mercury     (user needs → feature design)
```

## Communication Flow

### Feature Flow
```
Lux or Tisse (assigns feature)
  → Mercury or Nova (research & planning)
  → Mercury (technical design, Issue creation)
  → Copilot (code execution)
  → Mercury (PR review)
  → Tisse (final approval, merge)
```

### Research Flow
```
Nova (market research on schedule)
  → #product (findings posted)
  → Lux (incorporates into priorities)
  → Mercury (if feature work needed)
  → Copilot (if code needed)
```

### Algorithm Flow
```
Mercury (identifies improvement)
  → #data (proposal + rationale)
  → Copilot (Issue with specs)
  → Mercury (reviews PR, validates results)
  → Tisse (approves merge)
```

## When to @mention vs Regular Post

**@mention (needs attention now):**
- PR ready for review
- Blocker that needs unblocking
- Tisse asked something
- Production issue

**Regular post (read on next wake-up):**
- Status updates
- Research findings
- Ideas and proposals

## Response Expectations

| Urgency | Response Time | Examples |
|---------|--------------|----------|
| Urgent | < 1 hour | Production down, security issue, Tisse request |
| High | < 4 hours | PR review, blocker |
| Normal | < 24 hours | Feature questions, research, non-blocking |
