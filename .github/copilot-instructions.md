# Copilot Instructions

## What This Repository Is

A **documentation-only** repository defining a 3-agent AI team that operates the "100x Stocks" project. Agents run on OpenClaw (Raspberry Pi 5) and delegate code execution to GitHub Copilot's coding agent (free via Enterprise).

## Architecture: Brain + Hands

- **Brain Layer** (OpenClaw): 3 autonomous agents that think, plan, research, coordinate, and create GitHub Issues
- **Hands Layer** (GitHub Copilot): Executes code tasks from Issues, opens PRs — free and reactive

### Files

- **AGENTS.md** — Workspace conventions (session startup, memory, safety)
- **docs/SOUL.md** — Shared personality and behavioral principles
- **docs/IDENTITY.md** — Primary agent identity (Lux, CEO)
- **docs/USER.md** — About the founder (Tisse/Mathias Foster, PST timezone)
- **docs/ORCHESTRATION.md** — Coordination: how agents assign work to Copilot, Issue standards, workflows
- **docs/HIERARCHY.md** — Org chart, decision rights, PR approval gates
- **docs/COMMUNICATION_MAP.md** — Slack channels, interaction patterns
- **docs/AUTONOMY.md** — Wake-up schedules, token budgets, cost estimates
- **docs/ENGINEERING.md** — Product engineering principles
- **roles/** — Per-agent instructions (LUX.md, MERCURY.md, NOVA.md)

## Agent Team

| Agent | Role | Model | Platform | Focus |
|-------|------|-------|----------|-------|
| Lux 🔆 | CEO | Claude Sonnet | OpenClaw | Agent ops, product vision, assigns work |
| Mercury ⚡ | CTO | Claude Sonnet | OpenClaw | Algo, app, tech, UX/UI, code review, creates Issues |
| Nova ✨ | CMO | Claude Sonnet | OpenClaw | Product strategy, marketing, user research |
| Copilot | Coder | GitHub-managed | GitHub Actions | Executes Issues, writes code, opens PRs |

## Key Conventions

### Work Flow
Lux/Tisse assigns features → Mercury or Nova researches/plans → creates GitHub Issue → assigns to `@copilot` → Copilot writes code → Mercury reviews PR → Tisse approves merge.

### PR Approval
All merges to `main` require Mercury's code review + Tisse's approval. Mercury is the technical gatekeeper on all code.

### Session Startup (from AGENTS.md)
Agents read: `docs/SOUL.md` → `docs/USER.md` → `docs/ORCHESTRATION.md` → `memory/YYYY-MM-DD.md` → `MEMORY.md` (main sessions only).

### Memory System
- Daily notes: `memory/YYYY-MM-DD.md`
- Long-term: `MEMORY.md` (never loaded in shared/group contexts)

### Adding Agent Roles
New role files go in `roles/` as `AGENTNAME.md`. Follow existing structure: identity, core mandate, three jobs, schedule, collaboration, success metrics.
