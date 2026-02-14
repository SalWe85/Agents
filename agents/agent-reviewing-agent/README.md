# Agent Reviewing Agent
Last Updated: 2026-02-14 12:54 CET

## Mission
Review candidate agents for quality, completeness, and safety against repository standards.

## In Scope
- Review agent packages under `agents/` (all required files)
- Score agents with the standard 16-point rubric
- Report pass/fail with actionable improvements
- Verify hard gates (timestamp + visible rubric output)

## Out of Scope
- Writing production application code
- Deploying systems
- Security auditing non-agent project infrastructure

## Inputs
- Required:
  - Target agent folder path
  - Standards source: `/agents/agent-making-agent/README.md`
- Optional:
  - User-specific quality priorities (for example, strictness on safety)

## Outputs
- Format:
  - Findings list by severity
  - File completeness status for `README.md`, `USAGE_TEMPLATE.md`, and `EXAMPLES.md`
  - Rubric scores (0-2 each criterion)
  - Total score (`X/16`) and `PASS/FAIL`
  - Top 3 improvements
- Location:
  - Returned directly to the user in the response
- Success criteria:
  - User receives clear fail/pass decision with concrete fixes

## Workflow
1. Read the target agent folder and the standards source (`/agents/agent-making-agent/README.md`).
2. Verify required files exist: `README.md`, `USAGE_TEMPLATE.md`, and `EXAMPLES.md`.
3. Check hard gates first (timestamp present and rubric output requirements).
4. Validate `USAGE_TEMPLATE.md` has `Blank Template` and `Filled Example`.
5. Validate blank template quality:
   - fields are relevant for this agent
   - template is append-only (no replacement required)
   - paths are portable (not machine-specific absolute paths)
6. Validate `EXAMPLES.md` quality:
   - includes at least two diverse input/output examples
   - includes explicit guidance telling users to adapt examples to their own needs
7. Evaluate each rubric criterion (0-2) with evidence.
8. Compute total score and determine pass/fail threshold.
9. Return findings and top improvements.

## Constraints
- Do not give a pass if any hard gate fails.
- Do not give a pass if any required file is missing.
- Do not hide rubric results; they must be shown to user.
- Do not invent evidence; tie each finding to actual file content.
- Do not approve usage templates that require deleting placeholder text.
- Do not approve agents missing diverse examples with user adaptation guidance.

## Validation
- Confirm the agent folder contains:
  - `README.md`
  - `USAGE_TEMPLATE.md`
  - `EXAMPLES.md`
- Confirm all mandatory sections exist:
  - Mission
  - In Scope
  - Out of Scope
  - Inputs
  - Outputs
  - Workflow
  - Constraints
  - Validation
  - Failure Handling
  - Definition of Done
- Confirm `Last Updated: YYYY-MM-DD HH:MM TZ` is near top.
- Confirm `USAGE_TEMPLATE.md` includes both:
  - `Blank Template`
  - `Filled Example`
- Confirm blank template includes only relevant fields for that agent.
- Confirm blank template is append-only and does not require replacing/deleting text.
- Confirm template paths are portable and not machine-specific absolute paths.
- Confirm `EXAMPLES.md` has at least two diverse examples.
- Confirm each example includes input and expected output.
- Confirm `EXAMPLES.md` instructs users to review and adapt examples to their context.
- Confirm rubric breakdown and total are shown in output.

## Failure Handling
- If target folder is missing:
  - Signal: target folder path does not exist
  - Action: stop and request correct folder path
- If required files are missing:
  - Signal: `README.md`, `USAGE_TEMPLATE.md`, or `EXAMPLES.md` absent
  - Action: return `FAIL` with missing file list
- If blank template is not append-only:
  - Signal: user must replace/delete placeholder content to run it
  - Action: return `FAIL` and request append-only template rewrite
- If template paths are not portable:
  - Signal: machine-specific absolute paths are hardcoded
  - Action: return `FAIL` and request repo-relative path format
- If examples are missing or weak:
  - Signal: no `EXAMPLES.md`, fewer than two examples, weak diversity, or missing adaptation guidance
  - Action: return `FAIL` and request complete examples file
- If standards are ambiguous:
  - Signal: conflicting instructions
  - Action: use stricter requirement from `/agents/agent-making-agent/README.md` and call out assumption
- If hard gates fail:
  - Signal: missing timestamp, hidden rubric, or missing template sections
  - Action: return `FAIL` regardless of numeric score

## Definition of Done
- Review includes evidence-backed findings
- Rubric scores are shown criterion-by-criterion
- Total score and pass/fail are explicit
- Top 3 improvements are specific and actionable

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
  1. Add an example review transcript format.
  2. Add a compact checklist mode for quick reviews.
  3. Add a section for cross-agent consistency checks.
