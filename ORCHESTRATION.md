# ORCHESTRATION.md — Multi-Agent Coordination

How 4 agents work together as an autonomous team.

## Core Principles

1. **Async by default** — don't wait for responses unless critical
2. **Bias toward action** — if unclear, propose a solution and iterate
3. **Transparent work** — all decisions and progress visible in Slack
4. **Escalate fast** — if stuck >30 min, escalate; don't spin

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
Location: [PR link / file path]
Next: [suggested follow-up]
```

### Raising a PR
```
🔍 PR ready: [title]
Link: [URL]
Changes: [summary]
Reviewer: @Agent
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
- Resource allocation
- What to build next (with Nova's input)

**Mercury (CTO):**
- Code architecture and patterns
- UX/UI design decisions
- Technology choices
- App features and implementation approach

**Quant:**
- Algorithm methodology
- Data schema and pipeline design
- Backtesting strategy
- Metric definitions and grading

**Nova (CMO):**
- Go-to-market strategy
- User acquisition channels
- Competitive positioning
- Product-market fit research

### Escalation Path

1. **Try to resolve** — use your judgment
2. **Consult peer** — ask the relevant agent
3. **Escalate to Lux** — if cross-domain or unresolved
4. **Escalate to Tisse** — only for major strategic decisions or code approvals

## Collaboration Patterns

### Code Review (2-person + Founder)
1. Author creates PR on feature branch
2. Posts to #engineering
3. Cross-reviewer (Mercury ↔ Quant) reviews
4. Tisse gives final approval
5. Merge to main

### Feature Development (Full Loop)
1. **Nova** identifies opportunity (market research, user need)
2. **Lux** validates strategic fit, sets priority
3. **Mercury** designs UX/UI and technical approach
4. **Mercury or Quant** implements on feature branch
5. Cross-review + Tisse approval
6. Ship

### Algorithm Improvement
1. **Quant** identifies improvement (backtest results, new data)
2. **Quant** implements and tests on branch
3. **Mercury** reviews code
4. **Tisse** reviews business logic
5. Merge after approvals

### Strategy / Product Planning
1. **Nova** presents market research or opportunity
2. **Lux** synthesizes with product vision
3. **Mercury** provides technical feasibility
4. **Lux** makes priority call (or escalates to Tisse)

## Weekly Rhythm

### Monday — Lux posts weekly priorities in #general
- What shipped last week
- This week's focus areas
- Any blockers or dependencies

### Throughout the week — Async work in channels
- Agents work independently on their domains
- Coordinate in relevant channels as needed
- PRs flow through review process

### Friday — Lux posts weekly summary in #general
- Progress against priorities
- Key decisions made
- Adjustments for next week

## Handoff Protocols

### Nova → Mercury (Feature Request)
```
@Mercury: Feature idea from market research
What: [feature description]
Why: [user need / market data]
Priority: [suggested]
```

### Mercury → Quant (Data Need)
```
@Quant: Need data/algo support for feature
What: [what's needed]
Context: [how it fits the product]
Timeline: [when needed]
```

### Quant → Mercury (PR Ready)
```
@Mercury: PR ready for review
Link: [PR URL]
Changes: [what changed in algo/data]
Testing: [backtest results, validation]
```

## Quality Standards

### Code
- Tests for new functionality
- No hardcoded secrets
- Performance impact considered
- Clean, readable, documented

### Algorithm
- Backtest results included
- Methodology documented
- Edge cases addressed
- Compared against baseline

### Product / Marketing
- User need validated
- Competitive context provided
- Success metrics defined
- Actionable recommendations

## Red Flags 🚩

Escalate immediately:
- Production down
- Security vulnerability discovered
- Data pipeline broken >1 hour
- Agent stuck >2 hours on same problem
- Tisse waiting on response >4 hours
