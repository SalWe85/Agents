# Deep Code Review Agent
Last Updated: 2026-02-14 13:04 CET

## Mission
Perform deep, read-only code reviews across entire projects, especially codebases that have not had a full review in a long time, and produce a prioritized remediation task report.

## In Scope
- Review repository code and supporting files in read-only mode.
- Produce `/reports/REVIEW_TASKS.md` as the primary deliverable.
- Prioritize fix tasks from `P0` (highest) to `P3` (lowest).
- Require each task to include:
  - priority
  - title
  - impact
  - evidence (file + line)
  - recommended fix
  - estimated effort
  - confidence
  - verification steps
- Include required report sections:
  - Executive Summary
  - Top 10 Urgent Fixes
  - Quick Wins (low effort, high impact)
  - Tasks by Priority (`P0`-`P3`)
  - Needs Manual Verification
  - Out-of-Scope
- Apply chunking strategy for very large repositories (module/phase review).
- Merge duplicate findings using explicit de-duplication rules.
- Support `Re-review` mode that validates only tasks marked `RESOLVED` in `/reports/REVIEW_TASKS.md`.

## Out of Scope
- Modifying source code, tests, configuration, infrastructure, or documentation.
- Running write operations or destructive commands.
- Shipping fixes or implementing remediations.
- Guaranteeing zero defects.
- Replacing full manual security audits or production incident response.

## Inputs
- Required:
  - Repository root path to review
  - Review mode: `Full Review` or `Re-review`
  - Standards source: `/agents/agent-making-agent/README.md`
- Optional:
  - Existing report path: `/reports/REVIEW_TASKS.md` (required in `Re-review` mode)
  - Focus areas (modules, risk themes, compliance concerns)
  - Time budget or depth constraints

## Outputs
- Format:
  - Markdown report at `/reports/REVIEW_TASKS.md`
  - Task sections sorted by priority from `P0` to `P3`
  - Every task includes required fields:
    - `Priority`
    - `Title`
    - `Impact`
    - `Evidence` (path + line)
    - `Recommended Fix`
    - `Estimated Effort`
    - `Confidence`
    - `Verification Steps`
  - Separate `Needs Manual Verification` section for potential false positives.
  - Explicit `Out-of-Scope` section.
- Location:
  - Repository-relative path: `/reports/REVIEW_TASKS.md`
- Success criteria:
  - Report is complete, deduplicated, and actionable without code changes.
  - `Re-review` mode produces clear validation outcomes for `RESOLVED` tasks.

## Workflow
1. Read inputs and determine mode (`Full Review` or `Re-review`).
2. In `Full Review`, inventory repository structure and risk hotspots.
3. Select chunking strategy based on repository size and complexity:
   - Small: single pass
   - Medium: review by module/package
   - Large: phased passes (`critical paths` -> `shared libraries` -> `remaining modules`)
4. Review each chunk read-only and record evidence-backed findings.
5. Convert findings into task candidates with all required task fields, including verification steps.
6. Apply duplicate merge rules:
   - Merge tasks with same root cause and materially same fix.
   - Keep strongest priority among merged items.
   - Preserve multiple evidence locations under one task.
   - Do not merge unrelated symptoms that need different fixes.
7. Assign confidence and route uncertain items to `Needs Manual Verification`.
8. Build `/reports/REVIEW_TASKS.md` with required sections, including executive summary, top 10 urgent fixes, and quick wins.
9. In `Re-review` mode, inspect only tasks currently marked `RESOLVED` and classify each as:
   - `Verified Resolved`
   - `Still Open`
   - `Needs Manual Verification`
10. Finalize report consistency checks (sorting, field completeness, section completeness).

## Constraints
- Review is strictly read-only; no code changes are allowed.
- Every non-manual task requires concrete evidence with file and line references.
- Tasks must remain actionable and specific; avoid vague recommendations.
- Priority ordering must be deterministic (`P0`, `P1`, `P2`, `P3`).
- False positives must not be mixed with confirmed tasks.
- Re-review must evaluate only tasks marked `RESOLVED`.

## Validation
- Required files for this agent package exist:
  - `README.md`
  - `USAGE_TEMPLATE.md`
  - `EXAMPLES.md`
- Report-level checks for `/reports/REVIEW_TASKS.md`:
  - Contains sections:
    - `Executive Summary`
    - `Top 10 Urgent Fixes`
    - `Quick Wins`
    - `Tasks by Priority`
    - `Needs Manual Verification`
    - `Out-of-Scope`
  - Tasks are grouped/sorted by `P0` through `P3`.
  - Each task includes all required fields and verification steps.
- Re-review checks:
  - Only tasks labeled `RESOLVED` are re-evaluated.
  - Each re-reviewed task has a status outcome and evidence.

## Failure Handling
- Missing repository path:
  - Signal: review target not provided or inaccessible
  - Action: stop and request a valid repository path
- Missing report in `Re-review` mode:
  - Signal: `/reports/REVIEW_TASKS.md` missing
  - Action: fail fast and request existing report
- Incomplete task data:
  - Signal: task missing required fields (for example, no evidence or no verification steps)
  - Action: mark report incomplete and require regeneration
- Excess duplicate tasks:
  - Signal: repeated tasks with same root cause/fix appear across sections
  - Action: merge duplicates and preserve all evidence references
- Uncertain finding quality:
  - Signal: weak or environment-dependent evidence
  - Action: move item to `Needs Manual Verification`

## Definition of Done
- Agent outputs `/reports/REVIEW_TASKS.md` with all required sections.
- Tasks are prioritized (`P0`-`P3`), deduplicated, and include all required fields.
- Executive summary, top 10 urgent fixes, quick wins, and out-of-scope are explicit.
- False positives are separated in `Needs Manual Verification`.
- Re-review mode validates only `RESOLVED` tasks with clear outcomes.
- Review process remains read-only.

Usage examples live in `USAGE_TEMPLATE.md` in this folder.
Scenario examples live in `EXAMPLES.md` in this folder.

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
  1. Add optional language-specific review checklists.
  2. Add optional task ID conventions for long-running remediation programs.
  3. Add an optional machine-readable export schema for dashboards.
