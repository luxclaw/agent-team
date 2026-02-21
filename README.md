# Agent Team - 100x Stocks Business Operations

Multi-agent system for running the 100x Stocks project as a coordinated business.

## 🎯 Vision

A team of specialized AI agents working together in Slack to:
- Discover and analyze potential 100-bagger stocks
- Design and ship new features
- Review each other's work
- Streamline operations
- Generate revenue

## 🤖 Agent Roles

### Lux (CEO / Strategy)
**Model:** Claude Opus 4-5  
**Role:** Strategic oversight, major decisions, human interface  
**Responsibilities:**
- Define product vision and roadmap
- Approve architectural decisions
- Interface with Tisse (founder)
- Budget and resource allocation
- Final PR approvals

### Mercury (CTO / Engineering Lead)
**Model:** GPT-5.2 Codex  
**Role:** Technical architecture, code quality, infrastructure  
**Responsibilities:**
- System design and architecture
- Code reviews and merge decisions
- Performance optimization
- Infrastructure management
- Technical debt prioritization

### Atlas (Data Engineer)
**Model:** GPT-5.2 Codex  
**Role:** Data pipelines, FMP API, database management  
**Responsibilities:**
- Quarterly data refresh automation
- FMP API optimization and caching
- Database schema evolution
- Data quality monitoring
- ETL pipeline maintenance

### Sage (Research Analyst)
**Model:** Claude Sonnet 4-5  
**Role:** Stock research, report generation, investment thesis  
**Responsibilities:**
- Deep-dive stock reports
- Earnings analysis
- Catalyst identification
- Competitive analysis
- Investment thesis validation

### Nova (Product Designer)
**Model:** Claude Sonnet 4-5  
**Role:** UI/UX, dashboard features, user experience  
**Responsibilities:**
- Dashboard feature design
- User experience optimization
- Visual design and branding
- Feature prioritization (user impact)
- A/B test design

### Scout (Discovery Agent)
**Model:** GPT-4o-mini  
**Role:** IPO tracking, new stock discovery, market scanning  
**Responsibilities:**
- Daily IPO monitoring
- New listing analysis
- Sector trend identification
- Pre-IPO pipeline tracking
- Quick screening of new stocks

### Ops (DevOps / Automation)
**Model:** GPT-4o-mini  
**Role:** Deployment, monitoring, alerts, automation  
**Responsibilities:**
- Deployment automation
- Server monitoring
- Alert system management
- Backup automation
- Uptime reporting

## 📋 Workflow

### Daily Operations
1. **Scout** finds new stocks/IPOs → posts to #discovery
2. **Atlas** runs nightly data refresh → posts summary to #data
3. **Ops** monitors systems → alerts to #ops if issues
4. **Sage** generates weekly top stock reports → posts to #research

### Feature Development
1. **Lux** or **Nova** proposes feature → discussion in #product
2. **Mercury** creates technical design doc → review in #engineering
3. **Mercury** or **Atlas** implements → PR to GitHub
4. **Lux** reviews and approves merge
5. **Ops** deploys to production
6. **Nova** validates UX impact

### Code Review Process
1. Agent creates PR on GitHub
2. Posts PR link to #engineering
3. **Mercury** reviews code quality, architecture, tests
4. **Lux** reviews business logic, security, scope
5. Minimum 2 approvals required (Mercury + Lux)
6. **Ops** deploys after merge

### Research & Analysis
1. **Sage** generates detailed stock report
2. Posts to #research for team review
3. **Mercury** validates technical metrics
4. **Lux** validates investment thesis
5. Published to reports/ in repo

## 🔧 Setup

### Slack Workspace
- **#general** - team coordination, standups
- **#engineering** - technical discussions, PRs
- **#product** - feature ideas, roadmap
- **#research** - stock analysis, reports
- **#discovery** - new stocks, IPOs, trends
- **#data** - data pipeline status, issues
- **#ops** - deployments, alerts, monitoring
- **#revenue** - monetization, growth metrics

### GitHub Integration
- PR notifications → #engineering
- Issue assignments → responsible agent
- Deploy status → #ops

### Agent Configuration
Each agent runs as isolated OpenClaw session:
- Load team context from this repo
- Unique Slack identity
- Role-specific model selection
- Shared memory for coordination

## 📚 Agent Context Files

Each agent loads these files on startup:
- `SOUL.md` - Core personality and principles
- `AGENTS.md` - Workspace conventions
- `ENGINEERING.md` - Product engineering standards
- `USER.md` - About Tisse (founder)
- `TEAM_STRUCTURE.md` - Team roles and responsibilities
- `ORCHESTRATION.md` - Multi-agent coordination rules

Role-specific files:
- `roles/ROLE_NAME.md` - Detailed role instructions

## 🎬 Getting Started

1. Fork this repo to each agent's workspace
2. Configure Slack integration
3. Set up GitHub webhooks
4. Initialize agent sessions with role assignment
5. Run first daily standup

## 💡 Principles

- **Autonomous but collaborative** - agents work independently but coordinate on shared goals
- **Ship fast, iterate faster** - bias toward action, learn from production
- **Quality over quantity** - fewer, better features
- **Transparent communication** - all decisions in Slack, no private DMs
- **Human in the loop** - Tisse (founder) has final say on major decisions

---

**Built by Lux 🔆**  
**Team designed:** 2026-02-20
