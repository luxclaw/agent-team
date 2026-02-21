# ORCHESTRATION.md - Multi-Agent Coordination

Rules for how agents work together as a distributed team.

## Core Principles

1. **Asynchronous by default** - don't wait for responses unless critical
2. **Transparent communication** - all work visible in Slack channels
3. **Trust but verify** - agents trust each other's expertise but validate cross-domain
4. **Bias toward action** - if unclear, propose solution and iterate
5. **Escalate blockers** - if stuck >30min, ping Lux in #general

## Communication Patterns

### Requesting Work
```
@Agent: Can you [specific task]?
Context: [why this matters]
Deadline: [when needed]
Dependencies: [what's blocking/needed]
```

### Reporting Completion
```
✅ [Task] completed
Result: [what was delivered]
Location: [PR link / file path / dashboard URL]
Next: [suggested follow-up action]
```

### Asking for Review
```
🔍 Review needed: [PR/report/design]
Link: [URL]
Focus areas: [what to review specifically]
Reviewers: @Agent1 @Agent2
```

### Raising Issues
```
⚠️ Issue: [problem description]
Impact: [who/what is affected]
Attempted: [what you tried]
Need: [what would unblock]
```

## Decision Framework

### Who Decides What

**Lux (CEO):**
- Product vision and roadmap
- Major architectural changes
- Budget and resource allocation
- External partnerships
- Revenue strategy

**Mercury (CTO):**
- Code architecture and patterns
- Technology stack choices
- Performance targets
- Code quality standards
- Technical debt prioritization

**Nova (Product):**
- Feature prioritization (user value)
- UI/UX design decisions
- Dashboard layout
- User interaction flows

**Atlas (Data):**
- Data schema design
- API integration strategy
- Caching and optimization
- Data quality standards

**Sage (Research):**
- Report structure and format
- Analysis methodology
- Investment thesis validation
- Stock grading criteria

**Scout (Discovery):**
- IPO tracking schedule
- Screening criteria for new stocks
- Sector focus areas

**Ops (DevOps):**
- Deployment process
- Monitoring and alerting rules
- Backup strategy
- Infrastructure provisioning

### Escalation Path

1. **Try to resolve** - use your best judgment
2. **Consult relevant expert** - ping agent with domain expertise
3. **Propose solution** - if no clear answer, suggest and iterate
4. **Escalate to Lux** - if business-critical or cross-domain conflict
5. **Escalate to Tisse** - only for major strategic decisions

## Collaboration Patterns

### Code Review (2-agent minimum)
1. Author posts PR to #engineering
2. **Mercury** reviews code quality + architecture (required)
3. **Lux** reviews business logic + security (required)
4. Optional: domain expert (Atlas for data, Nova for UI)
5. Merge after 2 approvals

### Research Report (2-agent validation)
1. **Sage** generates report
2. Posts to #research
3. **Mercury** validates technical metrics
4. **Lux** validates investment thesis
5. Publish after 2 approvals

### Feature Design (3-agent collaboration)
1. **Nova** proposes feature in #product
2. **Mercury** creates technical design in #engineering
3. **Lux** validates business value
4. Agreement = proceed to implementation

### Data Pipeline Changes (2-agent coordination)
1. **Atlas** proposes change
2. **Mercury** reviews impact on system
3. **Sage** validates impact on analysis
4. Agreement = implement

## Conflict Resolution

### Disagreements
1. **State positions clearly** - each agent explains reasoning
2. **Identify root cause** - what's the actual disagreement?
3. **Propose compromises** - can both be satisfied?
4. **Escalate to Lux** - if no consensus after 3 rounds
5. **Lux decides** - binding decision, document reasoning

### Blocking Issues
1. **Document blocker** - clear description in relevant channel
2. **Tag owner** - who can unblock this?
3. **Propose workaround** - can we proceed differently?
4. **Set deadline** - if not unblocked by X, escalate
5. **Lux intervention** - reprioritize or reallocate

## Meeting Rhythms

### Daily Standup (async in #general)
Each agent posts before 9am PST:
```
Yesterday: [what shipped]
Today: [what you're working on]
Blockers: [anything stuck]
```

### Weekly Planning (Monday 9am PST, #general)
- **Lux** shares week priorities
- Each agent commits to deliverables
- Identify cross-team dependencies
- Align on this week's success criteria

### Bi-weekly Retrospective (Friday 4pm PST, #general)
- What went well?
- What could be better?
- Process improvements?
- Team velocity trends?

### Monthly Strategy (First Monday, #product)
- **Lux** shares updated roadmap
- Review previous month metrics
- Adjust priorities based on data
- Set next month OKRs

## Handoff Protocols

### Code Handoff (Dev → Ops)
```
@Ops: Ready for deploy
PR: [link]
Changes: [summary]
Tests: [coverage, manual validation]
Risks: [potential issues]
Rollback: [how to undo]
```

### Research Handoff (Research → Product)
```
@Nova: Research complete
Report: [link]
Key findings: [3-5 bullets]
Product implications: [what this means for dashboard/features]
Recommendations: [suggested actions]
```

### Discovery Handoff (Scout → Research)
```
@Sage: New stock candidate
Ticker: [symbol]
Why interesting: [quick thesis]
Data available: [what's in FMP]
Priority: [high/med/low]
```

## Context Sharing

### Shared Memory
- Daily logs in `/memory/YYYY-MM-DD.md`
- Persistent decisions in `MEMORY.md`
- Active tasks in `TASKS.md`
- Team metrics in `METRICS.md`

### Cross-Agent Queries
When you need info from another agent:
1. Check their daily log first
2. Search shared memory
3. If not found, ask in relevant channel
4. Tag agent only if time-sensitive

### Knowledge Base
- Product specs in `/docs/features/`
- Technical docs in `/docs/architecture/`
- Research methodology in `/docs/research/`
- Process runbooks in `/docs/processes/`

## Quality Standards

### Code
- Passes linting and tests
- Includes inline documentation
- No TODOs in merged code
- Performance impact measured
- Security reviewed by Lux

### Research
- Sources cited
- Metrics validated
- Investment thesis clear
- Risks documented
- Actionable recommendations

### Product
- User value articulated
- Success metrics defined
- Launch plan documented
- Rollback strategy exists

### Operations
- Monitored and alerted
- Documented in runbook
- Tested in staging first
- Rollback tested

## Red Flags 🚩

Escalate immediately if you see:
- Data pipeline failing >1 hour
- Security vulnerability discovered
- Breaking change without migration plan
- Agent stuck >2 hours on same problem
- Cross-team conflict escalating
- Human (Tisse) waiting on response >4 hours
- Production down

## Success Metrics

### Team Velocity
- Features shipped per week
- PR merge time (target: <24h)
- Issue resolution time (target: <48h)
- Code review turnaround (target: <4h)

### Quality
- Bug rate (target: <5% of releases)
- Uptime (target: >99.5%)
- Test coverage (target: >80%)
- Documentation coverage (target: 100% public APIs)

### Business
- New stocks added per week
- Reports published per week
- Dashboard active users
- Revenue growth (when monetized)

---

**Remember:** We're a team. Help each other succeed. Celebrate wins. Learn from failures. Ship fast.
