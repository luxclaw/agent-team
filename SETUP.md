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

## Step 2: GitHub Configuration

### 2a. Enable Copilot Coding Agent

1. Go to `mfoster58/100x-stocks` → **Settings** → **Copilot** → **Coding agent**
2. Enable it
3. The agent can now be assigned to Issues and will open PRs

### 2b. Create Issue Labels

Create these labels in `mfoster58/100x-stocks`:

| Label | Color | Description |
|-------|-------|-------------|
| `draft` | `#E4E669` | Mercury still scoping |
| `ready` | `#0E8A16` | Fully scoped, assign to Copilot |
| `in-progress` | `#1D76DB` | Copilot working on it |
| `in-review` | `#5319E7` | PR open, Mercury reviewing |
| `changes-requested` | `#FBCA04` | Mercury gave feedback |
| `ready-for-tisse` | `#D93F0B` | Mercury approved, waiting for Tisse |
| `urgent` | `#B60205` | Skip the queue |
| `feature` | `#A2EEEF` | New feature |
| `bugfix` | `#D73A4A` | Bug fix |
| `algorithm` | `#7057FF` | Algo improvement |
| `refactor` | `#C5DEF5` | Code cleanup |

You can create these via GitHub CLI:
```bash
cd /Users/mathiasfoster/repos/100x-stocks
gh label create draft --color E4E669 --description "Mercury still scoping"
gh label create ready --color 0E8A16 --description "Fully scoped, assign to Copilot"
gh label create in-progress --color 1D76DB --description "Copilot working on it"
gh label create in-review --color 5319E7 --description "PR open, Mercury reviewing"
gh label create changes-requested --color FBCA04 --description "Mercury gave feedback"
gh label create ready-for-tisse --color D93F0B --description "Mercury approved, waiting for Tisse"
gh label create urgent --color B60205 --description "Skip the queue"
gh label create algorithm --color 7057FF --description "Algorithm improvement"
```

### 2c. Branch Protection (Optional but Recommended)

Protect `main` in `mfoster58/100x-stocks`:
- Require pull request reviews before merging
- Required reviewers: 1 (you)
- Don't allow bypassing

## Step 3: OpenClaw Agent Setup

### 3a. Create GitHub PAT

Mercury and Nova need a GitHub PAT to create Issues and review PRs in `mfoster58/100x-stocks`:

1. Go to GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**
2. Create token with:
   - **Repository access:** `mfoster58/100x-stocks` + `luxclaw/agent-team`
   - **Permissions:** Issues (Read/Write), Pull Requests (Read/Write), Contents (Read)
3. Store this token securely on the rPi 5 for OpenClaw to use

### 3b. Configure OpenClaw Agents

Each agent needs:
- **Identity:** Read from `roles/AGENT_NAME.md` in this repo
- **System prompt:** Include the agent's role file + relevant coordination docs
- **Tools:** GitHub API (via PAT), Slack API, web search
- **Schedule:** Cron jobs per `AUTONOMY.md`

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
  - ORCHESTRATION.md
  - HIERARCHY.md
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
  - ORCHESTRATION.md
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
  - ORCHESTRATION.md
  - HIERARCHY.md
  - AUTONOMY.md
tools:
  - github_api       # Read pipeline status, Issue/PR state
  - slack_api         # Post to #general
repos:
  primary: mfoster58/100x-stocks
  config: luxclaw/agent-team
```

## Step 4: FMP API & MCP

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

### What Doesn't Work (Yet)

- Copilot coding agent running in GitHub Actions **cannot** call FMP live (no API key in CI)
- For tests involving FMP data, Copilot should mock the API or use cached data from `data/`

## Step 5: Cross-Repo Workflow

### How Agents Bridge the Two Repos

```
agent-team repo                        100x-stocks repo
┌─────────────────────┐                ┌──────────────────────┐
│ OpenClaw reads:     │                │ Copilot works here:  │
│ - roles/*.md        │                │ - Writes code        │
│ - ORCHESTRATION.md  │  GitHub API    │ - Opens PRs          │
│ - AUTONOMY.md       │ ────────────►  │ - Creates branches   │
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

## Step 6: First Test Run

Once everything is set up, test the pipeline end-to-end:

### Manual Test (No OpenClaw Needed)

1. Create a simple Issue in `mfoster58/100x-stocks`:
   ```
   Title: Add loading spinner to stock detail modal
   Body: When a user clicks a stock row, show a loading spinner while
         the detail data loads. Currently the modal is blank for ~1s.
   Labels: ready, feature
   Assignee: @copilot
   ```
2. Watch Copilot pick it up and open a PR
3. Review the PR yourself
4. If good, merge — the pipeline works

### OpenClaw Test

1. Start Mercury on the rPi with his config
2. Give him a simple task in Slack: "Mercury, create an Issue to add a dark mode toggle to the dashboard"
3. Mercury should:
   - Create a well-scoped Issue in `mfoster58/100x-stocks`
   - Assign it to `@copilot`
   - Label it `ready` + `feature`
   - Post to #engineering
4. Copilot picks it up, codes it, opens PR
5. Mercury reviews on next wake-up

## Checklist

- [ ] Slack workspace with 4 channels
- [ ] GitHub App installed in Slack
- [ ] Copilot coding agent enabled on `mfoster58/100x-stocks`
- [ ] Issue labels created in `mfoster58/100x-stocks`
- [ ] Branch protection on `main`
- [ ] GitHub PAT created for OpenClaw agents
- [ ] OpenClaw installed on rPi 5
- [ ] Lux, Mercury, Nova configured in OpenClaw
- [ ] Cron schedules set per AUTONOMY.md
- [ ] End-to-end test: Issue → Copilot PR → review → merge
