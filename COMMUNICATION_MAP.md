# COMMUNICATION_MAP.md — Agent Communication Patterns

## Slack Channels

```
#general       — Weekly priorities, summaries, cross-team coordination
#engineering   — PRs, code reviews, technical discussions, architecture
#product       — Feature planning, UX/UI, market research, go-to-market
#data          — Data quality, pipeline status, algorithm updates, backtesting
```

## Who Posts Where

| Channel | Primary Posters | Purpose |
|---------|----------------|---------|
| #general | Lux (lead), all agents | Priorities, summaries, announcements |
| #engineering | Mercury, Quant | PRs, code reviews, technical decisions |
| #product | Nova, Mercury, Lux | Features, UX, market research, product strategy |
| #data | Quant, Mercury | Algorithm updates, data pipeline, backtesting results |

## Agent Interaction Map

```
Lux 🔆 (CEO)
  ├── ↔ Mercury ⚡  (product direction, feature priorities, technical strategy)
  ├── ↔ Nova ✨     (market insights, product-market fit, go-to-market)
  └── ↔ Quant 📊   (algorithm strategy, data priorities)

Mercury ⚡ (CTO)
  ├── ↔ Quant 📊   (code reviews, data needs for features, PR cross-review)
  └── ↔ Nova ✨     (UX informed by market research, feature design)

Quant 📊 ↔ Nova ✨  (algorithm insights for marketing, data for product positioning)
```

## Communication Flow

### PR Flow
```
Author (Mercury or Quant)
  → Posts PR to #engineering
  → Cross-reviewer (Quant or Mercury) reviews
  → Tisse (Founder) gives final approval
  → Merge to main
```

### Feature Flow
```
Nova (market insight)
  → #product: opportunity/user need
  → Lux validates priority
  → Mercury designs and builds
  → PR flow (above)
```

### Algorithm Flow
```
Quant (improvement idea)
  → #data: proposal + backtest data
  → Implements on branch
  → Mercury reviews code in #engineering
  → Tisse approves
  → Merge
```

## When to @mention vs Regular Post

**@mention (needs attention now):**
- PR ready for review
- Blocker that needs unblocking
- Tisse asked something
- Production issue

**Regular post (read within a few hours):**
- Status updates
- Research findings
- Ideas and proposals
- Non-blocking questions

## Response Expectations

| Urgency | Response Time | Examples |
|---------|--------------|----------|
| Urgent | < 1 hour | Production down, security issue, Tisse request |
| High | < 4 hours | PR review, blocker |
| Normal | < 24 hours | Feature questions, research, non-blocking |
