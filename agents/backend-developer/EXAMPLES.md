# Examples

Use these as starting points. Review and adapt stack source, branch strategy, and validation commands to your repository conventions.

## Example 1: Backend Feature Implementation with Stack File Present

### Input
```text
Agent: backend-developer
Goal: Add pagination and filtering to the transactions endpoint.
Inputs: task_identifier: AG-312
Inputs: repo_root: /workspace/ledger-api
Inputs: default_branch: main
Inputs: acceptance_criteria: Endpoint supports page, pageSize, status filter, and keeps response backward compatible.
Inputs: stack_file_path: /workspace/ledger-api/STACK.md
Inputs: task_list_path: /workspace/ledger-api/reports/SPRINT_EXECUTION_LOG.md
Inputs: linear_issue_id: LED-312
Inputs: linear_workflow_path: /Users/slobodan/Projects/Agents/agents/_shared/LINEAR_WORKFLOW.md
Inputs: worktree_policy_path: /Users/slobodan/Projects/Agents/agents/_shared/WORKTREE_POLICY.md
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Commit messages must include AG-312.
- Run lint/test/build checks.
Output:
- Code changes + status updates + validation summary.
```

### Expected Output
```text
Creates/switches to branch codex/ag-312-transactions-pagination from main.
Implements endpoint changes and related tests.
Runs lint/test/build commands from stack file guidance.
Updates /reports/SPRINT_EXECUTION_LOG.md substatus to codex_dev_done.
Hands off to backend-tester with explicit changed-file scope.
Creates task-scoped commits with AG-312 in commit messages.
Pushes task branch before Linear update.
Updates Linear issue LED-312 to testing-ready status with handoff comment containing branch + commit.
```

## Example 2: Ambiguous Stack Detection Requiring User Choice

### Input
```text
Agent: backend-developer
Goal: Add rate limiting to authentication endpoints.
Inputs: task_identifier: SEC-77
Inputs: repo_root: /workspace/auth-service
Inputs: default_branch: develop
Inputs: acceptance_criteria: Login and token refresh endpoints enforce per-IP and per-account limits.
Inputs: stack_file_path:
Inputs: task_list_path: /workspace/auth-service/reports/SPRINT_EXECUTION_LOG.md
Inputs: commit_mode: commit
Constraints:
- Implement changes directly.
- Ask for user choice if stack/tooling ambiguity affects implementation path.
- Run lint/test/build checks.
Output:
- Code changes + status updates + validation summary.
```

### Expected Output
```text
Inspects repository and detects multiple plausible stack paths (for example Express middleware vs API gateway policy).
Returns recommended option and prompts user to choose implementation path before editing code.
After user decision, creates/switches task branch from develop, implements selected path, and runs validations.
Updates task list status to codex_dev_done and hands off to backend-tester.
Commits only SEC-77 scoped changes with SEC-77 in commit messages.
Pushes task branch and then updates Linear/testing handoff if linear_issue_id is provided.
```
