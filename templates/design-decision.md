# Design Decision Record — Blank Template

How to use: copy this file into `reviews/decisions/` for each significant design decision. Record the hypotheses, evidence, comparisons, and verdict summaries defined in the [design decision process](../docs/design-reasoning.md). Adjust links to the new location after copying.

## Identity and Scope

| Field | Entry |
|---|---|
| Decision ID / date / author and reviewer | TBD |
| Problem to solve / scope of this decision | TBD |
| Requirement IDs / component Review IDs / affected DS and SAT IDs | TBD |
| Baseline and candidate BOM, circuit, PCB, firmware, and model revisions | TBD |
| Actual review method | Specify self-review or independent review, the reviewer, and the record |
| Review time and resource limits / stopping and resumption conditions | TBD |

## DR-01 — Problem and Comparison Criteria

- Observed facts, conditions producing the problem, and result files: TBD.
- Evidence-supported limitations, provisional assumptions, and unknown information: TBD.

| Category | Requirement or Metric | Criterion, Unit, and Source | Evaluation Conditions, Error, and Uncertainty | Verification Method |
|---|---|---|---|---|
| Mandatory conditions | TBD | TBD | TBD | TBD |
| Improvement objectives and priorities | TBD | TBD | TBD | TBD |
| Permitted trade-offs | TBD | TBD | TBD | TBD |

## DR-02–DR-03 — Baseline, Alternatives, and Hypotheses

| Candidate ID | Changed Element and Solution Principle | Expected Benefit | Falsification or Rejection Condition | New Risks and Verification Burden | Evidence Link |
|---|---|---|---|---|---|
| Baseline | TBD | TBD | TBD | TBD | TBD |
| Alternative A | TBD | TBD | TBD | TBD | TBD |

- Baseline reproduction status and actual verified scope: UNVERIFIED / TBD.
- If only one alternative exists, explain why other approaches are infeasible or unnecessary: TBD.

## DR-04–DR-05 — Screening and Full-Scope Verification

| Candidate and Verification ID | Screening / Full Requirements Scope | Actual Configuration, Inputs, and Conditions | Method and Execution Status | Results, Uncertainty, and Files | DS/SAT Verdict | Remaining Scope |
|---|---|---|---|---|---|---|
| TBD | TBD | TBD | TBD | TBD | UNVERIFIED | TBD |

| Consistency Check | Actual Configuration and Evidence Location | Differences and Impact | Verdict |
|---|---|---|---|
| Proposed explanation ↔ BOM, circuit, PCB, and firmware | TBD | TBD | UNVERIFIED |
| Implementation revision ↔ configuration used in calculations, simulations, and tests | TBD | TBD | UNVERIFIED |

## DR-06 — Causal and Contribution Analysis

- Factors to isolate and the reason for doing so: TBD.
- Conditions held constant / changed conditions / interactions and uncertainty: TBD.
- Comparison results and unsupported hypotheses: TBD.
- Rationale for omitting this analysis if unnecessary: TBD.
- If changing physical hardware, identify the test article, authority, procedure, and restoration scope: TBD.

## DR-07 — Critique and Refinement

| Finding or Counterexample ID | Review Comment and Evidence | Required Sources, Calculations, or Tests | Actions Performed and Result Links | Resolved / Unresolved and Reason |
|---|---|---|---|---|
| TBD | TBD | TBD | TBD | Unresolved |

## DR-08 — Comparison and Final Decision

| Candidate | Mandatory-Condition Verdict | Improvements, Regressions, and Uncertainty | Complexity and Verification Burden | Stage Decision and Rationale |
|---|---|---|---|---|
| Baseline | UNVERIFIED | TBD | TBD | Defer / TBD |
| Alternative A | UNVERIFIED | TBD | TBD | Defer / TBD |

- Current stage decision: specify Proceed / Refine / Reject / Defer.
- Adopted option and decision summary: TBD.
- Reasons for not selecting other options: TBD.
- Permitted use scope and remaining unverified scope: TBD.
- Evidence for updating the baseline or reasons for retaining it: TBD.
- Updated files and revisions, and affected component review records: TBD.
- Next actions, owners, and resumption conditions: TBD.

Record the stage decision separately from PASS/FAIL/UNVERIFIED/NOT_APPLICABLE. Budget exhaustion does not demonstrate technical failure. Do not change an established technical PASS to FAIL merely because a candidate was not selected in a comparison.

## History

| Date and Iteration | Hypothesis or Change | Execution, Results, and Objections | Lessons and Next Decision | Linked Evidence |
|---|---|---|---|---|
| TBD | TBD | TBD | TBD | TBD |

Preserve failed and deferred attempts as well. Completing this form alone does not complete datasheet checks or physical testing.
