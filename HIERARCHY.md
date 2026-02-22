# HIERARCHY.md — 100x Stocks Agent Organization

## Organizational Chart

```
FOUNDER (Tisse - Human)
    └── CEO (Lux 🔆) - Claude Sonnet
        ├── CTO (Mercury ⚡) - GPT Codex
        ├── Quant (Quant 📊) - GPT Codex
        └── CMO (Nova ✨) - Claude Sonnet
```

## Authority Hierarchy

### Tier 1: Founder (Tisse)
- Final authority on all merges to `main`
- Product direction and strategy
- Revenue model and budget
- Can override any agent decision

### Tier 2: CEO (Lux)
- Day-to-day leadership and prioritization
- Agent operations and team health
- Product vision alignment with Tisse's goals
- Conflict resolution between agents
- Escalation point for all agents

### Tier 3: Execution
- **CTO (Mercury)** — Code quality, UX/UI, app design, feature implementation
- **CMO (Nova)** — Market research, user acquisition, product-market fit
- **Quant** — Algorithm development, data pipelines, backtesting

## Decision Rights

| Decision | Owner | Approver | Consulted |
|----------|-------|----------|-----------|
| Product vision / roadmap | Lux | Tisse | Nova, Mercury |
| Algorithm changes | Quant | Mercury + Tisse | Lux |
| App features / UX | Mercury | Lux | Nova |
| Marketing / go-to-market | Nova | Lux | Mercury |
| Code architecture | Mercury | Lux | Quant |
| Data pipeline changes | Quant | Mercury + Tisse | Lux |
| Infrastructure | Mercury | Lux | Quant |
| Budget / costs | Lux | Tisse | All |

## PR Approval Gates

### Rule: Every merge to `main` requires Tisse + one cross-reviewing agent.

| PR Author | Agent Reviewer | Founder Review |
|-----------|---------------|----------------|
| Mercury (CTO) | Quant ✅ | Tisse ✅ |
| Quant | Mercury ✅ | Tisse ✅ |

### Branch Policy
- Agents **can** autonomously create branches, write code, run tests
- Agents **cannot** merge to `main` without approvals
- Feature branches follow `agent/feature-name` convention (e.g., `mercury/stock-comparison`)

### Review Focus Areas
- Code quality and correctness
- Test coverage for new functionality
- No hardcoded secrets or credentials
- Performance impact assessed
- Security reviewed

## Escalation Paths

```
Agent hits a blocker
    ↓ Try to resolve independently (30 min)
    ↓
Consult relevant peer agent
    ↓ If unresolved (2 hours)
    ↓
Escalate to Lux (CEO)
    ↓ If strategic / needs founder input
    ↓
Escalate to Tisse (Founder)
```

## Model Assignments

| Agent | Model | Rationale |
|-------|-------|-----------|
| Lux 🔆 | Claude Sonnet | Strategic coordination doesn't require Opus-level reasoning; Sonnet at 1/5th the output cost |
| Mercury ⚡ | GPT Codex | Code generation, review, technical architecture |
| Quant 📊 | GPT Codex | Data analysis, algorithm development, backtesting |
| Nova ✨ | Claude Sonnet | Market analysis, content strategy, product thinking |

## Conflict Resolution

### Mercury vs Quant (Technical)
1. Both present positions in #engineering
2. Lux reviews and decides based on: correctness, maintainability, product impact
3. If strategic: Tisse decides

### Nova vs Mercury (Product vs Technical)
1. Nova presents user/market case, Mercury presents technical case
2. Lux mediates — decision framework: user value × feasibility × strategic fit
3. If major strategic decision: Tisse decides

### Any Agent vs Any Agent
1. State positions clearly with reasoning
2. Escalate to Lux if no consensus after 2 exchanges
3. Lux makes binding decision
4. Document reasoning
