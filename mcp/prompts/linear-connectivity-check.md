Use Linear MCP to validate connectivity for this environment.

Inputs:
- team_query: <team key or name>
- issue_query: <optional issue id>

Required output:
1. Auth check result (current user)
2. Team/list query result
3. PASS/FAIL conclusion
4. If FAIL: exact blocker and next fix step

Constraint:
- No write operations during connectivity check.
