---
name: overengineer-md
description: >-
  Use this when someone hands you a half-baked idea (any field: software,
  mechanical, electrical, civil, chemical, aerospace, bio, robotics, product,
  process) and wants it turned into a fully engineered, build-ready design spec
  full of real technical components, standards, and jargon.
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
2. **Classify the disciplines.** Identify the primary domain and every secondary one it touches (e.g. a smart planter = mechanical + electrical + embedded firmware + cloud software + industrial design + agronomy). Each one gets its own subsystem later.
3. **ConOps.** Write a short Concept of Operations: actors, operating environment (temperature, load, users, network, regulatory context), modes of operation (nominal, degraded, maintenance, failure), and a 3 to 5 step user/operator journey.
4. **Requirements.** Make a numbered table (`REQ-001`…) split into functional, performance, non-functional (reliability, safety, security, maintainability, scalability) and constraints (budget, mass, power, size, compliance). Give each one a measurable acceptance criterion and a verification method (Test, Analysis, Inspection, Demonstration).
5. **System architecture.** Break the system into subsystems and components. Draw a `mermaid` block or flow diagram. For each subsystem, list concrete components, materials, or software, with a one-line justification.
6. **Trade studies.** For the two or three biggest design decisions, compare two or three options in a weighted decision matrix (criteria, weights, scores 1 to 5, totals) and state the winner and why.
7. **Interfaces (ICD).** Table every interface between subsystems: type (mechanical, electrical, data, fluid, thermal, human), protocol or standard, signal or load, rate, and connector or API.
8. **Engineering analysis.** Do the budgets and calcs that matter for this domain, showing the formulas:
   - Mass, power, and thermal budgets; link or data budget; cost budget
   - Structural: loads, stresses, factor of safety; fluids/thermal: flow, pressure drop, heat dissipation
   - Electrical: current draw, battery life, wire/trace sizing
   - Software: throughput, latency targets (p50/p99), storage growth, availability (nines), scaling model
   - Control: plant model, controller type (PID, MPC, state machine), sampling rate, stability margin
9. **Software, firmware and data stack** (if any computing is involved): language, frameworks, runtime, data model, deployment (CI/CD, IaC, containers, OTA updates), observability (metrics, logs, traces), and security (threat model via STRIDE, authN/authZ, encryption at rest and in transit, secrets management).
10. **Materials and manufacturing / build.** BOM table (item, spec, quantity, unit cost `estimate`, supplier type), manufacturing process (CNC, injection moulding, sheet metal, PCB assembly, casting, pour, fabrication, cloud provisioning), DFM/DFA notes and tolerances.
11. **Safety, compliance and risk.** Run an FMEA table (failure mode, effect, cause, Severity, Occurrence, Detection, RPN, mitigation). List applicable standards and regulations for the domain and region, and add a risk register for the top five project risks.
12. **Verification and validation.** Write a test plan that maps back to the `REQ-` IDs: unit/component tests, integration, environmental (thermal cycling, vibration, IP rating, load tests), HIL/SIL, field trials, and the pass/fail criteria for each.
13. **Roadmap.** Phase the work by TRL or maturity: proof of concept, prototype (EVT), design validation (DVT), production validation (PVT), launch and scale. Give each phase milestones, deliverables, rough duration and cost (`estimate`).
14. **Open questions and next actions.** List what is still unknown, which assumptions carry the most risk, and the first three concrete things to build or test this week.

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
## 6. Trade studies (decision matrices)
## 7. Interface control (table)
## 8. Engineering analysis and budgets
## 9. Software / firmware / data stack (if applicable)
## 10. BOM and manufacturing
## 11. Safety, compliance, FMEA, risk register
## 12. Verification and validation plan
## 13. Roadmap (EVT/DVT/PVT or equivalent)
## 14. Open questions and next actions
```

Skip a section only if it truly does not apply, and say so in one line. Give the project a cool codename.

## Quality bar

- Someone in that field should be able to start building from it.
- Every component has a reason, and every number has a source, formula, or `estimate` label.
- It is overengineered in rigor and detail, not in pointless complexity: if a simpler component meets the requirement, pick it and say it won the trade study.
