# Refinement Implementer Prompt Template

Use this template when dispatching a refinement implementer subagent after an evaluator has identified issues.

**Purpose:** Act on the evaluator's critique to improve the implementation. Make a strategic decision: refine or pivot.

```
Task tool (general-purpose):
  description: "Refine implementation based on evaluator feedback — Iteration N"
  prompt: |
    You are improving an existing implementation based on detailed evaluator
    feedback. This is iteration N of a refinement loop.

    ## The Evaluator's Full Critique

    [PASTE: the evaluator's complete output from the previous round]

    ## Original Spec

    [PASTE: spec/plan or reference to spec file path]

    ## Evaluation Criteria

    [PASTE: the criteria the evaluator graded against]

    ## What Has Been Tried

    [PASTE: brief summary of previous iterations and what was changed — omit on
    first iteration]

    ## Your First Decision: Refine or Pivot

    Before writing any code, make a strategic decision:

    **REFINE** — if the evaluator's feedback is about specific issues within an
    approach that's fundamentally sound. Most iterations will be refinements.
    Examples: missing edge cases, incomplete features, style inconsistencies.

    **PIVOT** — if the evaluator's feedback suggests the current approach has a
    structural problem that targeted fixes won't solve. This is rare but important.
    Examples: architecture doesn't support a required feature, design approach is
    fundamentally flawed, too many interrelated issues to fix individually.

    State your decision and reasoning BEFORE starting work.

    ## Your Job

    Based on your strategic decision:

    1. Address every CRITICAL issue from the evaluator's critique — none may be skipped
    2. Address IMPORTANT issues — skip only with explicit justification
    3. Address MINOR issues if they're easy wins
    4. Run existing tests to verify nothing is broken
    5. Commit your changes with a descriptive message

    ## While You Work

    - Focus on the evaluator's feedback, not on adding new features
    - Don't over-engineer fixes — targeted changes are better than rewrites
    - If a PIVOT: you may restructure more broadly, but stay focused on what the
      evaluator flagged. Don't use "pivot" as an excuse for unrelated changes.
    - If you discover that an evaluator issue is actually not a real problem,
      explain why in your report — but you need strong evidence, not just
      disagreement

    ## Report Format

    Report back with:

    ```
    ## Strategic Decision: [REFINE / PIVOT]
    Reasoning: [why]

    ## Issues Addressed
    - [CRITICAL] [issue description]: [what you did] — [file:line]
    - [IMPORTANT] [issue description]: [what you did] — [file:line]
    - [MINOR] [issue description]: [what you did] — [file:line]

    ## Issues NOT Addressed
    - [issue]: [why not]

    ## What Changed
    [Summary of changes for the next evaluator to review]

    ## Concerns
    [Anything the coordinator should know — areas of uncertainty,
    potential regressions, issues that may need user input]
    ```
```
