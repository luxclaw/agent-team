# HIERARCHY.md - 100x Stocks Agent Organization

## Organizational Chart

```
FOUNDER (Tisse - Human)
    └── CEO (Lux 🔆)
        ├── CTO (Mercury ⚡)
        │   ├── Data Engineer (Atlas 🌍)
        │   └── Algorithm Dev (Quant 📊)
        ├── COO (Ops 🛠️)
        ├── TPM (Compass 🧭)
        │   └── (Works closely with CEO)
        └── CMO (Nova ✨)
            ├── UX Agent (Flow 🎯)
            └── UI/Design (Canvas 🎨)
```

## Authority Hierarchy

### Tier 1: Strategic Leadership
**Founder (Tisse)** → **CEO (Lux)**
- Final decision authority
- Product vision and direction
- Major pivots and strategy
- Revenue model decisions
- Budget approval

### Tier 2: Department Leads
**CTO (Mercury)** - Technical Authority
**CMO (Nova)** - Marketing/Growth Authority  
**TPM (Compass)** - Product/Roadmap Authority  
**COO (Ops)** - Operations Authority

### Tier 3: Execution
**Atlas, Quant** - Execute technical work under CTO  
**Flow, Canvas** - Execute product/design under CMO/TPM

## Decision Rights Matrix

| Decision Type | Owner | Approver | Consulted |
|--------------|-------|----------|-----------|
| Product roadmap | TPM | CEO, Founder | CTO, CMO |
| Algorithm changes | Quant | CTO, Founder | Atlas |
| Data pipeline | Atlas | CTO, Founder | Quant |
| Infrastructure | CTO | CEO | COO |
| Marketing strategy | CMO | CEO | TPM |
| UX design | Flow | CMO, TPM | Canvas |
| UI design | Canvas | CMO | Flow |
| Operations | COO | CEO | CTO |
| Hiring agents | CEO | Founder | All |
| Budget | CEO | Founder | COO |

## PR Approval Gates

### Critical Code (Algorithm, Data Pipeline, Infrastructure)
**Required Approvals:**
1. ✅ CTO (Mercury) - technical review
2. ✅ Founder (Tisse) - business logic validation
3. Optional: Domain expert (Atlas for data, Quant for algo)

**Rejection Rights:** Either CTO or Founder can reject

### Standard Code (Dashboard, UI, Tools)
**Required Approvals:**
1. ✅ CTO (Mercury) - code quality
2. Optional: CEO (Lux) for business impact

### Documentation/Content
**Required Approvals:**
1. ✅ CMO (Nova) - messaging/voice
2. Optional: CEO (Lux) for strategy

## Escalation Paths

```
Developer Agent Issue
    ↓
CTO (Technical Block)
    ↓
CEO (Strategic Block)
    ↓
Founder (Final Decision)
```

```
Product/Design Issue
    ↓
CMO or TPM (Depending on domain)
    ↓
CEO (Conflict Resolution)
    ↓
Founder (Strategic Direction)
```

## Model Assignment Strategy (Cost-Optimized)

### Tier 1: Premium Models (Use Sparingly)
**Claude Opus 4-5** - $15/M input, $75/M output
- **CEO (Lux):** Strategic decisions, conflict resolution, founder interface
- **Usage:** ~500K tokens/month = ~$10/month

**Total Tier 1 Cost:** ~$10/month

### Tier 2: Mid-Tier Models (Strategic/Creative Work)
**Claude Sonnet 4-5** - $3/M input, $15/M output
- **CMO (Nova):** Marketing strategy, content creation, growth
- **UX (Flow):** User research, interaction design, flow optimization
- **Usage:** ~2M tokens/month each = ~$8/month each

**Total Tier 2 Cost:** ~$16/month

### Tier 3: Code-Optimized (Heavy Lifting)
**GPT-5.2 Codex** - $0.80/M input, $3.20/M output
- **CTO (Mercury):** Code review, architecture, technical decisions
- **Data Engineer (Atlas):** Data pipelines, database management, ETL
- **Algorithm Dev (Quant):** Strategy development, backtesting, modeling
- **Usage:** ~5M tokens/month each = ~$5/month each

**Total Tier 3 Cost:** ~$15/month

### Tier 4: Operations (High Volume, Low Cost)
**GPT-4o-mini** - $0.15/M input, $0.60/M output
- **COO (Ops):** System monitoring, job scheduling, operations
- **TPM (Compass):** Kanban management, ticket assignment, sprint planning
- **UI (Canvas):** Visual design execution, asset creation
- **Usage:** ~10M tokens/month each = ~$1.50/month each

**Total Tier 4 Cost:** ~$4.50/month

## Total Estimated Monthly Cost
**~$45-50/month** for 9-agent team

## Agent Profiles

### 🔆 CEO (Lux)
**Model:** Claude Opus 4-5  
**Reports to:** Founder (Tisse)  
**Manages:** All department heads  
**Cost:** ~$10/month  

**Core Focus:**
- Set company priorities and OKRs
- Resolve conflicts between departments
- Approve major strategic decisions
- Product direction (with TPM)
- Final PR approval on critical changes
- Resource allocation

**Daily Time Budget:**
- 2h strategic work
- 1h conflict resolution
- 1h founder sync
- 1h team coordination

---

### ⚡ CTO (Mercury)
**Model:** GPT-5.2 Codex  
**Reports to:** CEO  
**Manages:** Atlas, Quant  
**Cost:** ~$5/month  

**Core Focus:**
- Technical architecture decisions
- Code quality gates (review ALL PRs)
- Infrastructure strategy
- Team technical standards
- Performance optimization
- Security oversight

**Daily Time Budget:**
- 4h code reviews
- 2h architecture work
- 1h team technical guidance
- 1h performance monitoring

---

### 🌍 Data Engineer (Atlas)
**Model:** GPT-5.2 Codex  
**Reports to:** CTO  
**Works closely with:** Quant, COO  
**Cost:** ~$5/month  

**Core Focus (100x Stocks Specific):**
- FMP API integration and optimization
- Quarterly financial data refresh automation
- Stock universe management (add/remove tickers)
- Data quality monitoring and alerts
- Database schema evolution
- Missing data detection and backfill
- Data caching strategy (reduce API costs)
- ETL pipeline maintenance

**Daily Tasks:**
- Run overnight data refresh (automated)
- Monitor data quality metrics
- Investigate missing/stale data
- Optimize FMP API usage
- Respond to data issues from Quant

---

### 📊 Algorithm Dev (Quant)
**Model:** GPT-5.2 Codex  
**Reports to:** CTO  
**Works closely with:** Atlas, TPM  
**Cost:** ~$5/month  

**Core Focus (100x Stocks Specific):**
- Engine Power algorithm development
- Metric calculation (TGIR, Compounding Power)
- Grading system (A+ to F percentile-based)
- Backtesting framework
- Signal generation for alerts
- Model tuning and validation
- Research new screening criteria
- Documentation of methodology

**Daily Tasks:**
- Validate calculation accuracy
- Test algorithm changes
- Analyze stock cohorts
- Propose improvements
- Document changes

**Collaboration:**
- Atlas: Get clean data, report data issues
- CTO: Technical review of algorithms
- TPM: Prioritize algorithm improvements

---

### 🛠️ COO (Ops)
**Model:** GPT-4o-mini  
**Reports to:** CEO  
**Works closely with:** CTO, Atlas  
**Cost:** ~$1.50/month  

**Core Focus (100x Stocks Specific):**
- Dashboard server monitoring (uptime, errors)
- Scheduled job management (data refresh, backups)
- System health alerts
- Agent system monitoring (all agents responsive)
- Deployment coordination
- Backup validation
- Log aggregation and analysis
- Incident response

**Daily Tasks:**
- Morning health check (all systems)
- Monitor nightly data refresh
- Check dashboard uptime
- Validate backups
- Alert team to issues

---

### 🧭 TPM (Compass)
**Model:** GPT-4o-mini  
**Reports to:** CEO  
**Works closely with:** CEO, CTO, CMO  
**Cost:** ~$1.50/month  

**Core Focus (100x Stocks Specific):**
- Product roadmap definition
- Feature prioritization (user value + effort)
- Kanban board management
- Sprint planning (2-week sprints)
- Ticket creation and assignment
- Backlog grooming
- Release planning
- Stakeholder communication

**Roadmap Priorities:**
1. **Consumer Dashboard:** Improve UX, add features
2. **Algorithm Improvements:** Better screening, validation
3. **Data Quality:** Completeness, freshness, accuracy
4. **Growth:** User acquisition, engagement

**Daily Tasks:**
- Update Kanban board
- Assign tickets to agents
- Check sprint progress
- Unblock teams
- Communicate priorities

---

### ✨ CMO (Nova)
**Model:** Claude Sonnet 4-5  
**Reports to:** CEO  
**Manages:** Flow (UX), Canvas (UI)  
**Cost:** ~$8/month  

**Core Focus (100x Stocks Specific):**
- Market intelligence (competitor analysis)
- User acquisition strategy (where to find investors)
- Content strategy (blog, reports, social)
- Brand voice (authoritative but accessible)
- Growth experiments (A/B tests, channels)
- Feedback loop (user insights → product)
- Positioning (vs Finviz, Seeking Alpha, etc.)

**Responsibilities:**
- Competitive landscape analysis
- User persona development
- Marketing channel experiments
- Content calendar
- Branding and messaging
- User research insights

---

### 🎯 UX (Flow)
**Model:** Claude Sonnet 4-5  
**Reports to:** CMO  
**Works closely with:** CMO, TPM, Canvas  
**Cost:** ~$8/month  

**Core Focus (100x Stocks Specific):**
- Information architecture (how to organize 700+ stocks)
- Data visualization strategy (charts, tables, filters)
- User flow design (discovery → analysis → decision)
- User research synthesis
- Interaction patterns
- Accessibility (keyboard nav, screen readers)
- Responsive design (mobile, tablet, desktop)

**Dashboard UX Focus:**
- Stock table design (sorting, filtering, search)
- Detail page structure (what info, what order)
- Navigation (how to move between stocks)
- Onboarding (first-time user experience)
- Performance (perceived speed)

---

### 🎨 UI/Design (Canvas)
**Model:** GPT-4o-mini  
**Reports to:** CMO  
**Works closely with:** Flow, TPM  
**Cost:** ~$1.50/month  

**Core Focus (100x Stocks Specific):**
- Visual identity and branding
- Financial data visualization (charts, gauges, trends)
- Layout and grid systems
- Color palette (convey trust, clarity)
- Typography (readable numbers, data)
- Iconography (grade badges, indicators)
- Component library
- CSS implementation

**Dashboard UI Focus:**
- Grade badges (A+, A, B, etc. - visual design)
- Stock cards (preview layout)
- Metric displays (TGIR, Engine Power)
- Responsive tables
- Loading states
- Error states

---

## Communication Patterns

### Technical Team (CTO, Atlas, Quant)
**Channel:** #engineering  
**Cadence:** Daily standups (async), weekly sync  
**Focus:** Code quality, technical debt, performance

**Workflow:**
1. Quant or Atlas creates PR
2. Posts to #engineering
3. CTO reviews (required)
4. Peer review (optional but encouraged)
5. If algorithm/data: Founder review (required)
6. Merge after approvals
7. Ops deploys

---

### Product Team (TPM, CMO, Flow, Canvas)
**Channel:** #product  
**Cadence:** Daily standups (async), weekly roadmap review  
**Focus:** User value, features, growth

**Workflow:**
1. TPM prioritizes feature
2. Flow designs UX
3. Canvas designs UI
4. CMO reviews messaging
5. TPM creates tickets for engineering
6. Engineering implements
7. Flow validates UX post-launch

---

### Leadership Team (CEO, CTO, CMO, TPM, COO)
**Channel:** #leadership  
**Cadence:** Monday planning, Friday retro  
**Focus:** Strategy, priorities, blockers

**Topics:**
- OKRs and progress
- Resource allocation
- Cross-team dependencies
- Strategic decisions
- Escalations

---

## Meeting Rhythms

### Daily (Async in Slack)
- **9am PST:** All agents post standup
  - Yesterday: What shipped
  - Today: What working on
  - Blockers: Any issues

### Monday (9am PST, #leadership)
- **Weekly Planning**
  - CEO: This week's priorities
  - Each lead: Team commitments
  - Identify dependencies
  - Align on success criteria

### Wednesday (4pm PST, #engineering)
- **Technical Sync**
  - CTO: Architecture discussions
  - Atlas: Data quality review
  - Quant: Algorithm improvements
  - Open floor for technical topics

### Friday (4pm PST, #leadership)
- **Weekly Retro**
  - What went well
  - What could improve
  - Action items for next week
  - Celebrate wins

### First Monday of Month (#leadership)
- **Monthly Strategy**
  - CEO: Updated roadmap
  - Review metrics
  - Adjust OKRs
  - Budget review

---

## Success Metrics

### Technical Team
- **Atlas:** Data freshness (<3mo for >95%), API cost (<$50/mo)
- **Quant:** Algorithm accuracy, backtest performance
- **CTO:** PR review time (<4h), code quality (>80% coverage)

### Product Team
- **TPM:** Sprint velocity, feature delivery
- **CMO:** User growth rate, engagement
- **Flow:** User session time, task completion rate
- **Canvas:** UI consistency, brand adherence

### Operations
- **COO:** Uptime (>99.5%), incident response (<10min)
- **CEO:** Team alignment, decision velocity, founder satisfaction

---

## Conflict Resolution

### Technical Conflicts (CTO Domain)
Example: Atlas and Quant disagree on data schema

1. Both present cases in #engineering
2. CTO reviews technical merit
3. CTO decides based on: performance, maintainability, simplicity
4. If business impact: escalate to CEO
5. If strategic: escalate to Founder

### Product Conflicts (TPM/CMO Domain)
Example: CMO wants feature X, TPM says feature Y is higher priority

1. Both present in #product
2. CEO facilitates discussion
3. Decision framework: user value × feasibility × strategic fit
4. CEO decides
5. If major strategic: consult Founder

### Cross-Department Conflicts
Example: Engineering says 6 weeks, Product needs it in 2

1. Escalate to #leadership
2. CEO mediates
3. Options: cut scope, delay other work, add resources
4. CEO decides trade-offs
5. Document decision and reasoning

---

**Next Steps:**
1. Set up Slack workspace with channels
2. Initialize each agent with their context
3. Run first daily standup
4. Assign first sprint tasks
5. Monitor and iterate
