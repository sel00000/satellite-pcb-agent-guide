# Common Satellite Board Design and Verification Criteria

Governing rules: [AGENTS.md](../AGENTS.md) · Starting point: [Requirements template](../templates/project-requirements.md)

The board function remains undefined. Add EPS, OBC, communication, sensor, or payload-specific reviews when the actual function is established. The following common criteria must be developed for the mission; they do not replace a complete standard or certification procedure.

## SAT-01 — Mission Conditions and Standards Baseline

Link orbit, inclination, mission lifetime, operating modes and duty cycles, power-bus range and transients, loads, communications, temperatures and thermal interfaces, radiation, and mechanical and material conditions to requirement IDs. Distinguish events requiring normal functionality from events requiring damage prevention or transition to a safe state.

For applicable standards, record the document title, edition, applicable clauses, tailoring, requirement owner, and approval record. Distinguish reference documents from contractual or mission requirements. Do not combine numerical limits from different standards merely for convenience. For undefined items, record `TBD`, the affected decisions, and the owner and target date for resolution.

## SAT-02 — Derating and End-of-Life Conditions

Record the derating source, edition, clause, and applicability for each component family and stress. Do not apply one ratio to every component or invent uniform voltage, current, or temperature margins without a source. The [ECSS derating document overview](sources.md#s6) is a starting point for identifying potentially applicable criteria.

Satisfy the manufacturer's normal operating conditions and the project's restrictions independently. Establish beginning-of-life (BOL) and end-of-life (EOL) criteria including tolerances, aging, mission degradation, and applicable radiation-induced changes. Do not create nonexistent post-radiation guarantees through interpolation. Without mission-specific evidence, the corresponding lifetime and derating suitability remains `UNVERIFIED`.

## SAT-03 — Thermal Design in Vacuum

Do not design a board exposed to vacuum to depend on air convection for cooling. Evaluate conduction through the PCB, mounting points, TIM, housing, and satellite structure, and radiation between surrounding surfaces. Model the actual pressure and fluid conditions separately for a sealed, pressurized compartment. [NASA thermal control reference](sources.md#s5)

Connect board hot/cold boundary temperatures, thermal contact resistance, neighboring heat sources, operating modes, and sunlit/eclipse intervals to the system thermal conditions. Distinguish cold start, hot operation, and non-operating survival. Specify radiation-model inputs such as emissivity, area, view factors, and opposing-surface temperatures. Do not substitute the external environmental temperature directly for PCB TA.

Datasheet thermal metrics depend on the package, board, and test conditions. Distinguish calculated or modeled results from thermal-vacuum and thermal-balance test evidence. Record how the model's actual thermal paths correspond to the test boundary conditions.

## SAT-04 — Radiation Suitability and Recovery

Define the required assessment scope for TID, displacement damage/TNID, and SEE under the mission and shielding conditions. RHA is mission-specific, and these three effect categories must be addressed separately. [ECSS radiation assurance document overview](sources.md#s7)

Record the following in the component review where required:

- Evidence connecting the tested manufacturer, MPN, die/process, package, and lot to the procured hardware.
- Test particles, energy, LET and penetration depth, fluence, dose and dose rate, bias, voltage, temperature, operating mode, sample size, acceptance conditions, and measured changes.
- Information actually present in the report, including TID units and material reference, SEE cross-sections, thresholds, and observation limits. Do not claim guaranteed tolerance beyond the tested range through unsupported extrapolation.
- Project radiation margins and a comparison of expected mission error rates or failure risks against requirements. Leave effects with missing data unverified.

Distinguish functional errors such as SEU/SET from potentially destructive effects such as SEL/SEB/SEGR. Where applicable, assess ECC, scrubbing, watchdogs, reset, current interruption and restart, redundancy, and safe mode. The existence of these measures alone does not establish radiation suitability. Check actual detection and isolation delays, energy, and retry conditions.

Do not substitute terrestrial component ESD or latch-up test results for space-radiation SEE evidence. Labels such as “rad-hard,” “rad-tolerant,” COTS, or automotive grade alone do not establish suitability for a particular mission. Using results from another die or lot in the same product family requires an applicability rationale.

## SAT-05 — Power, Interfaces, and Fault Isolation

Align bus variations, inrush, backfeeding, unpowered I/O, multiple-rail sequencing, grounding, return paths, chassis connections, protection, insulation, and EMI/EMC requirements with system interfaces. Review ground test equipment connections separately.

Record fault analysis as `event → detection condition → worst-case detection delay → isolation/recovery action → remaining current and energy → system effect → retry condition`. Include required scenarios such as shorts, opens, brownout, communication loss, and reset loops. The project defines acceptable single-fault behavior and fault-propagation criteria.

Software-configured clocks, current limits, switching frequency, and sensor duty cycles are part of the hardware operating conditions. Link setting changes to reassessment of the applicable DS-01 through DS-06 checks.

## SAT-06 — Materials, Assembly, Procurement, and Mechanical Environment

Review PCB stackup, materials and surface finish; solder, finish, and process compatibility; coating, adhesive, and TIM outgassing and contamination; cleaning and moisture control; thermal-cycle fatigue; launch vibration and shock; and retention of connectors and heavy components. Obtain applicable test levels from project requirements.

Assess pure tin, tin whiskers, component finish, reflow, and storage conditions using the relevant materials, processes, and standards. Avoid unsupported blanket statements that a material is always allowed or prohibited simply because the application is in space.

Manage exact orderable parts, approved supply channels, manufacturing and date/lot traceability, certificates, screening and inspection records, counterfeit prevention, and change notifications. Define additional COTS evaluation, screening, and procurement plans under the project's applicable criteria. [ECSS commercial component document overview](sources.md#s8)

## SAT-07 — Linking Verification Plans and Results

For each requirement, link the required inspection, analysis, or test method; component, BOM, board, and firmware revisions; environment, load, and instruments; acceptance criteria; and result files. Record planned work and executed results as separate states.

As required, plan power, functional, timing, and protection checks; worst-case electrical analysis; vacuum thermal testing; thermal cycling; vibration and shock; EMI/EMC; and radiation and fault-recovery verification. Distinguish qualification, acceptance, and protoflight purposes and the corresponding test article types. Do not invent test levels, durations, or cycle counts without supporting requirements.

ERC/DRC checks configured connectivity and physical rules. Do not present these checks as comprehensive evidence of datasheet compliance, SOA, radiation tolerance, vacuum thermal behavior, or flight suitability. Before relying on CAD automation, verify the required open, edit, save, and reopen operations. Do not report unexecuted operations as successful.

## Stage Completion Criteria

| Stage | Required Results | Handling Unverified Items |
|---|---|---|
| Candidate BOM | Exact MPNs, source availability, functional and rating comparisons, and a list of risks and unknowns | Retain draft status and continue alternative evaluation and evidence gathering |
| Design review complete | DS-00 through DS-06, applicable SAT-01 through SAT-06, circuit/PCB/firmware condition checks, calculations, analyses, and a completed verification plan | Do not mark the stage complete with FAIL/UNVERIFIED items in scope; track scheduled physical tests separately under SAT-07 |
| Ground prototype fabrication readiness | Electrical, thermal, protection, and manufacturing documentation and reviews required for the prototype purpose and test scope; explicit mission-related unknowns and restrictions | Flight verification, including radiation work, may remain open, but must not be confused with the ground prototype scope |
| Flight-use decision | Traceability to applicable requirements, component and lot traceability, required analyses and test results, disposition of open items, and approval by the responsible authority | The agent cannot assign flight-approved status without the necessary evidence |

Complete each stage only with evidence for its defined scope. When tests required for a later stage are still planned, keep them explicitly incomplete even if an earlier review stage is complete. For an authorized stage-specific exception, record who accepted which requirement deviation and on what basis; do not convert that item into a technical pass.

## Change Impact and Continued Work

Trace changed design inputs to the affected component reviews, calculations, and tests. Do not automatically repeat identical calculations or the entire test suite. Reassess the affected scope when changes such as a new voltage, MPN, thermal path, firmware timing, PCB stackup, or manufacturing lot invalidate prior evidence.

Continue independent comparisons, research, documentation, drafts, and test planning even when undefined requirements block a final verdict. Clearly distinguish established facts from the next evidence to obtain.

Apply the [design decision process](design-reasoning.md) to significant changes. Rapid screening prioritizes later verification; it does not justify omitting SAT-01 through SAT-07 or stage completion criteria. When adopting a revision, update the linked calculations, tests, and review records together with the BOM, circuit, PCB, and firmware.
