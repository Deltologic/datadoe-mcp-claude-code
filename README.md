# DataDoe MCP + Claude Code CLI Template

This repository is a starter template for integrating DataDoe MCP with Claude Code CLI in a secure, team-friendly way.

## Table of Contents

- [What This Repo Includes](#what-this-repo-includes)
- [Prerequisites](#prerequisites)
- [Get DataDoe Subscription and MCP Key](#get-datadoe-subscription-and-mcp-key)
- [Configure DataDoe MCP in Claude Code CLI](#configure-datadoe-mcp-in-claude-code-cli)
- [Claude Settings (Official Model)](#claude-settings-official-model)
- [Optional `.mcp.json` Structure](#optional-mcpjson-structure)
- [Validation Checklist](#validation-checklist)
- [How to get help](#how-to-get-help)
- [Recommended repository cleanup](#recommended-repository-cleanup)
- [Tags](#tags)

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

## Get DataDoe Subscription and MCP Key

1. Go to [app.datadoe.com](https://app.datadoe.com)
2. Create account
3. Purchase subscription
4. Accept Terms and Conditions and Privacy Policy
5. Go to `Integrations`
6. Click `MCP` tile (`/integrations/mcp`)
7. Click `MCP Key`, add name + expiration, click `Create`
8. Copy key and store in a secure secret manager

## Configure DataDoe MCP in Claude Code CLI

Run this exact command:

```bash
claude mcp add --transport http --scope project --header "datadoe-mcp-key: YOUR_API_KEY" datadoe "https://api.datadoe.com/mcp/v1?"
```

What this does:

- adds a project-scoped MCP server named `datadoe`
- creates/updates `.mcp.json` for shared project configuration
- keeps setup consistent for all collaborators

Reference: [Claude Code MCP docs](https://code.claude.com/docs/en/mcp)

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

## Optional `.mcp.json` Structure

You can keep this repo-managed structure (already provided in this repo):

```json
{
  "mcpServers": {
    "datadoe": {
      "type": "http",
      "url": "https://api.datadoe.com/mcp/v1?",
      "headers": {
        "datadoe-mcp-key": "${DATADOE_MCP_KEY}"
      }
    }
  }
}
```

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

## Recommended repository cleanup

For each repository using this template, keep settings lean:

- Disable GitHub Wiki if not used.
- Disable GitHub Projects if not used.
- Disable Discussions if not used.
- Keep branch protection minimal but enabled for your main branch.
- Do not commit `.env` or real API keys.

## Tags

`DataDoe` `MCP` `Anthropic` `Claude Code` `Amazon` `Amazon Seller` `AI Assistant` `LLM` `Prompting` `E-Commerce` `Online Marketplaces`
