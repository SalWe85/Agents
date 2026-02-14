# Agent Making Agent

Last Updated: 2026-02-14 12:14 CET

## Mission
Define and enforce a minimum quality standard for every new agent in this repository.

## In Scope
- Define mandatory sections all agent READMEs must include
- Provide a scoring rubric for agent quality
- Enforce mandatory hard gates before an agent is accepted
- Require visible rubric output so users can refine agent quality

## Out of Scope
- Implementing application code
- Running production deployments
- Replacing domain-specific technical review

## Inputs
- Required:
  - Candidate agent README content
  - Agent folder path under `agents/`
- Optional:
  - Relevant project constraints
  - Preferred output format for scoring feedback

## Outputs
- Format:
  - Agent acceptance result (`PASS` or `FAIL`)
  - Rubric table with criterion-by-criterion scores
  - Total score and improvement actions
  - Required deliverables check for two-file agent package
- Location:
  - Presented directly to the user in response output
  - Stored in agent README sections where applicable
- Success criteria:
  - Candidate agent includes both required files and passes hard gates and quality threshold

## Workflow
1. Verify the candidate agent package includes `README.md` and `USAGE_TEMPLATE.md`.
2. Verify README includes all required sections.
3. Validate hard gates (timestamp near top and rubric transparency requirements).
4. Validate `USAGE_TEMPLATE.md` has both `Blank Template` and `Filled Example`.
5. Score agent with the quality rubric (0-2 per criterion).
6. Output full scoring breakdown to user, including total and weak areas.
7. If failing, provide targeted revision actions and re-run scoring after edits.

## Constraints
- Do not approve agents missing required sections.
- Do not approve agents that hide or omit rubric output.
- Do not approve agents without a top-of-file freshness timestamp.
- Timestamp must be near top of agent README, directly below title.
- Required timestamp format:
  - `Last Updated: YYYY-MM-DD HH:MM TZ`

## Validation
- Required files exist in each agent folder:
  - `README.md`
  - `USAGE_TEMPLATE.md`
- Required README sections exist:
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
  - `USAGE_TEMPLATE.md` file (blank + filled)
- Hard gates pass:
  - [ ] Agent package includes both required files
  - [ ] Timestamp appears near top of file
  - [ ] Rubric score is computed
  - [ ] Rubric output is shown to user
  - [ ] `USAGE_TEMPLATE.md` exists with blank and filled examples
- Rubric score threshold:
  - Minimum `14/16` to pass

## Failure Handling
- Missing required files:
  - Signal: Agent folder does not contain `README.md` and `USAGE_TEMPLATE.md`
  - Action: Return `FAIL` and list missing files
- Missing required sections:
  - Signal: One or more mandatory sections absent
  - Action: Return `FAIL` with exact missing headings
- Missing timestamp:
  - Signal: No `Last Updated` line near top
  - Action: Return `FAIL` and require insertion before scoring pass
- Rubric not visible to user:
  - Signal: Score calculated internally only
  - Action: Return `FAIL` and require score output publication
- Missing usage template:
  - Signal: No `USAGE_TEMPLATE.md` file or missing blank/filled pair
  - Action: Return `FAIL` and require both template variants

## Definition of Done
- Candidate agent satisfies all hard gates
- Candidate agent scores at least `14/16`
- Full rubric output is shown to the user
- Candidate agent includes concrete next-step improvements if score is below perfect

## Quality Rubric (0-2 per criterion, Total 16)
- Purpose clarity
- Scope control
- Input completeness
- Output specificity
- Workflow determinism
- Safety coverage
- Validation quality
- Failure recovery clarity

## Hard Gates (Mandatory)
An agent fails regardless of score if any item below is false:

- [ ] `README.md` and `USAGE_TEMPLATE.md` both exist
- [ ] `Last Updated` timestamp exists near the top of the README
- [ ] Rubric is scored
- [ ] Rubric output is explicitly shown to the user
- [ ] `USAGE_TEMPLATE.md` exists with blank and filled variants

## Required Rubric Output Format
Every agent review must show this information to users:

1. Criterion scores (`0-2` each)
2. Total score (`X/16`)
3. Pass/fail result
4. Top 3 improvements to raise score

## Example Scoring Output
```md
Agent Review Result: FAIL
Total Score: 11/16

Criterion Scores
- Purpose clarity: 2/2
- Scope control: 1/2
- Input completeness: 1/2
- Output specificity: 2/2
- Workflow determinism: 1/2
- Safety coverage: 1/2
- Validation quality: 2/2
- Failure recovery clarity: 1/2

Top Improvements
1. Add explicit out-of-scope exclusions.
2. Add concrete validation commands.
3. Add failure signals and recovery actions.
```

## Agent Acceptance Checklist
- [ ] Agent folder contains `README.md` and `USAGE_TEMPLATE.md`
- [ ] Purpose is clear and narrow
- [ ] Inputs and outputs are documented
- [ ] Safety boundaries are explicit
- [ ] Workflow is deterministic enough to follow
- [ ] Verification steps are defined
- [ ] Failure handling is documented
- [ ] New contributor can use it without tribal knowledge
- [ ] Timestamp is present near top of README
- [ ] Rubric score and output are shown to user
- [ ] `USAGE_TEMPLATE.md` has blank and filled versions

## Minimal Template for Future Agents
Copy this into `agents/<new-agent>/README.md`:

```md
# <Agent Name>
Last Updated: YYYY-MM-DD HH:MM TZ

## Mission
<One sentence about what this agent does.>

## In Scope
- ...

## Out of Scope
- ...

## Inputs
- Required:
- Optional:

## Outputs
- Format:
- Location:

## Workflow
1. ...
2. ...
3. ...

## Constraints
- ...

## Validation
- Command/check:
- Expected result:

## Failure Handling
- If X happens, do Y.

## Definition of Done
- ...
```

Also create `agents/<new-agent>/USAGE_TEMPLATE.md` with:
- `Blank Template` section
- `Filled Example` section

## Self-Evaluation Rubric
- Purpose clarity: <0-2>
- Scope control: <0-2>
- Input completeness: <0-2>
- Output specificity: <0-2>
- Workflow determinism: <0-2>
- Safety coverage: <0-2>
- Validation quality: <0-2>
- Failure recovery clarity: <0-2>
- Total: <X/16>
- Result: <PASS/FAIL>
- Top improvements:
  1. ...
  2. ...
  3. ...
```
