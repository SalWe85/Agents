# Using Worktrees And Agent Threads

Quick findings for using Codex threads with git worktrees.

## Core Rules

- Prefer `Fork into new worktree` when creating a new agent thread.
- Do not rely on switching an existing thread to a different worktree if you need restart-stable context.
- If you want to keep threads under the same project context, stay in local/main thread flow.

## Why Fork Is Better

- Fork creates a dedicated worktree + thread pairing.
- Forked threads are more reliable across app restarts.
- A fork indicator in the navbar helps confirm you are in isolated context.
- Forked threads inherit context from the source thread at fork time.
- For subagent execution, fork from a lightweight launcher thread when possible to keep inherited context clean.

## Detached HEAD Notes

- A new worktree can open in detached HEAD.
- Detached HEAD is valid, but risky for orphan commits.
- Before edits, attach a branch: `git switch -c codex/<task-name>`.
- If asked to commit, the agent will handle branch safety, but users should still verify branch state.

## Cleanup and Safety

- Archiving a thread does not delete its worktree.
- Deleting a worktree while a thread is attached can break that thread's live workspace context.
- Move thread to another valid workspace before deleting its worktree.
- Deleting a worktree does not delete committed branch history.
- Uncommitted changes in a deleted worktree are lost.

## Broken Thread Context After Worktree Deletion

- If a thread's attached worktree path is deleted, thread UI actions can break.
- Typical broken UI actions: `handoff to local`, `branch here`, worktree-aware branch widgets.
- Conversation still works, but workspace-aware UI controls may fail because their anchor path is gone.
- Agent shell commands can still work only if a valid `workdir` is set explicitly.
- Practical recovery: start a new thread in a valid repo path (or fork from a valid thread/workspace) and continue there.
- Keep deleted-path threads as read-only history, then archive them.
- Prevention: never delete a worktree that still has an active thread attached.
- Clean worktrees only when the related thread is done and ready to be archived.

## Recommended Team Workflow

1. Start from main project workspace.
2. Keep one lightweight launcher thread for spawning subagent forks.
3. Use `Fork into new worktree` from that lightweight thread per parallel task.
4. Keep heavy planning/orchestrator threads separate from subagent execution forks.
5. Ensure each forked worktree is on a named branch.
6. Commit/push work.
7. Delete stale worktrees only after commits are safe and thread context is moved.

## AGENTS.md vs Skills vs MCP (And This Repo's Approach)

- `AGENTS.md`: instruction policy and context loading.
  - It defines how Codex behaves in a repo (rules, preferences, constraints).
  - It can be layered globally and per project.
  - Docs: [Custom instructions with AGENTS.md](https://developers.openai.com/codex/guides/agents-md)

- Skills: reusable capability packs (`SKILL.md` plus optional scripts/resources).
  - They define how Codex performs a specific type of task.
  - They can trigger explicitly or by matching task intent.
  - Docs: [Agent Skills](https://developers.openai.com/codex/skills/)

- MCP: protocol/server integration layer.
  - It gives Codex tools and context from external systems (for example docs, browser tools, Figma, Sentry).
  - Docs: [Model Context Protocol (MCP)](http://developers.openai.com/codex/mcp)

### How This Repo Differs

- This repo uses local "agent definitions" under `/agents` as a hybrid model:
  - policy + workflow contract + reusable templates in one place
  - explicit invocation by prompt
  - per-run customization through inputs
- These local agents are project-scoped, not globally auto-applied.
- This is intentional: it avoids hidden global behavior and keeps execution predictable per project/thread.
