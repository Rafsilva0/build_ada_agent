# Claude Code Skills for Demo Automation

These skills let the SC team run the Ada demo provisioning directly from Claude Code — with automatic prospect research, a customisable plan, and a post-provision summary.

## Skills

| Skill | Description |
|-------|-------------|
| `sc:provision-demo` | Provision a full Ada demo bot from a company name + website |

---

## Installation

Copy and paste the following prompt into Claude Code:

> Install the `sc:provision-demo` skill from `https://github.com/Rafsilva0/demo_automation`. Clone the repo to `~/Documents/GitHub/demo_automation` if it doesn't exist yet, install Python dependencies, copy `skills/provision-demo/SKILL.md` to `~/.claude/plugins/cache/sc-claude-tools/sc/5.5/skills/provision-demo/SKILL.md`, and register `sc@sc-claude-tools` in `~/.claude/settings.json` under `enabledPlugins`. Then tell me to restart Claude Code.

That's it — Claude will handle everything. After restarting, type `/sc:provision-demo` to confirm it's loaded.

> **No `.env` setup needed.** On first run, the skill automatically fetches shared credentials from a private Notion page and writes the `.env` file for you.

> **Hit a blocker or error?** Reach out to Raf Silva on Slack.

---

## Usage

```
/sc:provision-demo Club Brugge https://www.clubbrugge.be
/sc:provision-demo Shopify https://www.shopify.com
/sc:provision-demo Air Canada
```

Claude will:
1. **Research** the prospect via Glean + your Granola meeting notes
2. **Present a plan** — proposed actions, KB focus, conversation topics
3. **Wait for your approval** (you can swap actions, change focus, etc.)
4. **Provision** the bot (~10 min)
5. **Give you the summary** — chat link, API key, Beeceptor dashboard, and suggested questions to ask

---

## Keeping the skill up to date

Paste this into Claude Code:

> Update the `sc:provision-demo` skill — pull the latest from `https://github.com/Rafsilva0/demo_automation` and re-copy `skills/provision-demo/SKILL.md` to `~/.claude/plugins/cache/sc-claude-tools/sc/5.5/skills/provision-demo/SKILL.md`. Then tell me to restart Claude Code.
