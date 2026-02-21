# Agent Team - 100x Stocks Business Operations

Multi-agent system for running the 100x Stocks project as a coordinated business.

## 🎯 Vision

A 9-agent team working autonomously in Slack to:
- Discover and analyze potential 100-bagger stocks
- Design and ship new features
- Review each other's work (code, design, strategy)
- Streamline operations
- Generate revenue

**Founder:** Tisse (Human) - Product direction, strategy, final authority  
**CEO:** Lux (AI) - Day-to-day leadership, conflict resolution, priorities  
**Monthly Cost:** ~$45-50 (optimized for intelligence + cost efficiency)

---

## 🏢 Organization Structure

```
FOUNDER (Tisse - Human)
    └── CEO (Lux 🔆) - Opus $10/mo
        ├── CTO (Mercury ⚡) - Codex $5/mo
        │   ├── Data Engineer (Atlas 🌍) - Codex $5/mo
        │   └── Algorithm Dev (Quant 📊) - Codex $5/mo
        ├── COO (Ops 🛠️) - 4o-mini $1.50/mo
        ├── TPM (Compass 🧭) - 4o-mini $1.50/mo
        └── CMO (Nova ✨) - Sonnet $8/mo
            ├── UX (Flow 🎯) - Sonnet $8/mo
            └── UI/Design (Canvas 🎨) - 4o-mini $1.50/mo
```

**Total:** 9 agents, 4 model tiers, ~$45-50/month

---

## 🤖 Agent Roles

### Leadership Layer

**🔆 Lux (CEO)** - Claude Opus 4-5 ($10/mo)
- Strategic leadership and conflict resolution
- Product direction (with TPM)
- Final approvals on critical decisions
- Founder (Tisse) interface

### Technical Layer

**⚡ Mercury (CTO)** - GPT-5.2 Codex ($5/mo)
- Technical architecture and code quality
- **Required approval on ALL PRs**
- Infrastructure decisions
- Manages technical team (Atlas, Quant)

**🌍 Atlas (Data Engineer)** - GPT-5.2 Codex ($5/mo)
- FMP API integration and optimization
- Quarterly financial data refresh automation
- Database management and data quality
- Works closely with Quant

**📊 Quant (Algorithm Dev)** - GPT-5.2 Codex ($5/mo)
- Engine Power algorithm development
- Metric calculations and grading system
- Backtesting and model validation
- Works closely with Atlas

### Operations Layer

**🛠️ Ops (COO)** - GPT-4o-mini ($1.50/mo)
- System health monitoring and alerts
- Deployment coordination
- Job scheduling and incident response
- Agent system monitoring

**🧭 Compass (TPM)** - GPT-4o-mini ($1.50/mo)
- Product roadmap and sprint planning
- Kanban board management
- Feature prioritization and ticket assignment
- Works closely with CEO and CMO

### Growth & Product Layer

**✨ Nova (CMO)** - Claude Sonnet 4-5 ($8/mo)
- Marketing strategy and competitive analysis
- User acquisition and growth experiments
- Content strategy and brand voice
- Manages product/design team (Flow, Canvas)

**🎯 Flow (UX)** - Claude Sonnet 4-5 ($8/mo)
- Information architecture and user flows
- Data visualization strategy
- User research and interaction design
- Works closely with Canvas and Nova

**🎨 Canvas (UI/Design)** - GPT-4o-mini ($1.50/mo)
- Visual identity and branding
- Financial data visualization design
- Component library and CSS implementation
- Works closely with Flow

---

## 📋 Key Workflows

### PR Approval (Critical Code)
1. Developer (Atlas or Quant) creates PR
2. Posts to #engineering
3. **CTO (Mercury) reviews** ✅ (required)
4. **Founder (Tisse) reviews** ✅ (required for algorithm/data)
5. Merge after both approvals
6. COO (Ops) deploys

### Feature Development
1. TPM (Compass) prioritizes feature
2. UX (Flow) designs user flows
3. UI (Canvas) creates visual design
4. CMO (Nova) reviews messaging
5. TPM creates tickets for engineering
6. Technical team implements
7. UX validates post-launch

### Daily Operations
- **6am:** COO posts system health
- **7am:** Atlas posts data refresh summary
- **9am:** All agents post daily standup
- **9:30am:** CEO sets daily priorities
- Throughout day: async collaboration in domain channels
- **6pm:** COO deploys merged PRs
- **8pm:** CEO reviews progress

---

## 📚 Documentation

### Core Files
- **[HIERARCHY.md](HIERARCHY.md)** - Detailed org structure, decision rights, model assignments
- **[COMMUNICATION_MAP.md](COMMUNICATION_MAP.md)** - Channel usage, communication patterns, response SLAs
- **[ORCHESTRATION.md](ORCHESTRATION.md)** - Multi-agent coordination protocols
- **[TEAM_STRUCTURE.md](TEAM_STRUCTURE.md)** - Agent profiles and responsibilities

### Agent Context
- **SOUL.md** - Core personality and principles
- **AGENTS.md** - Workspace conventions
- **ENGINEERING.md** - Product engineering standards
- **USER.md** - About Tisse (founder)
- **TOOLS.md** - Local notes and setup

### Role Instructions
- **roles/LUX.md** - CEO detailed instructions
- **roles/MERCURY.md** - CTO detailed instructions
- *(More role files to be added)*

---

## 🚀 Getting Started

### 1. Set Up Slack Workspace

**Channels:**
- `#general` - Daily standups, company-wide updates
- `#leadership` - Strategic decisions, OKRs
- `#engineering` - PRs, code reviews, architecture
- `#product` - Feature specs, roadmap, UX/UI
- `#marketing` - Growth, content, competitive intel
- `#operations` - Deployments, monitoring, incidents
- `#data` - Data quality, pipeline status
- `#algorithm` - Strategy, backtesting, metrics

### 2. Initialize Agents

Each agent:
1. Forks this repo to their workspace
2. Loads team context (SOUL, AGENTS, etc.)
3. Reads their specific role file
4. Joins relevant Slack channels
5. Posts introduction in #general

### 3. First Sprint

**Week 1 Goals:**
- CEO: Set OKRs and roadmap
- CTO: Technical infrastructure audit
- TPM: Create initial Kanban board
- Atlas: Automate data refresh
- Quant: Document current algorithm
- CMO: Competitive analysis
- Flow: Dashboard UX audit
- Canvas: Create design system
- Ops: Set up monitoring and alerts

### 4. Daily Rhythm

- **Morning:** Standup posts, CEO priorities
- **Midday:** Async collaboration in channels
- **Evening:** Deployments, progress review
- **Monday:** Weekly planning in #leadership
- **Friday:** Retrospective in #leadership

---

## 💡 Design Principles

### Agent Coordination
- **Autonomous but collaborative** - Agents work independently but coordinate on shared goals
- **Transparent communication** - All decisions visible in Slack
- **Clear ownership** - Every decision has a clear owner
- **Fast iteration** - Bias toward action, learn from production
- **Quality gates** - CTO + Founder approval on critical code

### Cost Optimization
- **Tier models by task** - Opus for strategy, Codex for code, 4o-mini for ops
- **Efficient prompting** - Clear instructions, minimal context
- **Batch work** - Group similar tasks together
- **Smart caching** - Reuse computations and data

### Team Culture
- **Results over process** - Ship, don't just talk
- **Teach as you build** - Document decisions
- **Challenge with respect** - Disagree and commit
- **Celebrate wins** - Acknowledge good work
- **Human in the loop** - Tisse has final say

---

## 📊 Success Metrics

### Team Performance
- **Decision velocity:** <24h for major decisions
- **PR merge time:** <24h average
- **Deployment frequency:** >3x/week
- **Incident response:** <10min

### Product Performance
- **Dashboard uptime:** >99.5%
- **Data freshness:** <3 months for >95% stocks
- **API cost:** <$50/month
- **User growth:** Week-over-week increase

### Code Quality
- **Test coverage:** >80%
- **Bug rate:** <5% of releases
- **Technical debt:** Not increasing

---

## 🔧 Tools & Infrastructure

- **Communication:** Slack
- **Code:** GitHub (mfoster58/100x-stocks)
- **Project Management:** Kanban board (managed by TPM)
- **Documentation:** Markdown in repos
- **Monitoring:** Custom dashboards (managed by COO)
- **Financial Data:** FMP API

---

## 📖 Example Day in the Life

**6:00 AM** - Ops: "✅ All systems healthy. Data refresh completed. 712 stocks updated."  
**7:00 AM** - Atlas: "📊 Data refresh summary: 712/716 successful, 4 missing Q4 data (posted to #data)"  
**9:00 AM** - All agents post standup  
**9:30 AM** - Lux: "Today's priority: Ship stock comparison feature. @Compass @Mercury coordinate"  
**10:00 AM** - Compass: "Created tickets for comparison feature. Assigned to @Atlas"  
**11:00 AM** - Atlas: "PR #42 ready for review: Comparison endpoint"  
**11:30 AM** - Mercury: "✅ Approved. Good test coverage, clean code."  
**12:00 PM** - Tisse: "✅ Approved. Business logic looks solid."  
**2:00 PM** - Flow: "UX feedback on comparison view: add side-by-side toggle"  
**3:00 PM** - Canvas: "Updated designs with toggle. Posted to #product"  
**4:00 PM** - Friday retro in #leadership  
**6:00 PM** - Ops: "Deploying comparison feature... ✅ Live"  
**8:00 PM** - Lux: "Great week team. Shipped 3 features, 0 incidents. Have a good weekend! 🔆"

---

## 🎯 Next Steps

1. **Review docs** - Read HIERARCHY.md and COMMUNICATION_MAP.md
2. **Set up Slack** - Create channels, add integrations
3. **Initialize agents** - Give each agent their role context
4. **Run first standup** - Get the rhythm started
5. **Ship first sprint** - Learn and iterate

---

**Built by Lux 🔆**  
**Team designed:** 2026-02-20  
**Status:** Ready for deployment
