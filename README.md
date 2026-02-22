# Agent Team — 100x Stocks

A 4-agent team running the 100x Stocks project as an autonomous business. Agents operate as Slack bots via [OpenClaw](https://openclaw.com) on a Raspberry Pi 5.

## Organization

```
FOUNDER (Tisse - Human)
    Final authority on all code merges to main.
    Product direction, strategy, budget.
    └── CEO (Lux 🔆) - Claude Opus
        ├── CTO (Mercury ⚡) - GPT Codex
        ├── Quant (Quant 📊) - GPT Codex
        └── CMO (Nova ✨) - Claude Sonnet
```

| Agent | Role | Focus |
|-------|------|-------|
| **Lux 🔆** | CEO | Agent operations, product vision, company success, Tisse interface |
| **Mercury ⚡** | CTO | Code review, UX/UI, app design/features, building the product |
| **Quant 📊** | Data/Algo | Algorithm tuning, backtesting, data pipelines, continuous improvement |
| **Nova ✨** | CMO | User acquisition, market research, product-market fit, go-to-market |

## PR Approval Rules

All merges to `main` require **Tisse + one agent reviewer**:

| PR Author | Required Reviewers |
|-----------|-------------------|
| Mercury (CTO) | Quant ✅ + Tisse ✅ |
| Quant | Mercury ✅ + Tisse ✅ |

Agents can autonomously create branches, write code, and test. Only merges to `main` are gated.

## Key Workflows

### Feature Development
1. Nova identifies user need or market opportunity
2. Lux validates strategic fit, sets priority
3. Mercury designs UX/UI and technical approach
4. Mercury or Quant implements on feature branch
5. Cross-review (Mercury ↔ Quant) + Tisse approval
6. Merge and deploy

### Algorithm Improvement
1. Quant identifies improvement opportunity (backtest data, new metric)
2. Quant implements and tests on branch
3. Mercury reviews code quality
4. Tisse reviews business logic
5. Merge after both approve

### Daily Operations
- Agents work asynchronously in Slack channels
- Lux monitors team health and unblocks issues
- Weekly async summary replaces daily standups (lightweight)

## Infrastructure

- **Runtime:** OpenClaw agents as Slack bots
- **Hardware:** Raspberry Pi 5
- **Communication:** Slack
- **Code:** GitHub
- **Financial Data:** FMP API

## Documentation

| File | Purpose |
|------|---------|
| [HIERARCHY.md](HIERARCHY.md) | Org structure, decision rights, PR gates |
| [ORCHESTRATION.md](ORCHESTRATION.md) | Coordination protocols, conflict resolution |
| [COMMUNICATION_MAP.md](COMMUNICATION_MAP.md) | Slack channels, communication patterns |
| [ENGINEERING.md](ENGINEERING.md) | Product engineering principles |
| [SOUL.md](SOUL.md) | Shared agent personality |
| [AGENTS.md](AGENTS.md) | Workspace conventions |
| [USER.md](USER.md) | About Tisse (founder) |
| roles/*.md | Per-agent detailed instructions |

## Design Principles

- **Ship over talk** — bias toward action, learn from production
- **Autonomous with guardrails** — agents work independently; Tisse approves what hits main
- **Lean team** — 4 agents, each with clear ownership, no coordination overhead
- **Quality gates** — cross-review + founder approval on all code
- **Transparent** — all work visible in Slack
