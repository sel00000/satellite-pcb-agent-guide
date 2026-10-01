**English** | [한국어](README.ko.md)

# Satellite PCB Agent Guide

Bring datasheet evidence into every component decision when designing a satellite circuit board with an AI agent.

This repository provides an `AGENTS.md` entry point, detailed review criteria, and reusable record templates. It helps engineers and agents connect requirements, component specifications, circuit conditions, and verification results throughout the design process.

**Review the manufacturer's datasheet for every chip, both when evaluating BOM candidates and when checking how selected parts are used in the circuit and PCB.** Record the exact part, conditions, evidence, margins, and verdict before finalizing the selection.

## Start with your project

Clone the repository:

```bash
git clone https://github.com/sel00000/satellite-pcb-agent-guide.git
```

1. Copy [AGENTS.md](AGENTS.md), `docs/`, and `templates/` together into your PCB project's root directory. Merge existing instructions and folders carefully. Use an agent that reads `AGENTS.md`, or explicitly provide it as project guidance.
2. Complete the [project requirements template](templates/project-requirements.md). Leave unknown inputs as `TBD`; keep decisions that depend on them `UNVERIFIED`.
3. Copy the [component review template](templates/component-review.md) into `reviews/components/` for each candidate and operating context. Keep versioned manufacturer documents in a project location such as `evidence/datasheets/`.
4. Add candidate parts to the [BOM review register](templates/bom-review.csv) and link their review records. The supplied CSV contains headers only. A candidate list can grow while reviews are pending; a finalized BOM requires completed applicable checks.
5. For significant choices, copy the [design decision template](templates/design-decision.md) into `reviews/decisions/`. Use the [stage completion criteria](docs/space-board.md) to distinguish component review, design review, fabrication release, and flight approval.

For example, ask your agent:

```text
Review this candidate BOM using AGENTS.md. Read the manufacturer's datasheet
for each exact MPN, evaluate DS-00 through DS-06 under the actual circuit
conditions, and create linked component review records. Mark missing evidence
UNVERIFIED and list what is needed to resolve it. Apply the relevant satellite
criteria and decision process to significant choices.
```

These are instructions and templates. The project agent must follow them and have access to the necessary documents and tools; this repository does not automatically retrieve datasheets or enforce review results.

## Six checks for every component review

Start with **DS-00: identity and traceability**. Match the manufacturer, exact orderable part number (MPN), suffix, package, pinout, and applicable grades. Record the document revision and relevant pages, tables, figures, and footnotes.

| ID | Check | What the review must establish |
|---|---|---|
| DS-01 | Absolute Maximum Ratings | Steady-state and transient stresses stay within applicable limits. Absolute maximum ratings are not normal operating targets. |
| DS-02 | Recommended Operating Conditions | Supply, inputs, temperature, frequency, and sequencing satisfy the specified operating conditions and project restrictions. |
| DS-03 | Electrical Characteristics | Min/Typ/Max values and their test conditions support the required performance in the actual circuit. Typical values are not guarantees. |
| DS-04 | Thermal Characteristics | Device losses, thermal paths, boundary conditions, and junction temperatures support the required thermal margin. |
| DS-05 | Timing Characteristics | Setup/hold, propagation delay, rise/fall, startup, shutdown, and protection response meet applicable minimum and maximum requirements. |
| DS-06 | Peak / Continuous Current and SOA | Continuous, RMS, peak, and pulse stresses are acceptable for their duration, repetition, temperature, and simultaneous voltage conditions. |

Apply relevant checks to power semiconductors, passives, connectors, and interconnections too. The same MPN can share source documents, but different supply, load, timing, or cooling conditions require their own assessment. See the [detailed datasheet criteria](docs/datasheet-review.md).

## Account for the satellite environment

The [satellite board criteria](docs/space-board.md) cover mission requirements and standards, derating and end-of-life conditions, heat transfer in vacuum, radiation and recovery, power and fault effects, materials and traceability, and verification plans.

Select limits and acceptance criteria for the actual mission. Board function, orbit, lifetime, supply, loads, thermal interfaces, radiation environment, component grades, and applicable standards remain project inputs. The guide supplies no universal dose, derating factor, or test count. Mission-specific suitability stays `UNVERIFIED` until supported by evidence.

## Improve decisions through evidence

The [design decision process](docs/design-reasoning.md) adapts the hypothesis, experiment, critique, and refinement structure described in *ScientistTwo* into eight stages:

1. Define the problem, limitations, and acceptance criteria.
2. Establish a reproducible baseline.
3. Develop alternatives and testable hypotheses.
4. Screen candidates within a stated scope.
5. Verify the full requirements scope and implementation consistency.
6. Analyze causes and the contribution of each change.
7. Resolve review findings with additional evidence.
8. Reevaluate, adopt, and record the decision.

Requirements and reliability take priority over novelty. Preserve failure records, compare revisions under consistent conditions, and keep unresolved items `UNVERIFIED` when the review budget expires. The [source record](docs/sources.md#s9) identifies which ideas were adapted. This is a hardware review workflow; it does not install ScientistTwo, reproduce the paper's results, or automatically run multiple agents.

## Make the verdict traceable

| Status | Meaning |
|---|---|
| `PASS` | Evidence supports the check within its recorded scope and conditions. |
| `FAIL` | Evidence shows that an applicable requirement is not met. |
| `UNVERIFIED` | Necessary requirements, source data, analysis, or verification are missing, or a change has invalidated the evidence. |
| `NOT_APPLICABLE` | The check does not apply; a rationale and supporting evidence are recorded. |

**A required `FAIL` or `UNVERIFIED` prevents finalizing the component or dependent design.** Independent research, calculations, and drafts can continue. Reassess affected verdicts after changes to a part, document, circuit, PCB, firmware, load, clock, or thermal path.

Keep manufacturer facts, assumptions, calculations, simulations, measurements, and approvals distinct. A review `PASS`, ERC/DRC result, or room-temperature bench result does not establish flight approval. The project's designated authority and required qualification evidence determine release for flight.

## Repository map

The core instructions stay short; detailed criteria are opened when a task needs them. The guides and templates are in English. This README is also available in [Korean](README.ko.md).

| File | Purpose |
|---|---|
| [AGENTS.md](AGENTS.md) | Core rules and routing to the relevant references |
| [docs/datasheet-review.md](docs/datasheet-review.md) | Component identity, six mandatory checks, evidence, and margins |
| [docs/space-board.md](docs/space-board.md) | Satellite environment criteria and stage completion requirements |
| [docs/design-reasoning.md](docs/design-reasoning.md) | Baselines, hypotheses, comparisons, critique, and adoption |
| [docs/sources.md](docs/sources.md) | Source references, reviewed scope, and adaptation decisions |
| [templates/project-requirements.md](templates/project-requirements.md) | Mission and board requirements to establish before design decisions |
| [templates/component-review.md](templates/component-review.md) | Component and operating-context review record |
| [templates/design-decision.md](templates/design-decision.md) | Alternatives, verification, review findings, and decisions |
| [templates/bom-review.csv](templates/bom-review.csv) | Empty register linking BOM entries to review evidence |

## Scope and sources

This is a reusable documentation package for satellite PCB projects. No board function, actual BOM, circuit, or completed hardware qualification is supplied.

The [source notes](docs/sources.md) link manufacturer, NASA, ECSS, and research references and state what was reviewed. They also record the user-provided materials that informed the package. Those original attachments are not distributed here. Numerical examples in the supplied screenshots were treated as illustrations, not component ratings or mission requirements.

To suggest an improvement, describe the affected rule and use case, cite the supporting source, and explain any effect on review criteria. Keep the English and Korean README files aligned when changing their shared explanation.
