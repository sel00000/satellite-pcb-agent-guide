# A Process for Improving Design Decisions Through Evidence

Governing rules: [AGENTS.md](../AGENTS.md) · Record: [Design decision template](../templates/design-decision.md)

This process adapts the hypothesis, experiment, critique, and refinement structure described in §3.1–3.6, Table 1, and Figures 3–7 of the user-provided `ScientistTwo.pdf` to satellite board design. The paper addresses AI/ML research. The process below is a project-specific adaptation, not a satellite-hardware validation result reported by the authors. [Source and applicability](sources.md#s9)

## When to Apply This Process

Use it for decisions that change performance, reliability, or verification scope, such as component substitutions, power architecture, thermal paths, interfaces, and protection methods. Do not restart the full research process for every wording, formatting, or demonstrably equivalent change. Reuse existing decisions and evidence, updating the affected scope.

A reviewable record contains the problem, hypothesis, alternatives, source documents, calculation and test evidence, falsification conditions, results, and a decision summary. Prefer concise, traceable records over lengthy explanations without identifiable evidence.

## 1. Establish the Decision Basis

1. **Fix mandatory conditions first.** Manufacturer limits and normal operating conditions, mission requirements, DS/SAT criteria, and test scope are optimization constraints. Performance, price, or size scores cannot compensate for a constraint violation.
2. **Establish that the problem exists.** Distinguish an impression that something is undesirable from a limitation supported by data. Identify the conditions producing the symptom, the insufficient margin, and the affected requirements.
3. **State the improvement objective.** Define the actual objectives and priorities among reliability, margin, performance, mass, power, complexity, and procurement feasibility. Do not adopt a design based on novelty alone.
4. **Keep comparisons consistent.** Compare the baseline and candidates under the same load, temperature, voltage, waveform, and measurement conditions. If evaluation conditions change, record why and reevaluate both sides.

## 2. Decision Stages — DR-01 through DR-08

### DR-01 — Problem, Limitations, and Success Criteria

Link the problem to requirement IDs. Separate observed failure or degradation conditions, verified facts, provisional assumptions, and missing information. Give assumptions a verification plan; do not promote them into evidence for final acceptance.

Before comparing options, define mandatory acceptance conditions, improvement metrics, permitted trade-offs, error and uncertainty criteria for distinguishing meaningful improvement, and stopping conditions. Although the research paper explores without predefined numerical targets, retain explicit requirements for this board.

### DR-02 — Reproducible Baseline

Use the current design or an evidence-supported reference design as the baseline. Identify the MPNs, circuit, PCB, firmware, thermal paths, inputs, models, and test configuration, and recheck the relevant results. Distinguish a reference design from a baseline validated on the actual board.

If the baseline cannot be reproduced, first inspect the model, circuit connections, and test conditions. Do not directly compare unrelated reported numbers and claim a percentage improvement. For a new design without an existing board, explicitly identify a calculation- or model-level baseline and limit the verification claim accordingly.

### DR-03 — Alternatives and Testable Hypotheses

When meaningful alternatives exist, include retaining the current design and approaches based on different solution principles. Do not create artificial candidates merely to fill a comparison table. For each candidate, record:

- The changed elements and affected DS/SAT checks.
- The physical mechanism expected to improve a particular metric.
- Conditions that could produce a different outcome, results that would not support the hypothesis, or observations that would reject it.
- Required datasheets, calculations, models, tests, cost, time, and newly introduced risks or complexity.

Example: selecting a lower-RDS(on) MOSFET may reduce conduction loss while increasing gate charge and switching loss. Compare worst-case total losses, temperature, SOA, and drive margins, rather than RDS(on) alone. This example is not a component selection result.

### DR-04 — Rapid Screening

Start with source ratings, simple worst-case calculations, local models, and high-impact operating modes to identify clear incompatibilities or missing data early. Reduce major failure risks before expensive full analyses or fabrication.

State what screening has and has not verified. Do not promote a pass at representative conditions into a full-scope verification claim. Record actual limit violations as `FAIL`, and missing information or unperformed verification as `UNVERIFIED`.

### DR-05 — Full Requirements Scope and Implementation Consistency

For a promising candidate, expand verification to the supplies, loads, temperatures, tolerances, operating modes, startup/shutdown, transients, faults, and lifetime conditions required by the decision. Screening does not replace tests in the project's verification plan.

Check that claimed functions match the actual MPNs, schematics, netlist, PCB, and firmware settings. Align configuration revisions used in calculations, simulations, and measurements. If structures or conditions differ, do not use them as evidence for the same design until the effect of those differences is assessed.

Compare margins, performance, reliability, complexity, and verification burden together, rather than relying on one efficiency or cost metric. Record full-range worst cases and vulnerable modes; do not hide violations in averages.

### DR-06 — Causal and Contribution Analysis, and Falsification

When benefits are unclear or several changes are combined, use controlled comparisons, sensitivity analysis, and suitable experimental designs. Here, the paper's ablation concept means isolating which elements produced the observed result.

Where practical, hold other conditions constant and compare one factor at a time. Strong interactions require combinations of factors to be assessed; one comparison alone does not establish causality. Retain unfavorable results and differences within the uncertainty range. If the effect remains unclear, revise the hypothesis or narrow the improvement claim.

Do not remove protection, insulation, required decoupling, or redundancy solely because its performance contribution appears small. Fault analyses requiring removal or disabling of a function must use an appropriate model or a test with established authority and procedures. Do not automatically transfer an analysis-only configuration into the product configuration.

### DR-07 — Critical Review and Supplementary Verification

Examine counterexamples that could invalidate the proposal as well as evidence supporting it. Use the following review perspectives.

| Review Perspective | Questions to Resolve |
|---|---|
| Requirements | Is the problem tied to an actual requirement? Has a favorable metric obscured a mandatory condition? |
| Datasheets | Were the exact MPN, revision, footnotes, and test conditions used? Was Typ treated as guaranteed? |
| Worst cases | Are cold/hot, startup, transient, or fault conditions hidden by averages or steady-state results? |
| Comparison validity | Do baseline and candidate conditions, measurements, and models match? Is the improvement larger than the uncertainty? |
| Implementation consistency | Are the reported circuit, protection, and timing actually implemented in the files and settings? |
| Satellite applicability | Have terrestrial cooling, testing, or grades been overstated as evidence for vacuum, radiation, or mission lifetime? |

Check the evidence for each comment and perform the necessary additional calculations, measurements, or tests. Do not close an unresolved technical issue by editing the narrative alone. Answer unsupported objections with verifiable evidence.

One agent may sequentially adopt designer, critical reviewer, and final-check perspectives. Do not describe self-review by the same actor as independent review. If actual independent review is required, identify the reviewer and retain the review record. This document does not instruct the creation of sub-agents or external transmission.

### DR-08 — Reevaluate, Adopt, and Record

After refinement, repeat affected comparisons and DS/SAT checks. Among candidates satisfying mandatory conditions, decide according to the predefined objectives and trade-offs. Every metric need not improve simultaneously, but record any regression and the basis for accepting it.

Update the baseline only after evidence supports the new design. If the revision fails the criteria or its benefit is unconfirmed, retain the existing valid baseline. If that baseline itself violates a requirement, retaining it does not justify passing the final design.

Keep hypotheses, input and configuration revisions, executed calculations and verification, results, objections, and decision rationale for successful, failed, and deferred candidates in `reviews/decisions/`. Consider previous failures and different solution principles to avoid repeating the same change. Do not declare an unverified candidate to be the best solution.

## 3. Distinguish Stage Decisions from Technical Verdicts

| Stage Decision | Meaning | Relationship to Technical Verdicts |
|---|---|---|
| Proceed | Evidence required at the current stage is sufficient to perform the next verification step | A pass for the current scope, not final design acceptance or flight approval |
| Refine | Resolvable findings or incomplete verification require changes or additional evidence | Retain the original FAIL/UNVERIFIED verdict until the issue is resolved |
| Reject | End evaluation because of an actual requirement violation or insufficient adoption justification in a valid comparison | A requirement violation is FAIL; a technically passing candidate losing a comparison retains its PASS verdict |
| Defer | Requirements, evidence, test authority, or resources are missing, or the review budget has ended | Unverified items remain UNVERIFIED; budget exhaustion alone does not establish FAIL or PASS |

Review scores and confidence in a hypothesis do not replace [datasheet verdicts](datasheet-review.md) or [stage completion criteria](space-board.md).

## 4. Iteration Scope and Completion

Before starting another design iteration, briefly define the uncertainty to resolve, required evidence, permitted time and resources, and stopping conditions. Do not repeat the same attempt without new evidence, a justified change, or a different hypothesis. Diagnose tool execution failures and model errors separately from physical failures of the candidate.

A decision is complete only when the mandatory reviews, comparisons, major objections, implementation/evidence consistency checks, and decision record are complete for its scope. If external information or physical testing prevents completion, record the reason for deferral, remaining evidence, and conditions for resuming, and continue independent work. Completing a preset number of iterations is not evidence of completion.

## 5. Source Concepts and Adapted Criteria

| ScientistTwo Location | Referenced Structure | Satellite Board Adaptation |
|---|---|---|
| p.5, Listing 1 and Table 1 | Stage-specific critique, refinement, and acceptance | Distinguish evidence-supported DS/SAT stage decisions from deferral |
| p.6, §3.1 | Identify limitations and generate multiple hypotheses | Establish actual design limitations; prioritize requirements and reliability over novelty |
| pp.6–7, §3.2 | Reproduce a baseline and scale from subset to full-set | Screen quickly, then verify the full requirements scope of the decision |
| pp.7–8, §3.3 | Improve using success/failure history and explore other candidates | Preserve failures, retain the baseline, and compare alternatives |
| p.8, §3.4 | Ablation and verification of refinements | Safe contribution, sensitivity, causal, and falsification analyses |
| pp.8–9, §3.5–3.6 | Supplementary experiments in response to criticism and reevaluation after changes | Resolve technical comments with evidence and update implementation and verification records |
| p.30, Appendix A.2 and B | Bounded iterations and an explanation of research objectives | Do not import fixed models, iteration counts, or paper-review scores; define board requirements in advance |

Page numbers are one-based PDF pages in the attachment. Do not use the paper's reported AI research performance, automated review scores, or execution costs as this board's performance, safety criteria, or verification budget.
