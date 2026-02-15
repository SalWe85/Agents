# Figma MCP

## Purpose
Connect Codex to Figma design data (nodes, metadata, screenshots, variables, assets).

## Prerequisites
- Figma access to the target file(s)
- MCP server configured in Codex MCP config
- Valid auth configured for your server version (OAuth or API token)

## Setup Notes
- Keep credentials out of git; use environment variables.
- If access fails, verify file permissions in Figma first.
- If the server was just configured, restart Codex before retesting.

## Validation
- Run a simple MCP check (for example: whoami/list metadata on a known node).
- Confirm expected account is returned.
- Confirm a known file key/node ID can be read.

## Common Failure Modes
- Auth token type mismatch (OAuth vs personal token)
- Wrong file key/node ID format
- Server not loaded because Codex was not restarted
