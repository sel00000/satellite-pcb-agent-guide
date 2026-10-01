# Satellite Circuit Board Design Agent Guidelines

## Purpose and Scope

Manage requirements, the BOM, schematics, PCB design, and verification evidence together for a circuit board intended for satellite use. The board function is not yet defined. Do not invent the function, orbit, lifetime, power conditions, thermal boundary conditions, radiation environment, or applicable standards. Write explanations and reports in English unless the user explicitly requests another language. Preserve original component names, MPNs, symbols, units, and document identifiers.

## Core Rules

1. **When evaluating BOM candidates and when reviewing their application in the selected circuit and PCB, directly inspect the manufacturer's datasheet for the exact orderable part number (MPN) of every chip.** Match the component name, manufacturer, suffix, package, pinout, and temperature, quality, and radiation grades. Do not select a part using only a distributor description or the model's memory.
2. **For each component, record the evidence, operating conditions, worst-case conditions, margins, and verdicts for DS-01 through DS-06.** Instances of the same MPN may share source documents, but evaluate placements separately when supply voltage, load, timing, or cooling conditions differ. Apply relevant checks to power semiconductors, passive components, connectors, and other parts as well.
3. **Read the test conditions, footnotes, graphs, pin descriptions, errata, and package-specific restrictions as well as the datasheet tables.** Record the source URL, document number, revision, date, access date, and page, table, and figure references. Do not invent unread source content or missing specifications.
4. **Cover both steady-state and transient worst cases.** Include power-up, shutdown, brownout, reset, backfeeding, inrush, load changes, and required fault scenarios. Account for supply error and ripple, component tolerances, temperature, aging, and applicable radiation effects, and explain which conditions can occur together.
5. **Do not use Absolute Maximum Ratings as the normal operating range or as design targets.** Normal operation must satisfy both the manufacturer's operating and characteristic conditions and the project's derating criteria. Check applicable limits and duration conditions for transient stress as well.
6. **Missing evidence means `UNVERIFIED`.** Do not treat `Typ` as a guaranteed value, substitute zero for an unknown value, or relabel an unverified item as `NOT_APPLICABLE`. Use non-applicability only with a valid reason and supporting evidence.
7. **Do not finalize a component or a dependent design when a required review item is `FAIL` or `UNVERIFIED`.** Continue independent alternative research, calculations, and drafting, and record the blocking conditions. A preliminary candidate BOM is allowed, but must not be labeled as a reviewed and finalized BOM.
8. **Verify suitability for the space environment separately.** Review vacuum thermal management, radiation, mission lifetime, launch conditions, materials, assembly, and traceability. COTS status, automotive qualification, a wide temperature range, or a “space” label alone does not establish suitability for flight.
9. **Distinguish requirements, assumptions, manufacturer facts, calculations, simulations, measurements, and approvals.** Passing ERC/DRC or operating at room temperature does not demonstrate electrical margin, radiation tolerance, thermal performance in vacuum, or flight suitability.
10. **Reassess affected verdicts after changes.** Trace the effects of changes to the MPN, alternate part, package, document revision, circuit, PCB, load, supply, clock, firmware settings, thermal path, or applicable lot. Reuse evidence that remains valid and return invalidated items to `UNVERIFIED`.

## Design Decisions and Improvement

For significant component, circuit, thermal, and protection decisions, use `define the problem and limitations → establish a baseline → develop alternatives and testable hypotheses → screen quickly → verify the full requirements scope → analyze causes and contributions → review critically and resolve findings → adopt and record`. At each stage, use evidence to decide whether to proceed, refine, reject, or defer.

- Define mandatory requirements, evaluation metrics, conditions, and acceptance criteria before comparison. Other performance gains or scores cannot compensate for DS/SAT violations. Novelty alone is not a selection criterion.
- Use both favorable results and failure records. Check consistency among the proposed explanation, actual BOM, circuit, PCB, firmware, verification configuration, and results.
- Address objections with the necessary source documents, calculations, or tests. Reevaluate the revision under the same conditions before updating the baseline. Keep changes with unconfirmed benefits separate from the established baseline.
- Record hypotheses, alternatives, evidence, falsification conditions, and decision summaries using the [design decision process](docs/design-reasoning.md) and [decision record template](templates/design-decision.md). For minor changes, update only the affected items in the existing record.
- Define the iteration scope and stopping conditions. If the budget is exhausted or external evidence is pending, defer the decision, retain `UNVERIFIED`, and continue independent work. Separating review roles does not authorize multi-agent execution or flight approval.

## Mandatory Datasheet Checks

| ID | Topic | Required Assessment |
|---|---|---|
| DS-01 | Absolute Maximum Ratings | Do voltages, currents, junction temperature, pin stresses, and transients remain within the applicable limits? |
| DS-02 | Recommended Operating Conditions | Are the actual supply, inputs, temperature, frequency, and sequencing within the specified operating range? |
| DS-03 | Electrical Characteristics | Do Min/Typ/Max values and test conditions apply to the actual circuit, and is the required performance guaranteed? |
| DS-04 | Thermal Characteristics | Are losses, thermal paths, boundary temperatures, steady-state and transient junction temperatures, and margins supported by calculations and evidence? |
| DS-05 | Timing Characteristics | Are the required minimum and maximum setup/hold, delay, rise/fall, startup, shutdown, and protection response conditions satisfied? |
| DS-06 | Peak/Continuous Current & SOA | Are continuous, RMS, peak, pulse, repetition, and simultaneous voltage/current stresses acceptable? |

## Read References According to the Task

| Current Task | Required References |
|---|---|
| Start a project or change mission, power, or environmental conditions | [Requirements template](templates/project-requirements.md), [satellite board criteria](docs/space-board.md) |
| Make a significant design choice, improve performance, investigate repeated failures, or address review findings | [Design decision process](docs/design-reasoning.md), [decision record template](templates/design-decision.md) |
| Compare components, select or substitute BOM parts, or finalize the BOM | [Datasheet review criteria](docs/datasheet-review.md), [component review template](templates/component-review.md), [BOM review register](templates/bom-review.csv) |
| Change circuits, PCB layout, clocks, firmware, or thermal paths | Existing records for the changed components and the affected sections of the datasheet and satellite criteria |
| Prepare for fabrication or assess flight use | [Stage completion criteria](docs/space-board.md) and the applicable BOM, review, and test records |
| Check sources or the applicability of standards | [Sources and interpretation scope](docs/sources.md) |

Do not repeat the entire design review for wording or formatting changes. Do not skip the applicable checks when a change affects an engineering decision.

## Records and Completion Criteria

- Copy the [component review template](templates/component-review.md) into `reviews/components/` and link it to each BOM MPN, operating context, and placement. Record the rationale when grouping equivalent conditions.
- Use `PASS`, `FAIL`, `UNVERIFIED`, and `NOT_APPLICABLE`. A `PASS` applies only to the recorded scope and evidence; it is not flight approval.
- Every applicable check must have supporting evidence before a component is finalized. Fabrication and flight stages must additionally satisfy the [stage-specific criteria](docs/space-board.md).
- Link significant design decisions to requirement IDs, component review IDs, candidate and baseline revisions, and calculation or test results. Complete the decision record only when its summary matches the current implementation and evidence.
- If mission conditions are missing, proceed with common criteria and candidate evaluation while leaving mission-specific radiation, thermal, and derating suitability unverified. Do not fill gaps with invented voltages, doses, safety factors, or test counts.
- Complete the assigned documentation, calculations, changes, and verification. Report what changed, the supporting evidence, the verified scope, open items, and the actions needed to resolve them. Do not request repeated confirmation for already authorized research and local edits.
- Perform purchasing, fabrication orders, external submissions, and hardware tests only within the authority and procedures provided for that work. Record flight approval only from the project's designated responsible authority.

This file defines continuing project rules. Numerical examples and illustrative plots in the supplied images are not actual component ratings or project requirements.
