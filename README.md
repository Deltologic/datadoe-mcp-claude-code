# DataDoe MCP + Claude Code CLI Template

This repository is a minimal example of using the DataDoe MCP server from Claude Code CLI for Amazon-focused workflows.

## Table of Contents

- [What you can do with this repo](#what-you-can-do-with-this-repo)
- [What This Repo Includes](#what-this-repo-includes)
- [Prerequisites](#prerequisites)
- [How to get a DataDoe subscription and get MCP Key](#how-to-get-a-datadoe-subscription-and-get-mcp-key)
- [Configure DataDoe MCP in Claude Code CLI](#configure-datadoe-mcp-in-claude-code-cli)
- [Run Claude Code from Dedicated Launcher](#run-claude-code-from-dedicated-launcher)
- [Claude Settings (Official Model)](#claude-settings-official-model)
- [Example prompt library starter pack](#example-prompt-library-starter-pack)
- [DataDoe MCP Configuration Options](#datadoe-mcp-configuration-options)
- [Validation Checklist](#validation-checklist)
- [How to get help](#how-to-get-help)
- [Recommended repository cleanup](#recommended-repository-cleanup)
- [Tags](#tags)

## What you can do with this repo

- Connect Claude Code CLI to DataDoe MCP in a secure way.
- Ask Amazon seller questions using DataDoe-backed data.
- Reuse this setup as a template for new Amazon-focused assistant projects.

## What This Repo Includes

- Claude Code MCP setup guidance for a project-scoped `datadoe` server
- secure secret handling with `.env` and `.env.example`
- repository-specific assistant rules in `.claude/CLAUDE.md`
- validation checks to confirm integration is working

## Prerequisites

- Claude Code CLI installed and working (`claude --version`)
- A valid DataDoe subscription
- A generated DataDoe MCP key

If `claude --version` shows nothing or `claude` is not found, install and verify Claude Code CLI:

```bash
npm install -g @anthropic-ai/claude-code
hash -r
claude --version
```

If the command is still not found, add npm global binaries to your shell `PATH` (for `zsh`):

```bash
echo 'export PATH="$(npm config get prefix)/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
which claude
claude --version
```

## How to get a DataDoe subscription and get MCP Key

1. Go to [app.datadoe.com](https://app.datadoe.com).
2. Create an account.
3. Purchase a subscription.
4. Accept the Terms and Conditions and Privacy Policy.
5. Go to the `Integrations` module.
6. Click the `MCP` tile (this navigates to `/integrations/mcp`).
7. Click `MCP Key`, then add a name and expiration date, and click `Create`.
8. Copy the key and store it in a secure secret manager or another safe location.

## Configure DataDoe MCP in Claude Code CLI

Add DataDoe MCP with CLI command:

```bash
claude mcp add datadoe https://api.datadoe.com/mcp/v1 --transport http --scope project --header "datadoe-mcp-key: YOUR_API_KEY"
```

What this does:

- adds a project-scoped MCP server named `datadoe`
- creates/updates `.mcp.json` for shared project configuration
- keeps setup consistent for all collaborators

Reference: [Claude Code MCP docs](https://code.claude.com/docs/en/mcp)

## Run Claude Code from Dedicated Launcher

This repository includes a dedicated launcher script:

> [!WARNING] > `scripts/start-claude.sh` is the protected launcher for this repository.
> Do not edit, replace, or "quick fix" it unless you are intentionally changing launcher behavior.

```bash
./scripts/start-claude.sh
```

The launcher loads `.env`, exports `DATADOE_MCP_KEY` into the current process, and then starts Claude Code CLI from the repository root.

Short manual:

```bash
# Interactive menu (recommended)
./scripts/start-claude.sh

# Direct launch Claude Code CLI
./scripts/start-claude.sh --cli

# Validate env loading + Claude CLI availability only
./scripts/start-claude.sh --check

# Help
./scripts/start-claude.sh --help
```

If needed, make it executable once:

```bash
chmod +x ./scripts/start-claude.sh
```

## Claude Settings (Official Model)

Per the [Claude settings docs](https://code.claude.com/docs/en/settings), Claude Code supports multiple configuration scopes:

- **User scope**: `~/.claude/settings.json` (your personal defaults across all repos)
- **Project scope**: `.claude/settings.json` (shared with this repository team)
- **Local scope**: `.claude/settings.local.json` (personal overrides for this repo, not shared)
- **Project memory/instructions**: `.claude/CLAUDE.md` (team-shared assistant guidance)
- **Project MCP servers**: `.mcp.json` (team-shared MCP server definitions)

Precedence (high to low): managed settings, CLI args, local project settings, shared project settings, user settings.

Recommended workflow:

1. Use `/config` inside Claude Code to create or edit settings files safely.
2. Keep team-wide settings in `.claude/settings.json`.
3. Keep personal overrides in `.claude/settings.local.json`.
4. Use `/status` to verify active settings sources and resolve config issues.

Example shared project settings (`.claude/settings.json`) with schema and basic safety defaults:

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "permissions": {
    "deny": ["Read(./.env)", "Read(./.env.*)"]
  }
}
```

## Example prompt library starter pack

To help you start faster with an AI Agent + DataDoe MCP workflow, this repo includes a small prompt library at:

- `.claude/prompts/EXAMPLES.md`

Use it as a starter pack:

1. Open `.claude/prompts/EXAMPLES.md`.
2. Copy a prompt block and adjust placeholders (for example `{{seller_name}}`) to your account context.
3. Run the prompt in Claude Code CLI chat with DataDoe MCP enabled.
4. Save your own high-performing prompts in the same file to build a reusable internal playbook.

## DataDoe MCP Configuration Options

You can configure DataDoe MCP in either of these ways.

Option A: repository-managed `.mcp.json` (recommended for teams):

```json
{
  "mcpServers": {
    "datadoe": {
      "type": "http",
      "url": "https://api.datadoe.com/mcp/v1",
      "headers": {
        "datadoe-mcp-key": "${DATADOE_MCP_KEY}"
      }
    }
  }
}
```

Option B: add by CLI command (writes/updates `.mcp.json`):

```bash
claude mcp add datadoe https://api.datadoe.com/mcp/v1 --transport http --scope project --header "datadoe-mcp-key: YOUR_API_KEY"
```

If you use `${DATADOE_MCP_KEY}` in `.mcp.json`, ensure your shell has this variable set before starting Claude Code (the launcher does this automatically by loading `.env`).

> [!CAUTION]
> Treat `DATADOE_MCP_KEY` like a password. Do not publish repositories, screenshots, or logs that contain this key.
> Never commit real keys to git.
> If a key is exposed, rotate it immediately.

## Validation Checklist

- `.env` is ignored by Git.
- `.env.example` is tracked by Git.
- `.claude/CLAUDE.md` exists.
- `claude mcp list` shows `datadoe`.
- `/mcp` inside Claude Code CLI shows the server as available.

## How to get help

- Email: [contact@datadoe.com](mailto:contact@datadoe.com)
- Claude Code MCP Setup [docs](https://code.claude.com/docs/en/mcp)
- Claude Code Docs [docs](https://code.claude.com/docs/en/overview)
- Claude Code CLI reference [cli-reference](https://code.claude.com/docs/en/cli-reference)
