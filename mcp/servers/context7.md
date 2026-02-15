# Context7 MCP

## Purpose
Provide latest, version-aware framework/library documentation to reduce implementation drift and hallucinated APIs.

## When To Use
- Introducing a new library/framework not already used in the project.
- Performing major version upgrades.
- Implementing unfamiliar APIs where correctness depends on current docs.

## Prerequisites
- Context7 MCP server configured in Codex MCP config.
- Optional API key if your Context7 access tier requires it.

## Setup Notes
- Add `context7` server entry from `/mcp/templates/mcp-config.example.toml`.
- Keep secrets out of git.
- Restart Codex after setup/config changes.

## Validation
- Resolve a known library identifier.
- Fetch docs for a concrete topic/version.
- Confirm response includes actionable API guidance for the selected version.

## Common Failure Modes
- Server not loaded because Codex was not restarted.
- Missing API key on plans requiring auth.
- Vague library query producing wrong package match.
