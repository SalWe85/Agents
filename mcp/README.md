# MCP Portability Pack

This folder makes MCP usage portable across projects and teammates.

## What Is Portable
- Server onboarding docs
- Config templates
- Prompt templates for MCP-enabled runs
- Validation checklists

## What Is Not Portable
- Real API/OAuth tokens
- Personal auth state
- Local app runtime state

## Relationship To Skills
- Skills describe workflows and when to use tools.
- MCP provides tool access to external systems.
- Some skills require MCP servers to be configured.

## Recommended Baseline Servers
- `figma`: design metadata/screenshots/assets
- `linear`: issue/project operations
- `context7`: latest version-aware library/framework docs

## Folder Layout
- `servers/`: server-specific setup and troubleshooting
- `templates/`: config templates (no secrets)
- `checklists/`: onboarding and verification steps
- `prompts/`: reusable prompts for MCP-enabled agent runs

## Usage
1. Copy template config values from `templates/mcp-config.example.toml` into your Codex MCP config.
2. Set tokens via environment variables or local config values (never commit secrets).
3. Restart Codex.
4. Verify access using prompts from `prompts/`.

## Security Rules
- Never commit real tokens to this repository.
- Keep only `.example` config files in version control.
