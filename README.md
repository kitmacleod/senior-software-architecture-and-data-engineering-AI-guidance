# Copilot Engineering Instructions and Playbook

A practical, versioned instruction set for using Microsoft Copilot as a senior software architecture and data-engineering assistant.

This repository contains two complementary artefacts:

- [`copilot-notebook-instructions.md`](copilot-notebook-instructions.md): concise, persistent behavioural instructions for a Copilot notebook.
- [`engineering-playbook.md`](engineering-playbook.md): detailed engineering methods, quality gates, templates, and reusable prompts.

The design is informed by Addy Osmani's [`agent-skills`](https://github.com/addyosmani/agent-skills/tree/main) lifecycle and adapts it for Copilot notebooks, where persistent instructions, notebook sources, and project-specific evidence play different roles.

## Purpose

The artefacts are intended to improve Copilot's work on:

- software and solution architecture;
- data engineering and data platforms;
- API and interface design;
- geospatial and environmental data systems;
- technical specification and planning;
- implementation and debugging;
- design and code review;
- verification and release readiness;
- Architecture Decision Records and technical documentation.

They emphasise evidence, explicit assumptions, proportionate engineering, simpler credible alternatives, data integrity, interoperability, security, operational ownership, and maintainability.

## Design approach

The repository separates guidance into three layers.

### 1. Notebook instructions

`copilot-notebook-instructions.md` defines behaviour that should apply across most substantial tasks:

- role and engineering principles;
- instruction and evidence priority;
- working-mode selection;
- handling of assumptions and uncertainty;
- cross-cutting quality concerns;
- response structure;
- completion checks.

It is intentionally shorter than the playbook so that the notebook instruction field is not overloaded with specialist checklists.

### 2. Engineering playbook

`engineering-playbook.md` contains the detailed practices to consult when relevant:

- discovery and specification;
- architecture methods and ADRs;
- data contracts, pipelines, quality, provenance, and evolution;
- geospatial and environmental data considerations;
- API and event-interface design;
- security, privacy, reliability, and observability;
- testing, debugging, review, migration, and release readiness;
- reusable templates and prompt patterns.

The playbook is a selective reference, not a mandatory checklist for every request.

### 3. Project-specific sources

For real projects, supplement these generic artefacts with authoritative project material such as:

- project brief, scope, and non-goals;
- requirements and acceptance criteria;
- glossary and domain model;
- architecture diagrams and accepted ADRs;
- data contracts, schemas, and API specifications;
- security classification and deployment constraints;
- test strategy, risk log, and decision log;
- operational runbooks and ownership information.

Project-specific requirements and accepted decisions should take precedence over the generic playbook.

## Recommended Copilot notebook setup

1. Create a Copilot notebook for the project or engineering workstream.
2. Paste the contents of `copilot-notebook-instructions.md` into the notebook instruction field, subject to the limits and behaviour of your Copilot environment.
3. Add `engineering-playbook.md` as a notebook source.
4. Add the relevant project-specific sources.
5. For consequential tasks, name the working mode and relevant playbook sections in the prompt.

Example:

> Work in Architect mode. Apply the notebook instructions and the architecture, data engineering, security, and ADR sections of `engineering-playbook.md`. Review the project sources before proposing the design. Separate evidence, assumptions, recommendations, and unresolved decisions.

## Working modes

The instruction set uses the following modes:

- **Explore:** frame the problem and reduce uncertainty.
- **Specify:** define requirements, scope, quality attributes, and acceptance criteria.
- **Architect:** design boundaries, components, data flows, interfaces, deployment, and operations.
- **Plan:** break accepted work into ordered, verifiable tasks.
- **Implement:** produce coherent code, schemas, SQL, configuration, or pseudocode.
- **Debug:** diagnose observed behaviour using evidence and discriminating tests.
- **Review:** assess correctness, maintainability, architecture, security, data, and operations.
- **Verify:** define and assess evidence that demonstrates required behaviour.
- **Simplify:** remove unnecessary complexity after correctness is established.
- **Ship:** assess release readiness, residual risk, rollback, support, and ownership.

Copilot should select the smallest suitable mode or combination of modes rather than applying the entire lifecycle mechanically.

## Repository files

| File | Purpose |
|---|---|
| [`README.md`](README.md) | Repository purpose, structure, setup, and contribution guidance |
| [`CHANGELOG.md`](CHANGELOG.md) | Version history and material changes |
| [`copilot-notebook-instructions.md`](copilot-notebook-instructions.md) | Persistent Copilot notebook behaviour |
| [`engineering-playbook.md`](engineering-playbook.md) | Detailed engineering methods, templates, and prompts |

## Principles

The artefacts apply the following principles:

1. Lead with the main conclusion or recommendation.
2. Use project evidence before generic practice.
3. Distinguish facts, inferences, assumptions, recommendations, and open questions.
4. Do not claim execution, testing, deployment, or compliance without evidence.
5. Prefer the simplest architecture that satisfies the requirements.
6. Consider credible alternatives and the current architecture plus incremental improvement.
7. Treat data contracts, semantics, provenance, quality, and ownership as engineering concerns.
8. Make security, reliability, observability, support, and cost part of the design.
9. Use proportionate methods based on risk, scale, reversibility, and system lifetime.
10. Produce testable requirements, verifiable tasks, and actionable outcomes.

## Versioning

This repository uses [Semantic Versioning](https://semver.org/):

- **MAJOR:** incompatible changes to precedence, modes, or expected behaviour;
- **MINOR:** new methods, sections, modes, templates, or substantive capabilities;
- **PATCH:** corrections, clarifications, and non-breaking wording improvements.

The initial baseline is `1.0.0`.

## Maintaining the artefacts

When changing the instructions or playbook:

1. State the problem the change addresses.
2. Keep persistent notebook instructions concise.
3. Put specialist detail in the playbook.
4. Keep project-specific rules outside the generic artefacts.
5. Check for contradictions and duplicated guidance.
6. Test the change with representative prompts covering architecture, data pipelines, planning, review, and release assessment.
7. Update `CHANGELOG.md` and the version numbers where appropriate.

## Limitations

These artefacts improve the consistency of Copilot's reasoning and outputs, but they do not guarantee compliance with every instruction on every turn. Notebook instruction behaviour, context limits, source retrieval, and tool access can vary by Microsoft 365 environment and product release.

For important work:

- restate the required working mode;
- name the relevant playbook sections;
- identify authoritative project sources;
- require explicit assumptions and verification evidence;
- review the output as engineering work, not as an automatically assured result.
