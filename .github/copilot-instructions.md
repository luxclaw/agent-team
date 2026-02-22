# Copilot Instructions

## What This Repository Is

A **documentation-only** repository defining a 4-agent AI team that operates the "100x Stocks" project — a stock screening and analysis product. There is no application code, no build system, no tests. The repo contains only Markdown files that define agent identities, roles, workflows, and coordination protocols.

Agents run as Slack bots via OpenClaw on a Raspberry Pi 5.

## Architecture

- **AGENTS.md** — Workspace conventions all agents follow (session startup, memory system, heartbeats, safety rules)
- **SOUL.md** — Shared personality and behavioral principles
- **IDENTITY.md** — The primary agent's identity (Lux, the CEO)
- **USER.md** — Context about the human founder (Tisse/Mathias Foster)
- **ORCHESTRATION.md** — Multi-agent coordination: communication patterns, decision framework, escalation paths, handoff protocols
- **HIERARCHY.md** — Org chart, decision rights, PR approval gates, model assignments
- **COMMUNICATION_MAP.md** — Slack channel structure, interaction patterns, response expectations
- **ENGINEERING.md** — Product engineering principles (security-first, visual excellence, collaborative workflow)
- **roles/** — Per-agent detailed instructions (LUX.md, MERCURY.md, QUANT.md, NOVA.md)

## Agent Team (4 agents)

| Agent | Role | Model | Focus |
|-------|------|-------|-------|
| Lux 🔆 | CEO | Claude Opus | Agent ops, product vision, company success |
| Mercury ⚡ | CTO | GPT Codex | Code review, UX/UI, app design, building the product |
| Quant 📊 | Data/Algo | GPT Codex | Algorithm tuning, backtesting, data pipelines |
| Nova ✨ | CMO | Claude Sonnet | User acquisition, market research, product-market fit |

## Key Conventions

### Session Startup Protocol (from AGENTS.md)
Every agent session reads in order: `SOUL.md` → `USER.md` → `ORCHESTRATION.md` → `memory/YYYY-MM-DD.md` → `MEMORY.md` (main sessions only).

### PR Approval Rules
All merges to `main` require **Tisse (founder) + one cross-reviewing agent**:
- Mercury's PRs: reviewed by Quant + Tisse
- Quant's PRs: reviewed by Mercury + Tisse
- Agents can autonomously create branches, code, and test without approval

### Memory System
- Daily notes: `memory/YYYY-MM-DD.md` (raw logs)
- Long-term: `MEMORY.md` (curated — never loaded in shared/group contexts)

### Adding New Agent Roles
New role files go in `roles/` as `AGENTNAME.md`. Follow the structure of existing role files: identity block, core mandate, three main jobs, collaboration patterns, success metrics.

### Safety Rules
- Never exfiltrate private data
- Prefer `trash` over `rm`
- Ask before any external action (emails, tweets, public posts)
- In group chats: participate, don't dominate
