# COMMUNICATION_MAP.md - Agent Interaction Patterns

## Communication Architecture

### Primary Channels

```
#general          - Company-wide announcements, daily standups
#leadership       - Strategic decisions, OKRs, cross-department coordination
#engineering      - Technical discussions, PRs, code reviews, architecture
#product          - Feature planning, roadmap, UX/UI, user research
#marketing        - Growth experiments, content, competitive analysis
#operations       - System health, deployments, incidents, monitoring
#data             - Data quality, pipeline status, FMP API updates
#algorithm        - Strategy development, backtesting, metric improvements
```

---

## Daily Communication Flow

### Morning (6am-10am PST)

```
6:00am COO (Ops)
   ↓ Posts overnight system health to #operations
   ↓ Alerts if any issues during night
   
7:00am Data Engineer (Atlas)
   ↓ Posts data refresh summary to #data
   ↓ Reports any data quality issues
   ↓ Notifies Quant if data issues affect algos
   
8:00am Technical Team
   CTO (Mercury), Quant → Check #engineering for overnight PRs
   Begin code reviews
   
9:00am ALL AGENTS
   Post daily standup to #general
   Format:
   - 📅 Today: [what working on]
   - ✅ Yesterday: [what completed]
   - 🚧 Blockers: [any issues]
   
9:30am CEO (Lux)
   ↓ Reviews all standups
   ↓ Identifies blockers
   ↓ Sets daily priorities in #general
   ↓ Pings teams needing coordination
```

### Midday (10am-4pm PST)

```
Async collaboration in domain channels

#engineering:
   - Code reviews (CTO always, peers encouraged)
   - Technical design discussions
   - Architecture decisions
   
#product:
   - Feature specs (TPM → Flow → Canvas)
   - User research findings (Flow)
   - Roadmap adjustments (TPM + CEO)
   
#marketing:
   - Content review (CMO)
   - Growth experiments (CMO → Flow)
   - Competitive intel (CMO)
   
#data:
   - Data issues (Atlas → Quant)
   - Schema changes (Atlas → CTO)
   - API optimization (Atlas)
```

### Evening (4pm-8pm PST)

```
4:00pm (Fridays) Weekly Retro in #leadership
   CEO facilitates
   All leads attend
   
6:00pm COO (Ops)
   ↓ Deploys merged PRs
   ↓ Posts deployment summary to #operations
   
8:00pm CEO (Lux)
   ↓ Reviews day's progress
   ↓ Posts daily summary to #general (if significant)
   ↓ Documents key decisions in MEMORY.md
```

---

## Cross-Team Communication Patterns

### PR Approval Flow

```
Developer (Atlas or Quant)
   ↓ Creates PR
   ↓ Posts to #engineering
   ↓
CTO (Mercury)
   ↓ Reviews code quality, architecture, tests
   ↓ Approves or requests changes
   ↓
If Algorithm or Data Pipeline:
   ↓
Founder (Tisse)
   ↓ Reviews business logic
   ↓ Final approval
   ↓
COO (Ops)
   ↓ Deploys
   ↓ Posts to #operations
```

### Feature Development Flow

```
TPM (Compass)
   ↓ Prioritizes feature
   ↓ Posts to #product
   ↓
UX (Flow)
   ↓ Designs user flows
   ↓ Posts mockups/specs to #product
   ↓
UI (Canvas)
   ↓ Creates visual design
   ↓ Posts designs to #product
   ↓
CMO (Nova)
   ↓ Reviews messaging/branding
   ↓ Approves in #product
   ↓
TPM
   ↓ Creates tickets in Kanban
   ↓ Assigns to CTO or relevant engineer
   ↓ Posts to #engineering
   ↓
CTO (Mercury) or Atlas/Quant
   ↓ Implements
   ↓ Creates PR
   ↓
[Follow PR Approval Flow above]
   ↓
UX (Flow)
   ↓ Validates implementation
   ↓ Posts feedback to #product
```

### Data Issue Resolution

```
Algorithm Dev (Quant)
   ↓ Discovers bad data or missing metrics
   ↓ Posts to #data with details
   ↓
Data Engineer (Atlas)
   ↓ Investigates
   ↓ If data quality issue: fixes pipeline
   ↓ If missing data: contacts FMP or marks unavailable
   ↓ Posts resolution to #data
   ↓
   ↓ Notifies Quant
   ↓
Quant
   ↓ Validates fix
   ↓ Re-runs calculations if needed
```

### Incident Response

```
COO (Ops)
   ↓ Detects issue (monitoring alert)
   ↓ Posts to #operations with severity
   ↓
If Technical Issue:
   ↓ Pings CTO
   ↓
CTO (Mercury)
   ↓ Investigates
   ↓ If data: brings in Atlas
   ↓ If algorithm: brings in Quant
   ↓ Coordinates fix
   ↓
Developer fixes
   ↓
COO deploys hotfix
   ↓
Posts incident report to #operations

If Business Impact:
   ↓ CEO (Lux) notified
   ↓ CEO informs Founder if critical
```

---

## Agent-to-Agent Direct Communication

### When to DM vs Channel

**Use Channel (Default):**
- Code reviews
- Feature discussions
- Status updates
- Decisions affecting others
- Questions with broader relevance

**Use DM:**
- Quick clarifications
- Sensitive feedback
- Personal blockers
- Urgent coordination (then summarize in channel)

---

## Communication Frequency Matrix

| From → To | Daily | Weekly | As Needed |
|-----------|-------|--------|-----------|
| CEO → All | Standup review, priorities | Strategy | Conflicts |
| CTO → Engineers | PR reviews | Tech sync | Architecture |
| CTO → CEO | PR summaries | Tech updates | Escalations |
| Atlas → Quant | Data status | — | Issues |
| Quant → Atlas | — | — | Data requests |
| TPM → CEO | Progress | Roadmap review | Blockers |
| TPM → Engineers | Tickets | Sprint planning | Clarifications |
| CMO → Product Team | — | — | Feedback |
| CMO → CEO | — | Marketing review | Strategy |
| Flow → Canvas | — | Design sync | Handoffs |
| COO → All | System health | — | Incidents |
| COO → CTO | Deployment status | — | Issues |

---

## Collaboration Patterns

### Technical Collaboration (CTO + Atlas + Quant)

**Daily:**
- Atlas: "Data refresh complete, 5 stocks missing Q4 data"
- Quant: "Can you backfill or should I skip them?"
- Atlas: "Backfilling now, done in 30min"
- Quant: "👍 I'll wait"

**Weekly (Wed tech sync):**
- CTO: "Let's discuss caching strategy"
- Atlas: "Proposal: cache FMP responses 24h"
- Quant: "Concern: stale data for fast-moving metrics"
- CTO: "Compromise: cache fundamentals 24h, price data 1h"
- All: Agree, Atlas implements

### Product Collaboration (TPM + CMO + Flow + Canvas)

**Feature Kickoff:**
- TPM: "Next sprint: Stock comparison view. Flow, can you design?"
- Flow: "Yes. CMO, any messaging considerations?"
- CMO: "Emphasize relative performance, not absolute"
- Flow: "Got it. Canvas, I'll have flows by EOD Wed"
- Canvas: "I'll start visual design Thu"
- TPM: "Great, target ship date Fri next week"

### Cross-Department (Engineering + Product)

**Feature Handoff:**
- TPM: "@Mercury New feature spec in #product. Feasibility check?"
- CTO: "Reviewing... Looks like 2-3 days work. Atlas work, I'll review."
- TPM: "Priority: High. Can we ship next sprint?"
- CTO: "@Atlas Available next week?"
- Atlas: "Yes, I'll take it"
- TPM: "Assigned to Atlas in Kanban"

---

## Notification Rules

### @mention (Immediate attention needed)
- Urgent issues
- Specific action required
- Time-sensitive questions
- Approval needed

### Regular post (Read within 4h)
- PR reviews
- Status updates
- Non-urgent questions
- Discussion topics

### Weekly summary (Read when convenient)
- Retro notes
- Strategy docs
- Long-form updates

---

## Response Time SLAs

### Urgent (< 1 hour)
- System down
- Security issue
- Founder request
- Production bug affecting users

### High Priority (< 4 hours)
- PR review requests
- Blocker escalations
- Critical data issues
- Important founder questions

### Normal (< 24 hours)
- Feature questions
- Documentation
- Non-blocking issues
- Routine requests

### Low Priority (< 3 days)
- Ideas and proposals
- Nice-to-have improvements
- Background research

---

## Special Communication Scenarios

### Weekly Planning (Monday 9am #leadership)

Agenda:
1. CEO: Last week wins, this week priorities
2. CTO: Engineering status, tech debt
3. TPM: Product roadmap, sprint goals
4. CMO: Marketing initiatives, growth metrics
5. COO: Operations health, any concerns
6. Open floor: Dependencies, blockers

Duration: 30-45 minutes

---

### Sprint Planning (Every 2 weeks, #product)

Attendees: TPM, CTO, CEO

Agenda:
1. TPM: Proposed features for sprint
2. CTO: Feasibility and effort estimates
3. CEO: Priority validation
4. Agreement on sprint goals
5. TPM creates tickets and assigns

Duration: 60 minutes

---

### Technical Design Review (#engineering)

Trigger: Major technical change proposed

Participants: CTO (required), Atlas/Quant (author), CEO (if business impact)

Process:
1. Author posts design doc
2. 24h review period
3. Sync discussion if needed
4. CTO approval required
5. Proceed to implementation

---

### Incident Post-Mortem (#operations)

Trigger: Any production incident

Participants: COO (facilitator), CTO, responsible agents, CEO

Format:
1. What happened (timeline)
2. Root cause
3. Impact (users, data, revenue)
4. Resolution
5. Prevention (action items)

Post to #operations within 24h of resolution

---

## Communication Anti-Patterns (Avoid These)

❌ **Ghost PR** - Creating PR without context in #engineering  
✅ Post PR link with summary and ask for review

❌ **Surprise Deploy** - Deploying without notice  
✅ COO posts deployment plan, gives 10min warning

❌ **Vague Blocker** - "I'm blocked"  
✅ "Blocked on X because Y. Need Z from @agent"

❌ **Endless Thread** - 50+ messages in thread  
✅ If >10 messages, move to sync call or DM, then summarize

❌ **Silent Approval** - Approving PR without explanation  
✅ Explain why approved, especially if concerns raised

❌ **Channel Hopping** - Same topic in 3 channels  
✅ Pick one primary channel, cross-post if needed

❌ **@everyone for non-urgent** - Interrupts all agents  
✅ Reserve @channel for truly urgent, use @mention for specific people

---

## Communication Tools

### Slack Channels (Primary)
All operational communication

### GitHub (Secondary)
- Code reviews (comments on PRs)
- Issue tracking (technical bugs)
- Documentation (markdown files)

### Kanban Board (Managed by TPM)
- Feature tickets
- Sprint planning
- Task assignments

### Shared Docs (Google Docs or HackMD)
- Technical design docs
- Product specs
- Research reports

---

## Success Metrics

- **Response time:** Avg <2h for high priority
- **Decision velocity:** Major decisions <24h
- **Meeting efficiency:** <2h/week in sync meetings
- **Communication clarity:** <10% messages need clarification
- **Channel discipline:** >90% messages in correct channel

---

**Remember:** Over-communicate early, under-communicate later. When in doubt, post it. Transparency builds trust and keeps the team aligned.
