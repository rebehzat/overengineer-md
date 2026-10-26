# overengineer-md

An agent skill that takes a half-baked idea and turns it into an engineered, build-ready design package, in **any** engineering field: software, mechanical, electrical, civil, chemical, aerospace, bio, robotics, product or process.

It doesn't overcomplicate things. It overengineers the *rigor*: requirements with acceptance criteria, system architecture, trade studies, interface control, budgets and calcs, BOM, full technical stack, FMEA, compliance, a V&V plan and an EVT/DVT/PVT roadmap, all written in real technical jargon with real components and standards.

## Install

Copy the `overengineer-md/` folder (it holds `SKILL.md`) into your agent's skills directory, for example:

- Claude Code: `~/.claude/skills/overengineer-md/`
- Cursor / other agents that read `SKILL.md`: your skills folder

## Use

> use overengineer-md: a backpack that keeps my laptop cool

> overengineer this: an app that reminds me to drink water

You get one Markdown document, `<Codename>: Engineering Design Package`, with these sections:

0. TL;DR
1. Problem statement and assumptions
2. Disciplines involved
3. ConOps
4. Requirements
5. System architecture (mermaid diagram)
6. Technical stack (every layer: frontend, backend, servers, databases, hardware, CAD/CAE, process control and more, depending on the field, with a plain-language walkthrough)
7. Trade studies
8. Interface control
9. Engineering analysis and budgets
10. Security and data
11. BOM and manufacturing
12. Safety, compliance, FMEA, risk register
13. Verification and validation
14. Roadmap
15. Open questions and next actions

## Rules it follows

- The jargon has to be correct, and the components and standards have to be real.
- Every number shows its formula or is labelled `estimate`, `assumption` or `target`.
- Your core idea stays the same. Only the execution gets overengineered.

## License

MIT
