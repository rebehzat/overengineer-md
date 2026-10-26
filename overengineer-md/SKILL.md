---
name: overengineer-md
description: >-
  Use this when someone hands you a half-baked idea (any field: software,
  mechanical, electrical, civil, chemical, aerospace, bio, robotics, product,
  process) and wants it turned into a fully engineered, build-ready design spec
  full of real technical components, a full technical stack, standards, and
  jargon.
---
# overengineer-md

Turn a half-baked idea into an engineered, build-ready concept. The goal is **depth, not bloat**: every component, number and acronym earns its place, but the output should read like a design review package from a team that has shipped hard things.

## Voice and style rules

- Talk like a principal engineer in a design review. Dense, confident, precise. Use the real jargon of the discipline (e.g. *BOM, ICD, FMEA, DFM/DFA, tolerance stack-up, MTBF, SLO/SLA, p99 latency, PID loop, Bode plot, Reynolds number, factor of safety, TRL, ConOps, CAPEX/OPEX*).
- Name **real, specific** components, materials, software, protocols and standards (e.g. *STM32H7, ESP32-S3, 6061-T6 aluminium, PETG, Kubernetes, PostgreSQL, Kafka, ROS 2, CAN FD, MQTT, Modbus, LoRaWAN, ISO 9001, IEC 61508, ASME Y14.5, IPC-A-610, Eurocode 2, ISO 26262*). Pick ones that genuinely fit; never invent part numbers or standards.
- Jargon must be **correct**. If a term would be wrong for the context, don't use it.
- Numbers: show the calculation or label them clearly as `estimate`, `assumption`, or `target`. Never present a made-up figure as measured fact.
- Keep the user's core idea intact. Overengineer the *execution*, not the *goal*.
- Use tables, a `mermaid` block diagram, and code/pseudocode blocks where they beat prose.

## Steps

1. **Parse the idea.** Restate it in one line as a problem statement: who has the problem, what the system does, and what success looks like. List the unknowns you had to assume, and pick sensible defaults rather than stalling.
2. **Classify the disciplines.** Identify the primary domain and every secondary one it touches (e.g. a smart planter = mechanical + electrical + embedded firmware + cloud software + industrial design + agronomy). Each one gets its own subsystem and its own stack layers later.
3. **ConOps.** Write a short Concept of Operations: actors, operating environment (temperature, load, users, network, regulatory context), modes of operation (nominal, degraded, maintenance, failure), and a 3 to 5 step user/operator journey.
4. **Requirements.** Make a numbered table (`REQ-001`…) split into functional, performance, non-functional (reliability, safety, security, maintainability, scalability) and constraints (budget, mass, power, size, compliance). Give each one a measurable acceptance criterion and a verification method (Test, Analysis, Inspection, Demonstration).
5. **System architecture.** Break the system into subsystems and components. Draw a `mermaid` block or flow diagram. For each subsystem, list concrete components, materials, or software, with a one-line justification.
6. **Technical stack.** Spell out, for a human reader, *everything* that will be used to build, run and maintain the thing, layer by layer. Use one table per layer with columns **Layer / Choice / What it does here / Why this over alternatives**. Include every layer that applies to the disciplines from step 2, for example:
   - **Software / web / app:** frontend (framework, UI kit, state management, build tool), mobile (native or cross-platform), backend (language, framework, API style REST/GraphQL/gRPC), auth, databases (OLTP, cache, search, object storage, time-series), messaging/queues, background jobs, AI/ML models and serving, third-party APIs, servers and hosting (cloud provider, regions, VMs/containers/serverless, CDN, DNS, load balancer), infrastructure as code, CI/CD, observability, security tooling, dev tooling (repo, IDE, testing frameworks).
   - **Embedded / electrical / robotics:** MCU/SoC/FPGA, sensors, actuators, motor drivers, power electronics and battery chemistry, PCB stack-up and EDA tool (KiCad, Altium), RTOS or embedded Linux, firmware language and toolchain, middleware (ROS 2, Zephyr), comms buses and radios, bootloader and OTA, HIL rigs.
   - **Mechanical / aerospace / product:** CAD (SolidWorks, Fusion 360, CATIA, Onshape), CAE/FEA/CFD (ANSYS, Abaqus, OpenFOAM, COMSOL), materials and finishes, fasteners and bearings, manufacturing processes and machines, metrology, PLM/PDM.
   - **Civil / structural / architecture:** structural system, materials grades, BIM and analysis software (Revit, Tekla, ETABS, SAP2000, Civil 3D), geotech approach, MEP systems, construction method and plant, monitoring sensors.
   - **Chemical / process / energy / bio:** unit operations and equipment, reactor or bioreactor type, process simulation (Aspen Plus/HYSYS, DWSIM, MATLAB/Simulink), control system (PLC, DCS, SCADA, historian), instrumentation (P&ID tags), lab and QA/QC methods, utilities.
   - **Ops layer for anything physical:** how it is monitored, serviced and updated in the field (IoT platform, telemetry, CMMS, spare parts, firmware fleet management).
   End the step with a short plain-language paragraph that walks a non-specialist through how the whole stack fits together, from the user's first touch to the deepest component.
7. **Trade studies.** For the two or three biggest design decisions (often stack choices), compare two or three options in a weighted decision matrix (criteria, weights, scores 1 to 5, totals) and state the winner and why.
8. **Interfaces (ICD).** Table every interface between subsystems: type (mechanical, electrical, data, fluid, thermal, human), protocol or standard, signal or load, rate, and connector or API.
9. **Engineering analysis.** Do the budgets and calcs that matter for this domain, showing the formulas:
   - Mass, power, and thermal budgets; link or data budget; cost budget
   - Structural: loads, stresses, factor of safety; fluids/thermal: flow, pressure drop, heat dissipation
   - Electrical: current draw, battery life, wire/trace sizing
   - Software: throughput, latency targets (p50/p99), storage growth, availability (nines), server sizing and scaling model
   - Control: plant model, controller type (PID, MPC, state machine), sampling rate, stability margin
10. **Security and data** (when anything is connected or stores data): threat model via STRIDE, authN/authZ, encryption at rest and in transit, secrets management, privacy and data retention, applicable data laws.
11. **Materials and manufacturing / build.** BOM table (item, spec, quantity, unit cost `estimate`, supplier type), manufacturing or deployment process (CNC, injection moulding, sheet metal, PCB assembly, casting, pour, fabrication, cloud provisioning), DFM/DFA notes and tolerances.
12. **Safety, compliance and risk.** Run an FMEA table (failure mode, effect, cause, Severity, Occurrence, Detection, RPN, mitigation). List applicable standards and regulations for the domain and region, and add a risk register for the top five project risks.
13. **Verification and validation.** Write a test plan that maps back to the `REQ-` IDs: unit/component tests, integration, environmental (thermal cycling, vibration, IP rating, load tests), HIL/SIL, load and penetration tests for software, field trials, and the pass/fail criteria for each.
14. **Roadmap.** Phase the work by TRL or maturity: proof of concept, prototype (EVT), design validation (DVT), production validation (PVT), launch and scale (or MVP, beta, GA for software). Give each phase milestones, deliverables, rough duration and cost (`estimate`).
15. **Open questions and next actions.** List what is still unknown, which assumptions carry the most risk, and the first three concrete things to build or test this week.

## Output format

Deliver one Markdown document with these sections, in this order:

```
# <Project codename>: Engineering Design Package
## 0. TL;DR (3 lines: what it is, how it works, key numbers)
## 1. Problem statement and assumptions
## 2. Disciplines involved
## 3. ConOps
## 4. Requirements (table)
## 5. System architecture (mermaid + component list)
## 6. Technical stack (one table per layer + plain-language walkthrough)
## 7. Trade studies (decision matrices)
## 8. Interface control (table)
## 9. Engineering analysis and budgets
## 10. Security and data (if applicable)
## 11. BOM and manufacturing
## 12. Safety, compliance, FMEA, risk register
## 13. Verification and validation plan
## 14. Roadmap (EVT/DVT/PVT, MVP/beta/GA, or equivalent)
## 15. Open questions and next actions
```

Skip a section only if it truly does not apply, and say so in one line. Give the project a cool codename.

## Quality bar

- Someone in that field should be able to start building from it, and a non-specialist should understand from the technical stack section what is being used and why.
- Every component has a reason, and every number has a source, formula, or `estimate` label.
- It is overengineered in rigor and detail, not in pointless complexity: if a simpler component meets the requirement, pick it and say it won the trade study.
