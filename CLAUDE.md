# Claude Code Context

This repo contains Claude Code plugins for the SC (Solutions Consulting) team at Ada.

## Plugin Structure

```
plugins/sc/skills/                     ← all skills live here
plugins/sc/.claude-plugin/plugin.json  ← plugin manifest (bump version when adding skills)
.claude-plugin/marketplace.json        ← marketplace registration
```

## Installing as a Teammate (full setup)

```bash
# 1. Install Claude Code
brew install node
npm install -g @anthropic-ai/claude-code

# If `claude` is not found after install, fix PATH:
echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc

# 2. Launch Claude Code and log in
claude   # sign in when prompted, then exit with /exit

# 3. Set up GitHub auth (needed for private repo)
brew install gh
gh auth login

# 4. Clone the repo (provision.py runs locally)
git clone https://github.com/AdaSupport/build_ada_agent.git ~/Documents/GitHub/build_ada_agent
cd ~/Documents/GitHub/build_ada_agent && pip install -r requirements.txt && playwright install chromium

# 5. Install the plugin — run this inside Claude Code:
/plugin marketplace add AdaSupport/build_ada_agent
# Then restart Claude Code
```

## Testing Local Changes

```bash
claude --plugin-dir ./plugins/sc
```

## Adding a New Skill

When the user asks to create a new skill or add a tool for the SC team:

1. Copy `plugins/sc/skills/_template/SKILL.md` into a new directory: `plugins/sc/skills/<skill-name>/SKILL.md`
2. Fill in the frontmatter:
   ```yaml
   ---
   name: skill-name
   description: One sentence — what it does and when to use it.
   require-tools:
     - Bash
     - mcp__claude_ai_Notion*    # add any MCP tools the skill needs
   ---
   ```
3. Write the skill instructions in markdown below the frontmatter.
   - Be explicit about prerequisites (repos, env vars, credentials)
   - Include step-by-step logic the LLM should follow
   - Include example invocations
4. Bump the version in `plugins/sc/.claude-plugin/plugin.json` (increment minor, e.g. `1.0` → `1.1`)
5. Update the **Available Skills** table in this file and in `README.md`
6. Commit and push to both remotes:
   ```bash
   git add plugins/ README.md CLAUDE.md
   git commit -m "feat(skills): add <skill-name> skill"
   git push origin main && git push public main
   ```

Teammates who already have the plugin installed will get the new skill automatically on next Claude Code reload (or `/plugin update sc`).

## MCP Tool Naming

claude.ai connector tools follow the pattern `mcp__claude_ai_<Name>__<tool>`:
- Glean: `mcp__claude_ai_Glean*`
- Granola: `mcp__claude_ai_Granola*`
- Notion: `mcp__claude_ai_Notion*`
- Slack: `mcp__claude_ai_Slack*`

Use these in `require-tools` — never hardcode UUID-based tool IDs as they are machine-specific.

## Available Skills

| Skill | Invocation | Description |
|-------|-----------|-------------|
| build-ada-agent | `/sc:build-ada-agent` | Provision a full Ada AI agent demo from a company name + website |
