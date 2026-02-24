# Claude Code Skills for Demo Automation

The `build-ada-agent` skill lets the SC team provision Ada demo bots directly from Claude Code — with automatic prospect research, a customisable plan, and a post-provision summary.

## Skill

| Skill | Description |
|-------|-------------|
| `pd:build-ada-agent` | Build a full Ada AI agent demo from a company name + website |

---

## Installation

Run the install script — no GitHub access or prior setup required:

```bash
bash install.sh
```

The script is self-contained: it creates the `ada-demo-tools` plugin, writes the skill, and registers it in Claude Code automatically.

After running, restart Claude Code and type `/pd:build-ada-agent` to confirm it's loaded.

> **No `.env` setup needed.** On first run, the skill automatically fetches shared credentials from a private Notion page and writes the `.env` file for you.

> **Hit a blocker or error?** Reach out to Raf Silva on Slack.

---

## Keeping the skill up to date

Re-run the install script to get the latest version:

```bash
bash install.sh
```

Then restart Claude Code.

---

## Usage

```
/pd:build-ada-agent Club Brugge https://www.clubbrugge.be
/pd:build-ada-agent Shopify https://www.shopify.com
/pd:build-ada-agent Air Canada
```

Claude will:
1. **Research** the prospect via Glean + your Granola meeting notes
2. **Present a plan** — proposed actions, KB focus, conversation topics
3. **Wait for your approval** (you can swap actions, change focus, etc.)
4. **Provision** the bot (~10 min)
5. **Give you the summary** — chat link, API key, Beeceptor dashboard, and suggested questions to ask
