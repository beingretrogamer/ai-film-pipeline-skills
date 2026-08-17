# Install

## Quick (recommended)

```bash
npx skills add /path/to/ai-film-pipeline-skills
```

Or from GitHub once published:

```bash
npx skills add beingretrogamer/ai-film-pipeline-skills
```

## Manual

Copy or symlink the skill folders into your agent’s skills directory:

- Claude Code: `~/.claude/skills/` or project `.claude/skills/`
- Cursor: `.cursor/skills/` or `~/.cursor/skills/`
- Other agents that follow the agentskills.io standard: follow their documented path

Each skill is a folder containing `SKILL.md`. The folder name must match the `name:` field in the frontmatter.

## Prerequisites for generation stage

```bash
# Higgsfield CLI (current recommended method — check official docs for updates)
curl -fsSL https://raw.githubusercontent.com/higgsfield-ai/cli/main/install.sh | sh
# or
npm install -g @higgsfield/cli

higgsfield auth login
```

# fal.ai
pip install fal-client
export FAL_KEY="your-key"

Pre-production skills (breakdown, passports, stress-test, prompt writing) work without a live generation backend.

## Verify

In your agent, list skills or invoke:

```
/ai-film-pipeline
/film-setup
/studio-init
...
```
