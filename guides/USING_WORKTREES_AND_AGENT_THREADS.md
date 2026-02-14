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

## Recommended Team Workflow

1. Start from main project workspace.
2. Keep one lightweight launcher thread for spawning subagent forks.
3. Use `Fork into new worktree` from that lightweight thread per parallel task.
4. Keep heavy planning/orchestrator threads separate from subagent execution forks.
5. Ensure each forked worktree is on a named branch.
6. Commit/push work.
7. Delete stale worktrees only after commits are safe and thread context is moved.
