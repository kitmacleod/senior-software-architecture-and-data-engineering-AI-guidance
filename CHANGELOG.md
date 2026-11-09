# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the project uses [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Planned

- Validate the instructions against representative Copilot notebook tasks.
- Record product-specific constraints discovered during practical use.
- Consider lightweight templates for project brief, data contract, risk log, and decision log.
- Decide and document the repository licence.

## [1.0.0] - 2026-11-09

### Added

- Created `copilot-notebook-instructions.md` as a concise operating contract for Copilot notebook work in software architecture and data engineering.
- Defined ten working modes: Explore, Specify, Architect, Plan, Implement, Debug, Review, Verify, Simplify, and Ship.
- Added an explicit instruction hierarchy covering user requests, project-specific sources, notebook instructions, the engineering playbook, and general engineering practice.
- Added rules for distinguishing evidence, inference, assumptions, recommendations, and unresolved questions.
- Added safeguards against unsupported claims about APIs, source content, benchmark results, costs, compliance, testing, deployment, and production behaviour.
- Added proportionate application of engineering methods based on importance, risk, scale, maturity, team capacity, and reversibility.
- Added cross-cutting requirements for security, privacy, reliability, data integrity, provenance, interoperability, observability, maintainability, performance, cost, portability, and operational ownership.
- Added domain-specific considerations for geospatial and environmental data, including coordinate reference systems, spatial and temporal resolution, identifiers, uncertainty, and quality flags.
- Added response-format guidance and a final completion check for substantial work.
- Created `engineering-playbook.md` as the detailed companion reference.
- Added discovery and specification methods, including problem framing, requirements, acceptance criteria, and time-boxed uncertainty spikes.
- Added an architecture method covering views, decision drivers, option assessment, architecture fitness checks, and an Architecture Decision Record template.
- Added detailed data-engineering guidance covering ownership, systems of record, data contracts, pipeline design, storage layers, data quality, provenance, lineage, schema evolution, backfills, and corrections.
- Added geospatial and environmental data guidance covering geometry, time, units, measurement methods, uncertainty, provisional states, changing metadata, and evaluation of standards such as CF, OGC APIs, ISO 19115, and INSPIRE.
- Added API guidance for HTTP, OpenAPI, AsyncAPI, messaging, idempotency, ordering, replay, dead-letter handling, versioning, and deprecation.
- Added security and privacy guidance covering threat modelling, least privilege, workload identity, secrets, supply-chain risk, audit events, denial-of-service controls, and assurance language.
- Added reliability, resilience, observability, operational readiness, testing, verification, debugging, incident analysis, technical review, delivery planning, migration, compatibility, and release-readiness methods.
- Added reusable templates for ADRs, review findings, and outcome-oriented tasks.
- Added reusable prompts for architecture, data pipelines, technical review, implementation planning, uncertainty analysis, and release assessment.
- Added maintenance guidance for treating the playbook as a versioned engineering product.
- Added `README.md` documenting purpose, structure, notebook setup, working modes, principles, versioning, maintenance, and limitations.
- Added this `CHANGELOG.md` to establish a transparent version history.

### Changed

- Adapted the lifecycle and quality principles from Addy Osmani's `agent-skills` approach into a Copilot notebook model rather than copying all skills into one persistent instruction block.
- Moved detailed specialist rules out of the notebook instructions and into the playbook to reduce instruction overload and improve selective application.
- Refined the earlier condensed instructions to make proportionality, evidence priority, conflict handling, simpler alternatives, and project-source precedence explicit.
- Strengthened data engineering from a general cross-cutting concern into a first-class discipline alongside software architecture.

### Design decisions

- Adopted a two-artefact model: concise persistent instructions plus a detailed selectable playbook.
- Kept files at the repository root for the initial release to simplify review and use in Copilot notebooks.
- Set the initial version to `1.0.0` because the artefacts form a coherent and usable baseline.
- Used British English consistently.
- Avoided claiming that notebook instructions are guaranteed to be enforced or that Copilot can run, test, deploy, or inspect systems without appropriate tools and evidence.

[Unreleased]: https://github.com/OWNER/REPOSITORY/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/OWNER/REPOSITORY/releases/tag/v1.0.0
