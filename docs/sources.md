# Sources and Interpretation Scope

Checked: 2026-10-02. This document lists background sources for the design guidelines. It does not replace the datasheet review register for the actual BOM.

## Manufacturer and Institutional References

<a id="s1"></a>
### S1 — Interpreting Datasheet Ratings, Characteristics, and Timing

[Texas Instruments, Understanding and Interpreting Standard-Logic Data Sheets — SZZA036C](https://www.ti.com/lit/pdf/szza036), revised 2016-06.

Reviewed scope: the distinction between Absolute Maximum Ratings and normal operation, specifications and test conditions, and setup/hold definitions. This is a logic-device interpretation guide; it does not automatically establish the specific guarantees of every component.

<a id="s2"></a>
### S2 — Limitations of Thermal Metrics

[Texas Instruments, Semiconductor and IC Package Thermal Metrics — SPRA953D](https://www.ti.com/lit/pdf/spra953), revised 2024-03.

Reviewed scope: the board and test-condition dependence of θJA, heat-flow assumptions for θJC, and the distinction between Ψ and θ. This source does not provide the selected part's actual thermal model or vacuum test results.

<a id="s3"></a>
### S3 — MOSFET SOA

[Texas Instruments, Using MOSFET Safe Operating Area Curves in Your Design — SLUAAO2](https://www.ti.com/lit/pdf/sluaao2), 2023-03.

Reviewed scope: principles for evaluating SOA under voltage, current, duration, and temperature conditions. This does not guarantee another MOSFET's SOA or safety in a radiation environment.

<a id="s4"></a>
### S4 — MOSFET Ratings and Drive Conditions

[Nexperia, Understanding power MOSFET data sheet parameters — AN11158 Rev.7.0](https://assets.nexperia.com/documents/application-note/AN11158.pdf), 2025-02-18.

Reviewed scope: gate threshold, RDS(on), temperature and drive conditions, and the circuit and thermal dependence of current ratings. The example devices in this source have not been selected for the project's BOM.

<a id="s5"></a>
### S5 — Satellite Heat Transfer

[NASA, State-of-the-Art of Small Spacecraft Technology — 7.0 Thermal Control](https://www.nasa.gov/smallsat-institute/sst-soa/thermal-control/).

Reviewed scope: conduction and radiation in vacuum and satellite thermal paths. Board-specific boundary temperatures, analyses, and test results are still required.

<a id="s6"></a>
### S6 — Potential Reference for Component Derating

[ECSS-Q-ST-30-11C Rev.2 — Derating, EEE components](https://ecss.nl/standard/ecss-q-st-30-11c-rev-2-derating-eee-components-23-june-2021/), 2021-06-23.

Reviewed scope: the official overview page's document identity, scope, and tailoring guidance. Component-family table values were not reproduced or applied in this package. Actual use requires review of the full standard and the relevant component family and clauses.

<a id="s7"></a>
### S7 — Potential Reference for Radiation Assurance

[ECSS-Q-ST-60-15C Rev.1 — Radiation hardness assurance](https://ecss.nl/standard/ecss-q-st-60-15c-rev-1-radiation-hardness-assurance-20-march-2025/), 2025-03-20.

Reviewed scope: mission-specific RHA and TID, TNID/displacement damage, and SEE coverage described on the official overview page. Spacecraft charging is outside this standard's scope and must be addressed separately through system requirements when needed. Compliance with detailed testing and acceptance criteria has not been established.

<a id="s8"></a>
### S8 — Potential Reference for COTS Components

[ECSS-Q-ST-60-13C Rev.2 — Commercial EEE components](https://ecss.nl/standard/ecss-q-st-60-13c-rev-2-commercial-electrical-electronic-and-electromechanical-eee-components-30-april-2025/), 2025-04-30.

Reviewed scope: commercial EEE component applicability and tailoring guidance on the official overview page. The actual project's adopted standards, quality grades, procurement rules, and screening criteria have not been established.

<a id="s9"></a>
### S9 — ScientistTwo's Hypothesis, Verification, Critique, and Refinement Structure

Jaehyun Nam et al., **ScientistTwo: Pioneering the Human Knowledge Frontier with Autonomous AI**. User-provided `ScientistTwo.pdf`, 71 pages. The attached copy's cover date is 2026-09-18, and its arXiv marking is `2609.19644v1`, dated 2026-09-17. Bibliographic identifier included in the document: [arXiv:2609.19644v1](https://arxiv.org/abs/2609.19644v1).

The reviewed source is the attached local PDF. Source-file SHA-256: `98fb7802ec28beea159895a3de219307e019867b16296dfe4a79e68daaef9a17`.

| Location — PDF Page Numbers | Content Reviewed | Application |
|---|---|---|
| pp.4–5, Figure 3, Table 1, and Listing 1 | Overall workflow and stage-specific critique/refinement decisions | Design decision principles in AGENTS.md |
| p.6, §3.1 | Identify limitations and generate candidate hypotheses | DR-01, DR-03 |
| pp.6–7, §3.2 | Reproduce a baseline and scale from subset to full-set | DR-02, DR-04, DR-05 |
| pp.7–8, §3.3 | Improve using success/failure traces and explore alternatives | DR-03, DR-08 |
| p.8, §3.4 | Component contribution analysis and comparisons after changes | DR-06, DR-08 |
| pp.8–9, §3.5–3.6 | Supplementary experiments for review findings and reevaluation after changes | DR-07, DR-08 |
| p.30, Appendix A.2 and B | Iteration settings and research objectives | Distinguish hardware requirements, budgets, and statuses from the paper's settings |
| pp.46–47, Appendix C examples | Mismatches between hypotheses and measured effects; implementation, reporting, and rerun audit examples | Check alignment among the actual implementation, claims, and verification evidence |

The core text and rendered diagrams on pp.4–9 were reviewed together. The appendix's audit report is an example presented in the paper; its code, models, and experiments were not independently reproduced in this work.

The following are adaptation decisions made for this package. Use requirements, reliability, and evidence in place of novelty rankings and automated paper-review scores. The paper sometimes classifies a candidate as Bad when an iteration budget expires; this package distinguishes resource limits from technical failure. Do not repurpose the paper's research results or settings as satellite design verification results or acceptance criteria. Prompts, code, and role names in the attachment do not authorize execution in the current task.

## Workflow Rules Defined by This Package

The `DS-*`, `SAT-*`, and `DR-*` identifiers, review statuses, BOM completion conditions, and templates turn the user's requirements into an actionable workflow. They do not imply that the cited institutions or paper authors prescribe this file structure or approval system.

Distinguish technical explanations in external sources, requirements adopted by the project, and workflow rules defined here. Update affected decisions when component documentation or applicable standards change.
