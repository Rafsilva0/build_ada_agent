# Claude Code Skills for Demo Automation

These skills let the SC team run the Ada demo provisioning directly from Claude Code — with automatic prospect research, a customisable plan, and a post-provision summary.

## Skills

| Skill | Description |
|-------|-------------|
| `sc:provision-demo` | Provision a full Ada demo bot from a company name + website |

---

## Installation

### 1. Clone the repo (if you haven't already)

```bash
git clone https://github.com/Rafsilva0/demo_automation.git ~/Documents/GitHub/demo_automation
cd ~/Documents/GitHub/demo_automation
pip install -r requirements.txt
```

### 2. Install the Claude Code skill

Copy the skill into your local Claude plugins cache and register the `sc` plugin namespace:

> **No `.env` setup needed.** On first run, the skill automatically fetches shared credentials from a private Notion page and writes the `.env` file for you.

```bash
SKILLS_DIR=~/.claude/plugins/cache/sc-claude-tools/sc/5.5/skills

# Create the target directory
mkdir -p "$SKILLS_DIR/provision-demo"

# Copy the skill file
cp ~/Documents/GitHub/demo_automation/skills/provision-demo/SKILL.md \
   "$SKILLS_DIR/provision-demo/SKILL.md"

# Register the sc plugin with Claude Code (required — otherwise the skill is invisible)
node -e "
  const fs = require('fs'), p = require('os').homedir() + '/.claude/settings.json';
  const s = JSON.parse(fs.readFileSync(p, 'utf8'));
  if (!s.enabledPlugins) s.enabledPlugins = {};
  s.enabledPlugins['sc@sc-claude-tools'] = true;
  fs.writeFileSync(p, JSON.stringify(s, null, 2));
  console.log('Done — sc@sc-claude-tools registered.');
"
```

> **Note:** You only need to do this once. To update the skill in future, just re-run the copy command after pulling the latest changes.

### 3. Restart Claude Code

Quit and reopen Claude Code so it picks up the new skill. Verify it's loaded by typing `/sc:provision-demo` — you should see it in autocomplete.

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

> **Hit a blocker or error?** Reach out to Raf Silva on Slack.

---

## Keeping the skill up to date

When the skill is updated in this repo, pull and re-copy:

```bash
cd ~/Documents/GitHub/demo_automation
git pull

cp skills/provision-demo/SKILL.md \
   ~/.claude/plugins/cache/sc-claude-tools/sc/5.5/skills/provision-demo/SKILL.md
```

Then restart Claude Code.
