# ORCHESTRATION.md — Multi-Agent Coordination

How 3 OpenClaw agents + GitHub Copilot keep the pipeline full.

## Core Principles

1. **Pipeline always flowing** — 3-5 Issues in Copilot's queue at all times
2. **Tisse reviews, not debugs** — PRs labeled `ready-for-tisse` are polished and Mercury-approved
3. **Parallel work streams** — multiple features progressing simultaneously
4. **Bias toward action** — if unclear, propose a solution and iterate
5. **Escalate fast** — if stuck >30 min, escalate; don't spin

## The Pipeline

```
BACKLOG → SPRINT → IN PROGRESS → IN REVIEW → READY FOR TISSE → DONE
```

Work flows left to right. Multiple items at each stage simultaneously. The system never stalls waiting for one person.

### GitHub Projects Board

We use a **GitHub Projects** Kanban board on `mfoster58/100x-stocks` as the single source of truth for all work.

**Columns:**

| Column | What's Here | Who Manages |
|--------|-------------|-------------|
| Backlog | Ideas, research findings, unscoped work | Nova adds, Lux prioritizes |
| Sprint | Scoped Issues for current week | Lux assigns weekly, Mercury scopes |
| In Progress | Copilot actively coding | Auto-moves when assigned to `@copilot` |
| In Review | PR open, Mercury reviewing | Mercury moves after review |
| Ready for Tisse | Mercury approved, awaiting final sign-off | Mercury moves after approval |
| Done | Merged to main | Auto-moves on PR merge |

**Custom Fields:**

| Field | Type | Values |
|-------|------|--------|
| Sprint | Iteration | Weekly (Mon-Sun) |
| Stream | Select | `Algorithm`, `App`, `Data Pipeline`, `Product/Marketing` |
| Priority | Select | `P0 (Critical)`, `P1 (High)`, `P2 (Medium)`, `P3 (Low)` |
| Effort | Select | `S (hours)`, `M (1-2 days)`, `L (3+ days)` |

**Built-in Automations:**
- Issue created → add to Backlog
- PR linked to Issue → move to In Progress
- PR merged → move to Done
- Issue closed → move to Done

**Who adds to the board:**
- **Tisse:** Add features directly — create an Issue or card, Lux picks it up
- **Lux:** Prioritizes backlog, creates sprint iterations, moves items to Sprint
- **Mercury:** Scopes Issues, assigns to Copilot, moves through review columns
- **Nova:** Adds research-backed feature ideas to Backlog

### Issue Labels

Labels complement the board (used for filtering, not column tracking):

| Label | Meaning |
|-------|---------|
| `algorithm` | Engine Power, metrics, backtesting |
| `app` | Dashboard, UX, endpoints |
| `data-pipeline` | FMP integration, refresh, caching |
| `product` | Marketing pages, content, analytics |
| `bugfix` | Bug fix |
| `refactor` | Code cleanup |
| `urgent` | Skip the queue, immediate attention |

## Issue Creation Standards

When Mercury or Nova creates a GitHub Issue for Copilot:

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

**Scope small:** 2-3 hour tasks. Break big features into multiple chained Issues.

## Work Flows

### Feature Development (Full Pipeline)
1. **Nova** identifies user need through daily research → posts to #product
2. **Lux** validates strategic fit during daily check-in → assigns to Mercury
3. **Mercury** designs technical approach during deep work session
4. **Mercury** creates 1-3 Issues (breaking feature into parts) → assigns to `@copilot`
5. **Copilot** writes code on branch, opens PR
6. **Mercury** reviews during morning/afternoon review → approves or requests changes
7. **Copilot** iterates on feedback if needed
8. **Mercury** approves, labels `ready-for-tisse` → posts summary to #engineering
9. **Tisse** reviews batch of PRs when checking in → approves → merge

### Algorithm Improvement
1. **Mercury** identifies improvement during deep work (backtest data, new metric, bug)
2. **Mercury** creates Issue with hypothesis, acceptance criteria, expected results
3. **Copilot** implements on branch, opens PR
4. **Mercury** reviews code + validates results
5. Label `ready-for-tisse` → Tisse approves → merge

### Product-Related Code (Nova-Initiated)
1. **Nova** identifies need for product code (landing page, analytics, content feature)
2. **Nova** creates Issue with user context and acceptance criteria
3. **Copilot** implements, opens PR
4. **Mercury** reviews for code quality
5. Label `ready-for-tisse` → Tisse approves → merge

### Continuous Research (Nova)
1. **Nova** wakes daily with rotating research focus (competitors, users, content, PMF, growth)
2. Posts findings to #product
3. Twice weekly: deep dives on priority topics
4. Weekly: synthesis of findings into actionable recommendations
5. Recommendations feed into Lux's weekly planning → Mercury's Issue backlog

### Urgent Fix
1. Anyone spots issue → posts to #engineering
2. **Mercury** creates Issue with `urgent` label → assigns to `@copilot`
3. **Copilot** implements fix, opens PR
4. **Mercury** reviews immediately
5. Label `ready-for-tisse` → Tisse approves → merge

## Mercury's Review Loop

Mercury doesn't just approve/reject — he iterates with Copilot:

1. **Copilot opens PR** → Mercury reviews during next scheduled wake-up
2. **If good:** Move card to Ready for Tisse, post summary to #engineering
3. **If needs work:** Request specific changes in PR comments → Copilot iterates → Mercury re-reviews next session
4. **If fundamentally wrong:** Close PR, rewrite Issue, re-assign to Copilot

**Goal:** PRs labeled `ready-for-tisse` are high quality. Tisse's review is a final sanity check, not a debugging session.

## Parallel Work Streams

Mercury maintains Issues across multiple streams simultaneously:

```
Stream 1: Algorithm (Engine Power improvements, new metrics, backtesting)
Stream 2: App features (dashboard, UX, endpoints, visualizations)
Stream 3: Data pipeline (refresh automation, quality, caching)
Stream 4: Bug fixes / maintenance (as needed)
```

At any given time, there should be:
- 3-5 Issues assigned to Copilot (in progress)
- 1-3 PRs in Mercury review
- 1-3 PRs labeled `ready-for-tisse`

## When Tisse Checks In

Tisse should find a clear, actionable queue:

1. **#general** — Lux's latest update with pipeline status
2. **GitHub PRs** — Filter by `ready-for-tisse` label
3. **#engineering** — Mercury's summary of what each PR does and why

Approve in batch, merge, move on. The team keeps shipping while you're away.

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

### Pipeline Status (Lux posts daily)
```
📊 Sprint [N] Status
Ready for Tisse: [PR #X, PR #Y]
In Review: [PR #Z]
In Progress: [Issue #A, Issue #B]
Sprint Backlog: [N items remaining]
Backlog: [N total items]
Velocity: [N merged this week]
```

## Decision Framework

### Who Decides What

**Lux (CEO):**
- Product priorities and roadmap
- Cross-agent conflict resolution
- What to build next (with Nova's input)
- Pipeline health and velocity

**Mercury (CTO):**
- Code architecture and patterns
- Algorithm methodology and improvements
- UX/UI design decisions
- Issue scoping and Copilot delegation
- PR approval (before Tisse's final review)

**Nova (CMO):**
- Go-to-market strategy
- User acquisition channels
- Competitive positioning
- Product-market fit research
- Product-related Issue creation

## Daily Rhythm

```
8am   Mercury: Review overnight Copilot PRs
9am   Lux: Daily check-in, pipeline status, unblock
9am   Nova: Daily research (rotating topic)
11am  Mercury: Create new Issues, deep technical work
2pm   Nova (Tue/Thu): Deep research dive
3pm   Mercury: Afternoon PR review, follow-up
7pm   Mercury: Evening pipeline check, queue tomorrow
```

Weekend: Mercury light check Saturday. Lux preps Monday priorities Sunday evening.

## Red Flags 🚩

Escalate immediately:
- Production down
- Security vulnerability discovered
- Issue queue empty (pipeline stalled)
- >3 PRs sitting in `ready-for-tisse` for >48 hours (Tisse bottleneck — ping them)
- Copilot failing repeatedly on same Issue type
- Agent stuck >2 hours on same problem

## Cross-Repo Workflow

Agents are configured in `luxclaw/agent-team` but build in `mfoster58/100x-stocks`.

```
agent-team (OpenClaw reads)          100x-stocks (Copilot works)
├── roles/*.md (who agents are)      ├── src/ (Python screener)
├── ORCHESTRATION.md (how to work)   ├── public/ (dashboard)
├── AUTONOMY.md (when to work)       ├── server.js (Node API)
└── HIERARCHY.md (who decides)       └── .github/copilot-instructions.md
```

**Mercury/Nova create Issues via GitHub API** in `mfoster58/100x-stocks`, assigning to `@copilot`. Copilot reads `100x-stocks/.github/copilot-instructions.md` for codebase context.

### What Lives Where

| Content | Repo |
|---------|------|
| Agent identities & roles | `agent-team` |
| Coordination protocols | `agent-team` |
| Wake-up schedules | `agent-team` |
| Product source code | `100x-stocks` |
| Copilot coding instructions | `100x-stocks` |
| GitHub Issues & PRs | `100x-stocks` |
| FMP MCP config | `100x-stocks` |

### FMP API Access

- **MCP server** configured in `100x-stocks/.vscode/mcp.json` (for VS Code sessions)
- **API reference** at `100x-stocks/docs/FMP_API_REFERENCE.md` (Mercury references when creating algo Issues)
- **API key** in `100x-stocks/.env` (never committed; used by Python scripts at runtime)
- **Copilot in CI** needs `FMP_API_KEY` as a GitHub Actions secret to call FMP live (see [SETUP.md](../SETUP.md))
