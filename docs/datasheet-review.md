# Component Datasheet Review Criteria

Governing rules: [AGENTS.md](../AGENTS.md) · Record: [Component review template](../templates/component-review.md)

## 1. Review Timing and Component Identity — DS-00

When comparing candidates, use primary documents to screen functionality, ratings, and package suitability. After selection, review the actual circuit and PCB conditions. Before finalizing the BOM, introducing an alternate, or preparing for fabrication, confirm that the evidence still applies to the current design. Unchanged documents do not need to be downloaded repeatedly, but their revision and applicability must still be checked.

Required identity information includes manufacturer, full MPN and suffix, function, reference designators (RefDes), package code, pin count and pinout, temperature grade, and quality and radiation grades. Distinguish orderable options with different ratings, dies, or test coverage. Check library symbols, footprints, exposed pads, and NC/DNC handling against the source documents.

For each source, record its URL, document number, revision, publication or revision date, access date, and the relevant page, section, table, figure, and footnote references. Record both PDF and printed page numbers when they differ. If the file is retained, record its path and SHA-256 so that the reviewed edition can be reproduced.

Prioritize manufacturer datasheets and supplement them with relevant errata, application notes, product change notices (PCNs), and quality or radiation reports. Record inaccessible sources, OCR errors, conflicting revisions, or missing information for the exact orderable part as `UNVERIFIED`. Do not transfer another part's application-note example into a guaranteed specification for the selected component.

## 2. Information Required for Every Numerical Value

| Category | Required Record |
|---|---|
| Manufacturer specification | Parameter, symbol, unit, Min/Typ/Max, and whether the value is guaranteed, characterized, or provided for reference |
| Conditions of applicability | Supply voltage, load and current, TA/TC/TJ, frequency, waveform, duty cycle, test circuit, and footnotes |
| Design requirement | Required performance or permitted stress, requirement ID, and supporting source |
| Actual use | Normal, startup, shutdown, standby, transient, and fault scenarios; applicable RefDes |
| Worst case | Minimum and maximum values including errors, tolerances, temperature, aging, and applicable radiation effects |
| Comparison criteria | Distinguish manufacturer restrictions from project restrictions and use their applicable intersection |
| Verdict | Equations, assumptions, input sources, results, units, margins, evidence type, status, and actions for unresolved items |

For an upper bound, record `margin = applicable upper limit − worst-case operating value`. For a lower bound, record `margin = worst-case operating value − applicable lower limit`. Calculate both margins for a two-sided limit. Preserve units and signs, and do not replace a multidimensional constraint such as SOA with a voltage-only or current-only margin. Determine whether a positive margin is sufficient using the project's minimum-margin requirements.

A `Typ` value alone is not a guaranteed upper or lower bound. Record reading uncertainty and characterization conditions for values taken from graphs. If a necessary guaranteed value is unavailable, obtain manufacturer clarification, suitable testing, or a different part. Estimates may still be developed, but must remain distinct from evidence used for final acceptance.

## 3. Six Mandatory Checks

### DS-01 — Absolute Maximum Ratings

- Check positive and negative supply and relevant pin voltages; per-pin, per-port, and total device currents; injection/clamp current; differential and common-mode limits; and junction temperature.
- Do not interpret storage temperature, soldering temperature, or ESD ratings as normal operating limits. Do not assume that all maximum ratings are simultaneously permissible.
- Evaluate supply tolerances and ripple, overshoot/undershoot, inductive spikes, reverse polarity, backfeeding, and signals applied to unpowered pins.
- Apply transient exceptions only when the manufacturer explicitly specifies the relevant conditions, duration, and repetition rate. A short duration alone is not evidence of acceptability.

Retain rating-table footnotes and scenario-specific stress comparisons as evidence. Absolute maximum ratings concern damaging stress limits; they do not define guaranteed normal functionality. [Manufacturer interpretation reference](sources.md#s1)

### DS-02 — Recommended Operating Conditions

- Compare actual operation with the specified supply and ripple, the applicable TA/TC/TJ limit, input range and common-mode voltage, clock, load, power sequencing, and ramp rate.
- Do not compare nominal rail labels alone. Include regulator error, wiring drop, load variation, and cold start.
- Intervals requiring normal operation must meet the specified operating conditions. Apply the manufacturer's separately defined conditions to intervals such as startup when provided.
- If a part has no section with this title, establish the operating range from the functional description and the conditions attached to guaranteed characteristics. Do not substitute absolute maximum ratings for an undefined operating range.

### DS-03 — Electrical Characteristics

Map each parameter's test conditions to its actual use. Confirm whether it is guaranteed across the required voltage, temperature, and load range. Even when a table includes Min/Max values, check footnotes for restrictions to particular conditions.

| Applicable Function | Representative Checks |
|---|---|
| Logic and interfaces | VIH/VIL, VOH/VOL load conditions, input leakage, pin capacitance, power-off behavior, and voltage-domain compatibility |
| MOSFETs and diodes | RDS(on) at the actual VGS and temperature, leakage, VF, Qg, Coss, reverse recovery, and applicable avalanche limits |
| Regulators and power ICs | Output error, dropout, IQ, minimum and maximum load, current-limit variation, stability and output-capacitor requirements, and reverse current |
| ADCs, DACs, sensors, and amplifiers | Input/output ranges, accuracy, offset, gain, noise, reference voltage, source impedance, and settling conditions |

Do not select a gate-drive voltage on the assumption that a MOSFET's `VGS(th)` fully enhances the device. Check the required RDS(on) and switching performance at the actual gate-drive conditions. [MOSFET interpretation reference](sources.md#s4)

### DS-04 — Thermal Characteristics

Calculate the losses generated in the device and define the actual thermal paths and boundary temperatures through the PCB, case, and satellite structure. Check repeated pulses and startup or fault transients as well as steady-state temperature.

- Distinguish the conditions represented by `θJA`, `θJC(top/bottom)`, `θJB`, `ΨJT/ΨJB`, and transient thermal impedance. Do not treat `Ψ` as an arbitrary thermal resistance.
- `TJ ≈ TA + P_loss × θJA` is an estimate restricted to the applicable θJA test conditions or a validated model. Do not directly apply a general datasheet θJA value to vacuum operation.
- `TJ ≈ TC + P_loss × θJC` is an approximation when the specified case path dominates and the assumed heat flow is valid. Do not automatically assume that all heat passes through the measured surface.
- Include the actual copper, vias, pads, TIM, contacts, mounting structure, and heat from neighboring components. Record sensor location and junction-temperature estimation uncertainty.
- Evaluate normal operating limits, project derating, and reliability restrictions together. Do not use thermal shutdown as a routine operating control point.

Use the [TI thermal metrics reference](sources.md#s2) for metric limitations and the [satellite board criteria](space-board.md) for mission boundary conditions.

Choose loss equations appropriate to the circuit. The following are basic relationships; they do not automatically include every loss in a real component.

| Target | Basic Relationship and Conditions |
|---|---|
| Resistive conduction | `P = I_RMS² × R`; use R at the applicable temperature and tolerance |
| MOSFET conduction | `P_cond ≈ I_RMS² × RDS(on)`; if RMS is calculated over the full evaluation period with zero current outside conduction intervals, do not multiply by duty cycle again |
| LDO | For a simple steady-state circuit, `P_loss ≈ (VIN − VOUT) × IOUT + VIN × IQ`; adjust for the IC's internal current paths |
| Converter | Steady-state average `P_loss = P_in − P_out`; allocate losses to the IC, FETs, inductors, and other locations where they occur, and do not treat output power as IC self-heating |
| Switching and pulses | `E_loss = ∫v(t)i(t)dt`; calculate repetitive loss from the applicable energy and repetition rate, avoiding double-counting with other loss equations |

State the assumptions and limitations of thermal calculations without detailed models. Do not mark the applicable flight thermal verification complete before the required tests are closed.

### DS-05 — Timing Characteristics

- Check applicable setup/hold times, minimum and maximum propagation delays, rise/fall times, minimum pulse width, duty cycle, maximum clock rate, and reset, power-good, startup, and settling times.
- Build a path budget including transmitter, receiver, routing, connectors, clock skew, and jitter. Confirm that supply voltage, temperature, load capacitance, and logic thresholds match the specification conditions.
- Check setup using the latest data arrival and hold using the earliest data change. A datasheet's maximum frequency alone does not establish interface timing closure.
- For gate drivers, check turn-on/off delays, variation, dead time, and the actual load. For power and protection circuits, check the total interval from detection through isolation and energy dissipation.

Record `setup margin = receiver deadline − latest data-valid time` and `hold margin = earliest data-change time − receiver hold-window end`. Apply clock skew and jitter on a consistent time reference. Review synchronizers and metastability mitigation separately for asynchronous signals. [Timing terminology reference](sources.md#s1)

### DS-06 — Peak / Continuous Current, SOA

- Distinguish continuous, average, RMS, peak, single-pulse, and repetitive-pulse currents. Record temperature, cooling, waveform, pulse width, duty cycle, and repetition rate numerically.
- Compare the MOSFET's VDS–ID trajectory with the SOA for the applicable duration and temperature. Low RDS(on), maximum current, or total energy alone does not establish acceptability during linear-mode operation or short-circuit protection.
- Do not apply single-pulse SOA directly to repetitive pulses or DC operation. SOA extrapolation and temperature correction require a manufacturer-supported method and applicability range.
- Review the entire current path, including pins and package, connector contacts, cables, vias, traces, shunts, and protection devices. Include simultaneously loaded contact count and temperature-rise conditions when evaluating connectors.
- Check that the combination of maximum current-limit threshold and shutdown delay does not exceed the protected component's electrical, thermal, or SOA limits. The presence of protection circuitry alone does not establish a pass.

Consult the [manufacturer SOA reference](sources.md#s3) for interpreting SOA plots and transient models, but base the final verdict on the selected component's source documents.

## 4. Non-IC Components and Interconnections

| Target | Checks at Component and Circuit Level |
|---|---|
| Capacitors | Effective capacitance versus voltage, temperature, DC bias, tolerance, and aging; ESR, ripple, surge, and polarity |
| Resistors and shunts | Power, working voltage, pulse energy, temperature coefficient, Kelvin connections, and measurement error |
| Inductors and transformers | Saturation and RMS current, temperature- and frequency-dependent losses, insulation, startup, and fault conditions |
| Connectors and wiring | Contact and wire current, contact resistance, temperature rise, mechanical retention, and mating security |
| PCB | Stackup, current and return paths, clearance, creepage, grounding, insulation, and thermal paths |

A component-level pass is distinct from correct board operation. Review power stability, complete decoupling loops, analog settling, signal integrity, EMI/EMC, and fault propagation at the interconnection level.

## 5. Verdicts and Reassessment

| Status | Meaning |
|---|---|
| PASS | Required evidence and applicability are established, and the criteria and margins are satisfied for the stated scope |
| FAIL | Verified source data, calculations, or tests demonstrate a requirement violation |
| UNVERIFIED | Documents, requirements, conditions, calculations, or tests are missing, or a change has invalidated the evidence |
| NOT_APPLICABLE | The item does not physically apply to the component or circuit; a reason and supporting evidence are required |

DS-00 identity and source traceability cannot be skipped for a populated component. For example, digital setup/hold may not apply to a resistor, but the absence of an SOA graph does not make the entire power and pulse review inapplicable. Do not mark DS-05 inapplicable without checking whether the chip has relevant timing requirements.

Evaluate an alternate part as a separate MPN. Update affected verdicts when voltage, load, firmware speed, routing, or cooling changes, even if the component is unchanged. When manufacturer documentation changes, inspect the differences and reassess the affected items.

When candidate selection, substitution, or improvement requires an engineering decision, apply the [design decision process](design-reasoning.md) and record the baseline, alternatives, hypotheses, comparison conditions, and results. Link individual DS verdicts to that record. A candidate's benefits cannot compensate for unmet DS-01 through DS-06 requirements.
