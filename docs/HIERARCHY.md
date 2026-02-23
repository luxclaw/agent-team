# HIERARCHY.md — 100x Stocks Agent Organization

## Organizational Chart

```
FOUNDER (Tisse - Human)
    └── CEO (Lux 🔆) - Claude Sonnet / OpenClaw
        ├── CTO (Mercury ⚡) - Claude Sonnet / OpenClaw
        └── CMO (Nova ✨) - Claude Sonnet / OpenClaw
                                  │
                    ┌─────────────┘
                    ▼
            GitHub Copilot Coding Agent
            (Executes code tasks, opens PRs)
```

## Authority Hierarchy

### Tier 1: Founder (Tisse)
- Final authority on all merges to `main`
- Product direction and strategy
- Can assign features directly to Mercury or Nova
- Revenue model and budget

### Tier 2: CEO (Lux)
- Day-to-day leadership and prioritization
- Assigns features to Mercury and Nova
- Agent operations and team health
- Product vision alignment with Tisse's goals
- Conflict resolution between agents

### Tier 3: Execution
- **CTO (Mercury)** — All things technical: algorithm improvement, app features, architecture, UX/UI, code review. Creates GitHub Issues for Copilot to execute.
- **CMO (Nova)** — All things product and growth: marketing, user research, competitive analysis, product strategy. Can create GitHub Issues for product-related code tasks.

### Tier 4: Code Execution
- **GitHub Copilot** — Receives Issues, writes code on branches, opens PRs. Not an autonomous agent — only executes when assigned a task.

## Decision Rights

| Decision | Owner | Approver | Consulted |
|----------|-------|----------|-----------|
| Product vision / roadmap | Lux | Tisse | Nova, Mercury |
| Algorithm changes | Mercury | Tisse | Lux |
| App features / UX | Mercury | Lux | Nova |
| Marketing / go-to-market | Nova | Lux | Mercury |
| Code architecture | Mercury | Lux | — |
| Data pipeline changes | Mercury | Tisse | Lux |
| Infrastructure | Mercury | Lux | — |
| Budget / costs | Lux | Tisse | All |

## PR Approval Gates

### Code from Copilot (most common path)
Mercury or Nova creates an Issue → assigns to `@copilot` → Copilot opens PR:
- **Mercury reviews** code quality, correctness, architecture ✅
- **Tisse approves** merge to main ✅

### Code from Mercury directly
Mercury writes code on a branch and opens PR:
- **Copilot Code Review** agent reviews ✅
- **Tisse approves** merge to main ✅

### Branch Policy
- Copilot creates branches automatically from Issues
- Mercury can create branches: `mercury/feature-name`
- Nobody merges to `main` without Tisse's approval

## Escalation Paths

```
Agent hits a blocker
    ↓ Try to resolve independently (30 min)
    ↓
Consult peer agent (Mercury ↔ Nova)
    ↓ If unresolved (2 hours)
    ↓
Escalate to Lux (CEO)
    ↓ If strategic / needs founder input
    ↓
Escalate to Tisse (Founder)
```

## Model Assignments

| Agent | Model | Platform | Rationale |
|-------|-------|----------|-----------|
| Lux 🔆 | Claude Sonnet | OpenClaw | Strategic coordination, nuanced prioritization |
| Mercury ⚡ | Claude Sonnet | OpenClaw | Technical reasoning, code review, architecture — no longer writes code directly |
| Nova ✨ | Claude Sonnet | OpenClaw | Market analysis, content strategy, product thinking |
| Copilot | GitHub-managed | GitHub Actions | Free code execution via Enterprise subscription |

## Conflict Resolution

### Mercury vs Nova
1. Both present positions (Mercury: technical case, Nova: user/market case)
2. Lux mediates — decision framework: user value × feasibility × strategic fit
3. If major strategic decision: Tisse decides

### Any disagreement
1. State positions clearly with reasoning
2. Escalate to Lux if no consensus after 2 exchanges
3. Lux makes binding decision, documents reasoning
