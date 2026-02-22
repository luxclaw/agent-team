# Agent Team — 100x Stocks

A 3-agent team running the 100x Stocks project as an autonomous business. Agents run on OpenClaw (Raspberry Pi 5) and delegate code execution to GitHub Copilot's coding agent.

## Organization

```
FOUNDER (Tisse - Human)
    Final authority on all merges to main.
    Product direction, strategy, budget.
    Can assign features directly to Mercury or Nova.
    └── CEO (Lux 🔆) - Claude Sonnet / OpenClaw
        ├── CTO (Mercury ⚡) - Claude Sonnet / OpenClaw
        └── CMO (Nova ✨) - Claude Sonnet / OpenClaw
                                  │
                    ┌─────────────┘
                    ▼
            GitHub Copilot Coding Agent
            (Free execution layer — writes code, opens PRs)
```

| Agent | Role | Model | Runs On | Focus |
|-------|------|-------|---------|-------|
| **Lux 🔆** | CEO | Claude Sonnet | OpenClaw | Agent ops, product vision, company success, assigns work |
| **Mercury ⚡** | CTO | Claude Sonnet | OpenClaw | Algo, app features, tech architecture, UX/UI, code review |
| **Nova ✨** | CMO | Claude Sonnet | OpenClaw | Product strategy, marketing, user research, go-to-market |
| **Copilot** | Coder | GitHub-managed | GitHub Actions | Executes code tasks from Issues, opens PRs |

## How Work Flows

1. **Lux or Tisse** assigns a feature/priority to Mercury or Nova
2. **Mercury or Nova** does research, planning, and design (on OpenClaw)
3. **Mercury or Nova** creates a GitHub Issue with clear specs and assigns to `@copilot`
4. **Copilot coding agent** writes code on a branch, runs tests, opens a PR
5. **Mercury** reviews the PR for code quality and correctness
6. **Tisse** gives final approval → merge to main

## PR Approval Rules

All merges to `main` require **Tisse + agent review**:

| PR Author | Reviewer | Founder |
|-----------|----------|---------|
| Copilot (assigned by Mercury) | Mercury ✅ | Tisse ✅ |
| Copilot (assigned by Nova) | Mercury ✅ | Tisse ✅ |
| Mercury (direct code) | Copilot Code Review ✅ | Tisse ✅ |

Mercury is the technical gatekeeper on all code. Tisse has final say on all merges.

## Infrastructure

- **Agent Runtime:** OpenClaw on Raspberry Pi 5
- **Code Execution:** GitHub Copilot coding agent (free via Enterprise)
- **Code Review:** GitHub Copilot code review agent (free via Enterprise)
- **Project Board:** GitHub Projects (Kanban — Lux manages sprints)
- **Communication:** Slack
- **Code:** GitHub
- **Financial Data:** FMP API

## Repos

| Repo | Purpose |
|------|---------|
| `luxclaw/agent-team` (this repo) | Agent identities, roles, coordination protocols — OpenClaw reads this |
| `mfoster58/100x-stocks` | Product code (Python + Node.js) — Copilot writes code here |

Agents are **configured** in `agent-team`, but **work** in `100x-stocks`.

## Documentation

| File | Purpose |
|------|---------|
| [SETUP.md](SETUP.md) | **Start here** — step-by-step launch guide |
| [HIERARCHY.md](HIERARCHY.md) | Org structure, decision rights, PR gates |
| [ORCHESTRATION.md](ORCHESTRATION.md) | Coordination protocols, issue creation workflow |
| [COMMUNICATION_MAP.md](COMMUNICATION_MAP.md) | Slack channels, communication patterns |
| [AUTONOMY.md](AUTONOMY.md) | Wake-up schedules, token budgets, cost estimates |
| [ENGINEERING.md](ENGINEERING.md) | Product engineering principles |
| [SOUL.md](SOUL.md) | Shared agent personality |
| [AGENTS.md](AGENTS.md) | Workspace conventions |
| [USER.md](USER.md) | About Tisse (founder) |
| roles/*.md | Per-agent detailed instructions |
