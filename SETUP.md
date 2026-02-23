# SETUP.md — Getting the System Running

Step-by-step guide to launch the 3-agent team.

## Prerequisites

- [ ] Raspberry Pi 5 with OpenClaw installed
- [ ] GitHub Copilot Enterprise (free via your subscription)
- [ ] Slack workspace created
- [ ] FMP API key (already in `100x-stocks/.env`)
- [ ] GitHub PAT with `repo` scope (for agent API access)

## Repos

| Repo | Purpose | Agents Active |
|------|---------|--------------|
| `luxclaw/agent-team` | Agent identities, roles, coordination protocols | OpenClaw reads this |
| `mfoster58/100x-stocks` | Product code (Python + Node.js) | Copilot writes code here |

Agents think in `agent-team`, build in `100x-stocks`.

## Step 1: Slack Setup

### 1a. Create Channels

```
#general       — Lux posts pipeline status, cross-team coordination
#engineering   — Mercury posts PRs, technical decisions, Copilot updates
#product       — Nova posts research, product strategy, feature proposals
#data          — Mercury posts algo updates, backtesting results
```

### 1b. Install GitHub App in Slack

1. Go to your Slack workspace → **Apps** → search **"GitHub"**
2. Install the official GitHub app
3. In any channel, type `/github subscribe mfoster58/100x-stocks`
4. This gives you PR notifications, Issue updates, etc.

### 1c. Copilot Coding Agent via Slack

In any Slack channel, `@GitHub` triggers the Copilot coding agent:
```
@GitHub Add a tooltip to the stock detail modal showing Engine Power breakdown
```

This creates a branch in `100x-stocks`, writes the code, and opens a PR. The agent follows `100x-stocks/.github/copilot-instructions.md` for context.

**Note:** Slack-triggered Copilot uses the repo where the GitHub app is subscribed. Make sure `mfoster58/100x-stocks` is your default.

## Step 2: GitHub Projects Board

### 2a. Create the Project

1. Go to `mfoster58/100x-stocks` → **Projects** tab → **New project**
2. Choose **Board** layout
3. Name it **"100x Stocks"**

### 2b. Set Up Columns

Delete default columns, create these (in order):

| Column | Description |
|--------|-------------|
| Backlog | Ideas, research findings, unscoped work |
| Sprint | Current week's prioritized work |
| In Progress | Copilot actively coding |
| In Review | PR open, Mercury reviewing |
| Ready for Tisse | Mercury approved, awaiting final sign-off |
| Done | Merged to main |

### 2c. Add Custom Fields

In Project settings → **Fields**, add:

| Field | Type | Options |
|-------|------|---------|
| Sprint | Iteration | 1-week iterations starting next Monday |
| Stream | Single select | `Algorithm`, `App`, `Data Pipeline`, `Product/Marketing` |
| Priority | Single select | `P0 (Critical)`, `P1 (High)`, `P2 (Medium)`, `P3 (Low)` |
| Effort | Single select | `S (hours)`, `M (1-2 days)`, `L (3+ days)` |

### 2d. Enable Automations

In Project settings → **Workflows**:
- **Item added** → Set status to Backlog
- **Pull request merged** → Set status to Done
- **Item closed** → Set status to Done

### 2e. Link the Project to the Repo

Go to `mfoster58/100x-stocks` → **Settings** → **Projects** → link the board. This lets Issues auto-appear on the board.

## Step 3: GitHub Configuration

### 3a. Enable Copilot Coding Agent

1. Go to `mfoster58/100x-stocks` → **Settings** → **Copilot** → **Coding agent**
2. Enable it
3. The agent can now be assigned to Issues and will open PRs

### 3b. Configure FMP MCP for Coding Agent

This gives Copilot **live access to FMP financial data** while coding (backtesting, validating metrics, fetching data).

1. Go to `mfoster58/100x-stocks` → **Settings** → **Copilot** → **Coding agent**
2. In the **MCP configuration** section, add:
   ```json
   {
     "mcpServers": {
       "fmp": {
         "type": "sse",
         "url": "https://financialmodelingprep.com/mcp?apikey=$COPILOT_MCP_FMP_API_KEY",
         "tools": ["*"]
       }
     }
   }
   ```
3. Click **Save**
4. Go to **Settings** → **Environments** → **New environment** → name it `copilot`
5. Under **Environment secrets**, add `COPILOT_MCP_FMP_API_KEY` with your FMP API key value

### 3c. Custom Agents (Already Created)

Three custom agent profiles exist in `.github/agents/`:

| Agent File | Name | Assigned By | Domain |
|------------|------|-------------|--------|
| `algo-engineer.agent.md` | algo-engineer | Mercury | Algorithm, Python, FMP data, backtesting |
| `app-engineer.agent.md` | app-engineer | Mercury | Dashboard, Express API, vanilla JS |
| `product-engineer.agent.md` | product-engineer | Nova | Landing pages, content, analytics |

When assigning an Issue to Copilot, select the right custom agent from the dropdown — each has deep domain context baked in.

### 3d. Create Issue Labels

Create these labels in `mfoster58/100x-stocks` (status tracking is handled by the Projects board columns, so labels are for type/stream filtering):

| Label | Color | Description |
|-------|-------|-------------|
| `algorithm` | `#7057FF` | Engine Power, metrics, backtesting |
| `app` | `#A2EEEF` | Dashboard, UX, endpoints |
| `data-pipeline` | `#1D76DB` | FMP integration, refresh, caching |
| `product` | `#E4E669` | Marketing pages, content, analytics |
| `bugfix` | `#D73A4A` | Bug fix |
| `refactor` | `#C5DEF5` | Code cleanup |
| `urgent` | `#B60205` | Skip the queue |

You can create these via GitHub CLI:
```bash
cd /Users/mathiasfoster/repos/100x-stocks
gh label create algorithm --color 7057FF --description "Engine Power, metrics, backtesting"
gh label create app --color A2EEEF --description "Dashboard, UX, endpoints"
gh label create data-pipeline --color 1D76DB --description "FMP integration, refresh, caching"
gh label create product --color E4E669 --description "Marketing pages, content, analytics"
gh label create bugfix --color D73A4A --description "Bug fix"
gh label create refactor --color C5DEF5 --description "Code cleanup"
gh label create urgent --color B60205 --description "Skip the queue"
```

### 3e. Branch Protection (Optional but Recommended)

Protect `main` in `mfoster58/100x-stocks`:
- Require pull request reviews before merging
- Required reviewers: 1 (you)
- Don't allow bypassing

## Step 4: OpenClaw Agent Setup

### 4a. Create GitHub PAT

Mercury and Nova need a GitHub PAT to create Issues and review PRs in `mfoster58/100x-stocks`:

1. Go to GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**
2. Create token with:
   - **Repository access:** `mfoster58/100x-stocks` + `luxclaw/agent-team`
   - **Permissions:** Issues (Read/Write), Pull Requests (Read/Write), Contents (Read)
3. Store this token securely on the rPi 5 for OpenClaw to use

### 4b. Configure OpenClaw Agents

Each agent needs:
- **Identity:** Read from `roles/AGENT_NAME.md` in this repo
- **System prompt:** Include the agent's role file + relevant coordination docs
- **Tools:** GitHub API (via PAT), Slack API, web search
- **Schedule:** Cron jobs per `docs/AUTONOMY.md`

#### Mercury's OpenClaw Config (Conceptual)

```yaml
name: mercury
model: claude-sonnet
schedule:
  - "0 8 * * 1-5"   # 8am weekdays — morning PR review
  - "0 11 * * 1-5"  # 11am weekdays — create Issues, deep work
  - "0 15 * * 1-5"  # 3pm weekdays — afternoon PR review
  - "0 19 * * 1-5"  # 7pm weekdays — evening pipeline check
  - "0 10 * * 6"    # 10am Saturday — weekly review
context:
  - roles/MERCURY.md
  - docs/ORCHESTRATION.md
  - docs/HIERARCHY.md
tools:
  - github_api       # Create Issues, review PRs in mfoster58/100x-stocks
  - slack_api         # Post to #engineering, #data
  - web_search        # Research, documentation lookup
repos:
  primary: mfoster58/100x-stocks   # Where code lives
  config: luxclaw/agent-team        # Where identity lives
```

#### Nova's OpenClaw Config (Conceptual)

```yaml
name: nova
model: claude-sonnet
schedule:
  - "0 9 * * 1-5"   # 9am weekdays — daily research
  - "0 14 * * 2,4"  # 2pm Tue/Thu — deep research dives
  - "0 10 * * 6"    # 10am Saturday — weekly synthesis
context:
  - roles/NOVA.md
  - docs/ORCHESTRATION.md
tools:
  - github_api       # Create product-related Issues
  - slack_api         # Post to #product
  - web_search        # Market research, competitor analysis
  - playwright        # Browse competitor sites, user research
repos:
  primary: mfoster58/100x-stocks
  config: luxclaw/agent-team
```

#### Lux's OpenClaw Config (Conceptual)

```yaml
name: lux
model: claude-sonnet
schedule:
  - "0 9 * * 1-5"   # 9am weekdays — daily check-in
  - "0 20 * * 0"    # 8pm Sunday — prep Monday priorities
context:
  - roles/LUX.md
  - docs/ORCHESTRATION.md
  - docs/HIERARCHY.md
  - docs/AUTONOMY.md
tools:
  - github_api       # Read pipeline status, Issue/PR state
  - slack_api         # Post to #general
repos:
  primary: mfoster58/100x-stocks
  config: luxclaw/agent-team
```

## Step 5: FMP API & MCP

### Already Configured

The `100x-stocks` repo already has FMP MCP configured:

**`.vscode/mcp.json`:**
```json
{
  "servers": {
    "fmp": {
      "type": "sse",
      "url": "https://financialmodelingprep.com/mcp?apikey=${FMP_API_KEY}"
    }
  }
}
```

This gives **VS Code Copilot sessions** direct access to FMP financial data.

### What Agents Can Do with FMP

- **Mercury** can reference `docs/FMP_API_REFERENCE.md` when creating Issues that involve new FMP endpoints
- **Copilot coding agent** can write Python scripts that call FMP (using the key in `.env`)
- **Live FMP queries** happen when you run the Python scripts locally or on the rPi

### Enabling FMP for Copilot Coding Agent

The coding agent runs in a sandboxed GitHub Actions VM — it doesn't have your local `.env` or MCP servers. To give it FMP access:

1. Go to `mfoster58/100x-stocks` → **Settings** → **Secrets and variables** → **Actions**
2. Add `FMP_API_KEY` as a **repository secret**
3. Copilot can now use the key in Python scripts it runs during coding

**Note:** The `.vscode/mcp.json` MCP config only works in local VS Code sessions. The coding agent calls FMP directly via Python `requests` — no MCP needed.

### Custom Skills for Copilot

Copilot can install packages and run any script in the repo. To give it "skills":

- `scripts/backtest.py` — validate algo changes
- `scripts/regression_analysis.py` — test new metrics
- Any Python/Node script is a tool Copilot can execute

Add dependencies to `requirements.txt` and Copilot will `pip install` them automatically.

## Step 6: Cross-Repo Workflow

### How Agents Bridge the Two Repos

```
agent-team repo                        100x-stocks repo
┌─────────────────────┐                ┌──────────────────────┐
│ OpenClaw reads:     │                │ Copilot works here:  │
│ - roles/*.md        │                │ - Writes code        │
│ - docs/ORCHESTRATION.md  │  GitHub API    │ - Opens PRs          │
│ - docs/AUTONOMY.md       │ ────────────►  │ - Creates branches   │
│                     │ (create Issues │                      │
│ Mercury/Nova think  │  review PRs)   │ copilot-instructions │
│ here, act there     │                │ .md guides Copilot   │
└─────────────────────┘                └──────────────────────┘
```

**Key insight:** Agents are *configured* by `agent-team` but *work* in `100x-stocks`.

### Mercury Creates an Issue (Example API Call)

When Mercury wakes up and decides to create a task:

```
POST /repos/mfoster58/100x-stocks/issues
{
  "title": "Add ROIC metric to Engine Power calculation",
  "body": "## Task\nAdd Return on Invested Capital...",
  "labels": ["ready", "algorithm"],
  "assignees": ["copilot"]
}
```

Mercury reads his role docs from `agent-team`, creates Issues in `100x-stocks`.

### Keeping copilot-instructions.md in Sync

`100x-stocks/.github/copilot-instructions.md` already exists and is comprehensive. If the agent team process changes (new labels, new conventions), update it there too.

## Step 7: First Test Run

Once everything is set up, test the pipeline end-to-end:

### Manual Test (No OpenClaw Needed)

1. Create a simple Issue in `mfoster58/100x-stocks`:
   ```
   Title: Add loading spinner to stock detail modal
   Body: When a user clicks a stock row, show a loading spinner while
         the detail data loads. Currently the modal is blank for ~1s.
   Labels: app
   Assignee: @copilot
   ```
2. Add the Issue to the Projects board → Sprint column
3. Watch Copilot pick it up and open a PR
4. Review the PR yourself
5. If good, merge — card auto-moves to Done

### OpenClaw Test

1. Start Mercury on the rPi with his config
2. Give him a simple task in Slack: "Mercury, create an Issue to add a dark mode toggle to the dashboard"
3. Mercury should:
   - Create a well-scoped Issue in `mfoster58/100x-stocks`
   - Assign it to `@copilot`
   - Label it `app`
   - Add to Projects board → Sprint
   - Post to #engineering
4. Copilot picks it up, codes it, opens PR
5. Mercury reviews on next wake-up, moves card through columns

## Checklist

- [ ] Slack workspace with 4 channels
- [ ] GitHub App installed in Slack
- [ ] GitHub Projects board created with 6 columns
- [ ] Custom fields added (Sprint, Stream, Priority, Effort)
- [ ] Board automations enabled
- [ ] Copilot coding agent enabled on `mfoster58/100x-stocks`
- [ ] Issue labels created in `mfoster58/100x-stocks`
- [ ] Branch protection on `main`
- [ ] GitHub PAT created for OpenClaw agents
- [ ] OpenClaw installed on rPi 5
- [ ] Lux, Mercury, Nova configured in OpenClaw
- [ ] Cron schedules set per docs/AUTONOMY.md
- [ ] End-to-end test: Issue → Copilot PR → review → merge
