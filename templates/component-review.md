# Component Datasheet Review Record — Blank Template

How to use: copy this file into `reviews/components/`. The default status is `UNVERIFIED` until actual review results are entered. Use separate records or scenarios for different operating conditions, even when the MPN is the same.

Review criteria: [Datasheet review](../docs/datasheet-review.md), [satellite board criteria](../docs/space-board.md). Adjust links to the new location after copying.

## 1. Component and Applicable Design — DS-00

| Field | Entry |
|---|---|
| Review ID / date / reviewer | TBD |
| Linked Design Decision ID / decision record path | TBD; link significant design choices using the [decision record template](design-decision.md) |
| Board ID / schematic and PCB revision / firmware settings baseline | TBD |
| Manufacturer / full MPN / suffix | TBD |
| Function / RefDes / quantity | TBD |
| Package / pin count / pinout / exposed pad / footprint | TBD |
| Temperature grade / quality grade / radiation grade and evidence | TBD |
| Operating-context group / rationale for grouping equivalent conditions | TBD |
| Procurement status / supply channel / date, lot, and die traceability and applicability | TBD |
| Stage and review scope | Specify candidate / design / ground prototype / flight |
| Overall verdict | UNVERIFIED |

## 2. Source Traceability

| Source Type | Manufacturer URL and Document Number | Revision and Document Date | Access Date | Local Path and SHA-256 | Applicable MPN and Scope |
|---|---|---|---|---|---|
| Datasheet | TBD | TBD | TBD | TBD | TBD |
| Errata / applicable notices | TBD | TBD | TBD | TBD | TBD |
| Required application notes, quality documents, and radiation reports | TBD | TBD | TBD | TBD | TBD |

If a source is missing or inaccessible, record the reason and the action to obtain it. Distinguish a document that has not been found from one that is not required.

## 3. Operating Scenarios and Boundary Conditions

| Scenario | Supply and I/O Minimum–Maximum | Current, Load, Frequency, and Duty Cycle | Temperature and Thermal Boundaries | Duration and Repetition Rate | Requirement and Calculation Evidence |
|---|---|---|---|---|---|
| Normal operation / maximum load | TBD | TBD | TBD | TBD | TBD |
| Startup / shutdown / reset / brownout | TBD | TBD | TBD | TBD | TBD |
| Standby / partial power / backfeeding | TBD | TBD | TBD | TBD | TBD |
| Applicable transients and faults | TBD | TBD | TBD | TBD | TBD |
| End of life / applicable radiation effects | TBD | TBD | TBD | TBD | TBD |

State whether each scenario requires normal functionality, freedom from damage, or transition to a safe state. Mark irrelevant scenarios as not applicable with supporting evidence.

## 4. Parameter Evidence and Margins

Duplicate the row below for each parameter and scenario. Link detailed calculations, waveforms, and test files in the results column.

| Check ID / Symbol | Unit / Min, Typ, Max, and Guarantee Type | Manufacturer Test Conditions | Source Page, Table, Figure, and Footnote | Requirement / Project Restriction | Actual Conditions and Worst-Case Value | Calculation, Margin, and Result Link | Status |
|---|---|---|---|---|---|---|---|
| TBD | TBD | TBD | TBD | TBD | TBD | TBD | UNVERIFIED |

## 5. Mandatory Check Summary

| ID | Required Summary | Verdict | Evidence Location / Action to Resolve Unknowns |
|---|---|---|---|
| DS-00 | Exact MPN, package, pins, source revision, and mapping to placements | UNVERIFIED | TBD |
| DS-01 | Absolute maximum ratings and steady-state/transient stresses | UNVERIFIED | TBD |
| DS-02 | Normal operating range, supply, temperature, and sequencing | UNVERIFIED | TBD |
| DS-03 | Min/Typ/Max characteristics, test conditions, and performance margins | UNVERIFIED | TBD |
| DS-04 | Losses, thermal paths, junction temperature, and thermal margin | UNVERIFIED | TBD |
| DS-05 | Minimum/maximum timing and complete path margins | UNVERIFIED | TBD |
| DS-06 | Continuous, RMS, peak, pulse, repetition conditions, and SOA | UNVERIFIED | TBD |

`NOT_APPLICABLE` requires a non-applicability rationale. Use `UNVERIFIED` for missing data.

## 6. Space Environment Links

| ID | Item to Link to the Component Review | Verdict | Board-Level Record or Component Evidence |
|---|---|---|---|
| SAT-01 | Applicable mission conditions, standards, and grades | UNVERIFIED | TBD |
| SAT-02 | Derating and BOL/EOL | UNVERIFIED | TBD |
| SAT-03 | Vacuum thermal paths and boundary conditions | UNVERIFIED | TBD |
| SAT-04 | TID, TNID/DDD, SEE, and required recovery | UNVERIFIED | TBD |
| SAT-05 | Power, interfaces, and fault effects | UNVERIFIED | TBD |
| SAT-06 | Materials, assembly, procurement, lot traceability, and mechanical conditions | UNVERIFIED | TBD |
| SAT-07 | Required verification plans, execution, and results | UNVERIFIED | TBD |

Link the location and revision of evidence common to the board instead of copying it. Distinguish a completed plan from completed physical testing.

## 7. Evidence and Open Items

| Type | Evidence or Result | Verified Scope | Limitations and Incomplete Work |
|---|---|---|---|
| Requirements and assumptions | TBD | TBD | TBD |
| Manufacturer source documents | TBD | TBD | TBD |
| Calculations and simulations | TBD | TBD | TBD |
| Circuit and PCB checks | TBD | TBD | TBD |
| Physical measurements and environmental tests | TBD | TBD | TBD |
| Stage approval records | TBD | TBD | TBD |

| Open Item ID | Missing Information / Violation | Affected Components, Verdicts, and Stages | Resolution Action, Owner, and Target Date |
|---|---|---|---|
| TBD | TBD | TBD | TBD |

## 8. Decision and Change Impact

- Decision: `Undecided`. Record selected, deferred, or rejected, together with the rationale.
- Permitted use scope: TBD. Do not extend a ground prototype decision into a flight-use decision.
- Design inputs that trigger reassessment and linked calculations/tests: TBD.
- Change history: date / previous and new MPN or design revision / affected check IDs / reassessment results.
- For a formally authorized exception, retain the applicable requirement, scope, rationale, approving authority, and approval record while preserving the original technical verdict.
