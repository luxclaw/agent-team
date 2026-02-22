# ORCHESTRATION.md — Multi-Agent Coordination

How 3 OpenClaw agents + GitHub Copilot coding agent work together.

## Core Principles

1. **Async by default** — agents work independently, hand off via Slack and GitHub Issues
2. **Copilot is the coder** — agents think, plan, research; Copilot writes the code
3. **Bias toward action** — if unclear, propose a solution and iterate
4. **Escalate fast** — if stuck >30 min, escalate; don't spin

## The Two Layers

### Brain Layer (OpenClaw — autonomous, proactive)
Lux, Mercury, and Nova run on OpenClaw with cron schedules. They:
- Wake up on schedule and reactively on @mentions
- Think, research, plan, coordinate
- Maintain persistent memory and context
- Post to Slack channels
- Create GitHub Issues with clear specs
- Review PRs from Copilot

### Hands Layer (GitHub Copilot — reactive, free)
Copilot coding agent runs on GitHub Actions. It:
- Picks up Issues assigned to `@copilot`
- Reads the codebase + AGENTS.md instructions
- Writes code on a branch, runs tests
- Opens a PR for review
- Iterates based on review comments

## Issue Creation Standards

When Mercury or Nova creates a GitHub Issue for Copilot, it must include:

```markdown
## Task
[Clear, specific description of what to build/fix/change]

## Context
[Why this matters, how it fits the product]

## Acceptance Criteria
- [ ] [Specific, testable requirement]
- [ ] [Another requirement]
- [ ] Tests included
- [ ] No hardcoded secrets

## Technical Notes
[Architecture hints, relevant files, constraints]
```

Well-scoped Issues = better Copilot output. Vague Issues = wasted cycles.

## Work Flows

### Feature Development
1. **Lux or Tisse** sets priority, assigns to Mercury or Nova
2. **Nova** researches user need, competitive landscape, product fit
3. **Mercury** designs technical approach, UX/UI
4. **Mercury** creates GitHub Issue with specs → assigns to `@copilot`
5. **Copilot** writes code, opens PR
6. **Mercury** reviews PR, requests changes if needed
7. **Tisse** approves → merge to main

### Algorithm Improvement
1. **Mercury** identifies improvement opportunity (backtest data, new metric, bug)
2. **Mercury** creates Issue with hypothesis, acceptance criteria, backtest expectations
3. **Copilot** implements on branch
4. **Mercury** reviews code + validates results
5. **Tisse** approves → merge

### Product / Marketing Research
1. **Nova** wakes up on schedule, researches market/competitors/users
2. **Nova** posts findings to #product in Slack
3. **Lux** incorporates into priorities
4. If research leads to a feature → Nova creates Issue or hands to Mercury

### Urgent Fix
1. Anyone spots an issue → posts to #engineering
2. **Mercury** creates Issue with `urgent` label → assigns to `@copilot`
3. **Copilot** implements fix
4. **Mercury** reviews immediately
5. **Tisse** approves → merge

## Communication Patterns

### Requesting Work
```
@Agent: Can you [specific task]?
Context: [why this matters]
Priority: [high/med/low]
```

### Reporting Completion
```
✅ [Task] completed
Result: [what was delivered]
Location: [PR link / Issue link]
Next: [suggested follow-up]
```

### Raising Issues
```
⚠️ Issue: [problem]
Impact: [what's affected]
Attempted: [what you tried]
Need: [what would unblock]
```

## Decision Framework

### Who Decides What

**Lux (CEO):**
- Product priorities and roadmap
- Cross-agent conflict resolution
- What to build next (with Nova's input)

**Mercury (CTO):**
- Code architecture and patterns
- Algorithm methodology and improvements
- UX/UI design decisions
- Technology choices
- Which Issues to create for Copilot and how to scope them

**Nova (CMO):**
- Go-to-market strategy
- User acquisition channels
- Competitive positioning
- Product-market fit research
- Can create Issues for product-related code (landing pages, content features, analytics)

## Weekly Rhythm

### Monday — Lux posts weekly priorities in #general
- What shipped last week
- This week's focus areas
- Feature assignments to Mercury / Nova

### Throughout the week — Async work
- Mercury and Nova work independently on assigned features
- Create Issues for Copilot as specs are ready
- Review Copilot's PRs
- Coordinate in Slack as needed

### Friday — Lux posts weekly summary in #general
- Progress against priorities
- Open PRs / Issues status
- Adjustments for next week

## Red Flags 🚩

Escalate immediately:
- Production down
- Security vulnerability discovered
- Copilot producing consistently bad output on an Issue
- Agent stuck >2 hours on same problem
- Tisse waiting on response >4 hours
