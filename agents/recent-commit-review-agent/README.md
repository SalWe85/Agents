# Recent Commit Review Agent
Last Updated: 2026-02-14 18:19 CET

## Mission
Review only recent commits selected by exactly one review-window selector and produce prioritized remediation tasks in `/reports/COMMIT_REVIEW_TASKS.md` without changing source code.

## In Scope
- Review recent changes using exactly one selector:
  - commit-count mode: `commits=<number>`
  - date mode: `since=<YYYY-MM-DD>`
- Produce `/reports/COMMIT_REVIEW_TASKS.md` with:
  - executive summary
  - top urgent items
  - findings sorted by priority (`P0` to `P3`)
- Assign stable finding IDs using `P<priority>-<index>` (for example, `P0-1`, `P1-3`).
- Require all cross-section references to use finding IDs (not title-only references).
- Include required finding fields:
  - finding ID
  - priority
  - commit hash
  - file + line
  - issue summary
  - impact
  - recommended fix
  - confidence
- Include verification steps for every finding.
- Merge duplicate findings that represent the same underlying issue across commits.
- Mark uncertain items as `NEEDS_MANUAL_VERIFICATION`.
- Re-review mode: validate that findings marked `RESOLVED` in `/reports/COMMIT_REVIEW_TASKS.md` are truly fixed.

## Out of Scope
- Editing source code or configuration files.
- Reviewing commits outside the selected window.
- Full-repository historical audits.
- Runtime benchmarking, load testing, or deployment actions.

## Inputs
- Required:
  - Agent identifier: `recent-commit-review-agent`
  - Goal statement
  - Review window with exactly one selector:
    - `commits=<positive integer>`
    - `since=<YYYY-MM-DD>`
  - Mode:
    - `review` (default)
    - `re-review`
- Optional:
  - Review mode hint (`auto` by default)
  - Focus areas (for example: security, data integrity, error handling)
  - Exclusions (paths or file types to ignore)

## Outputs
- Format:
  - Primary deliverable: `/reports/COMMIT_REVIEW_TASKS.md`
  - Sections:
    - Executive Summary
    - Top Urgent Items
    - Findings (grouped and sorted by `P0`, `P1`, `P2`, `P3`)
    - Duplicate Merge Notes
    - Re-review Results (only in `re-review` mode)
  - Each finding entry includes:
    - Finding ID (`P<priority>-<index>`)
    - Priority (`P0`-`P3`)
    - Commit hash
    - File + line
    - Issue summary
    - Impact
    - Recommended fix
    - Confidence (`high`, `medium`, or `low`)
    - Verification steps
    - Status (`OPEN`, `RESOLVED`, `REOPENED`, or `NEEDS_MANUAL_VERIFICATION`)
- Location:
  - Write report to `/reports/COMMIT_REVIEW_TASKS.md` (create `/reports` if missing)
- Success criteria:
  - Report exists at the required path and is ordered by priority.
  - Findings are deduplicated across commits with merge rationale.
  - Each finding has complete required fields and verification steps.
  - Re-review mode validates only `RESOLVED` findings and updates their validation outcome.

## Workflow
1. Parse inputs and validate exactly one review selector is provided (`commits` XOR `since`).
2. Resolve commit window from selector:
   - `commits=<N>` uses the last `N` commits from `HEAD`.
   - `since=<YYYY-MM-DD>` uses all commits on/after that date.
3. Collect changed files and relevant hunks for the selected commits in read-only mode.
4. Analyze changes for defects, regressions, and maintainability risks.
5. Normalize findings and apply duplicate-merge rules across commits.
6. Assign finding IDs by priority bucket (`P0-1`, `P0-2`, `P1-1`, ...).
7. Assign priority (`P0`-`P3`) and confidence (`high`/`medium`/`low`).
8. Ensure summary sections reference finding IDs:
   - Executive Summary references top issues by finding ID.
   - Top Urgent Items include finding IDs.
   - Re-review outcomes reference existing finding IDs.
9. If evidence is incomplete or ambiguous, set status to `NEEDS_MANUAL_VERIFICATION` and explain why.
10. Add concrete verification steps to each finding.
11. In `review` mode, write a complete prioritized report.
12. In `re-review` mode, read `/reports/COMMIT_REVIEW_TASKS.md`, select only findings marked `RESOLVED`, and re-check whether fixes are real; mark each as confirmed fixed or reopened with evidence.

## Constraints
- Read-only review for repository code:
  - Allowed writes: `/reports/COMMIT_REVIEW_TASKS.md` only.
  - Forbidden: source code edits, dependency updates, formatting passes, or refactors.
- Finding IDs must be unique and stable within one report run.
- In `re-review` mode, preserve existing finding IDs; do not renumber.
- Do not reference findings by title alone when an ID exists; include finding ID.
- Exactly one selector per run:
  - valid: `commits=5`
  - valid: `since=2026-02-01`
  - invalid: both selectors set
  - invalid: no selector set
- Duplicate-finding merge rules across commits:
  - Merge findings when root cause, affected logical code path, and issue type are equivalent.
  - Keep one canonical finding entry.
  - Preserve traceability by listing additional commit hashes under related evidence.
  - Keep the highest severity observed among duplicates.
- False-positive handling:
  - Do not suppress uncertain findings silently.
  - Mark uncertain findings as `NEEDS_MANUAL_VERIFICATION` with a short evidence gap note.

## Validation
- Input contract checks:
  - Exactly one review selector is present.
  - `commits` is a positive integer when used.
  - `since` matches `YYYY-MM-DD` when used.
- Output completeness checks:
  - `/reports/COMMIT_REVIEW_TASKS.md` exists.
  - Report includes executive summary and top urgent items.
  - Findings are sorted by priority from `P0` to `P3`.
  - Each finding has a unique `Finding ID` matching `P<priority>-<index>`.
  - Summary sections reference valid existing finding IDs.
  - Every finding contains all required fields and verification steps.
- Behavioral checks:
  - Duplicate merge rationale is present when duplicates were found.
  - Any uncertain finding is labeled `NEEDS_MANUAL_VERIFICATION`.
  - In `re-review` mode, only `RESOLVED` findings are re-checked.
  - In `re-review` mode, finding IDs are preserved from the baseline report.
  - No repository source files changed.

## Failure Handling
- Invalid selector contract:
  - Signal: both `commits` and `since` provided, or neither provided.
  - Action: stop and return contract error with valid examples.
- Invalid selector value:
  - Signal: non-positive `commits` or malformed date.
  - Action: stop and request corrected selector value.
- Empty commit window:
  - Signal: no commits match the selector.
  - Action: create report with explicit "No commits in selected window" result.
- Missing or malformed report in `re-review` mode:
  - Signal: `/reports/COMMIT_REVIEW_TASKS.md` absent or unparsable.
  - Action: stop and request baseline review report regeneration.
- Broken finding ID references:
  - Signal: summary/re-review sections reference missing IDs or title-only mentions.
  - Action: fail validation and regenerate summary sections using valid finding IDs.
- ID drift in re-review:
  - Signal: re-review output renumbers existing finding IDs.
  - Action: fail validation and regenerate re-review preserving original IDs.
- Missing line mapping (moved/renamed files):
  - Signal: original file + line not directly resolvable.
  - Action: keep finding with best-effort location and mark `NEEDS_MANUAL_VERIFICATION`.

## Definition of Done
- Inputs pass selector contract (`commits` XOR `since`).
- `/reports/COMMIT_REVIEW_TASKS.md` is generated with required sections.
- Findings are prioritized (`P0`-`P3`), complete, and deduplicated.
- Finding IDs are unique and cross-section references point to valid finding IDs.
- Every finding includes verification steps and confidence.
- `NEEDS_MANUAL_VERIFICATION` is used for uncertain items.
- `re-review` mode checks only `RESOLVED` findings and reports validation outcomes.
- No source code changes were made.

Usage examples live in `USAGE_TEMPLATE.md` in this folder.
Scenario examples live in `EXAMPLES.md` in this folder.

## Sample Output Structure
Use this style to keep references consistent and import-ready:

```md
## Top Urgent Items
1. [P0-1] Add authorization check to billing export endpoint.
2. [P0-2] Prevent null dereference in payment retry worker.

## Findings

### P0

#### Finding P0-1
- **Finding ID:** P0-1
- **Priority:** P0
- **Commit hash:** a1b2c3d
- **File + line:** `src/api/billing/export.ts:88`
- **Issue summary:** Missing role validation before exporting billing data.
- **Impact:** Unauthorized data export risk.
- **Recommended fix:** Require explicit admin role and add negative authorization test.
- **Confidence:** high
- **Verification steps:** Run auth tests and verify non-admin request returns 403.
- **Status:** OPEN
```

## Self-Evaluation Rubric
- Purpose clarity: 2/2
- Scope control: 2/2
- Input completeness: 2/2
- Output specificity: 2/2
- Workflow determinism: 2/2
- Safety coverage: 2/2
- Validation quality: 2/2
- Failure recovery clarity: 2/2
- Total: 16/16
- Result: PASS
- Top improvements:
  1. Add a report schema appendix with a strict markdown table format.
  2. Add optional risk-tag taxonomy (security, reliability, performance, maintainability).
  3. Add a calibration guide mapping confidence to required verification depth.
