# Engineering Playbook for Software Architecture and Data Engineering

Version: 1.0.0  
Status: Baseline playbook  
Companion instructions: `copilot-notebook-instructions.md`

## 1. Purpose

This playbook provides reusable methods, quality gates, and templates for software architecture and data engineering. It is designed to be consulted selectively by Copilot and by human contributors. It is not a mandatory checklist for every task.

The companion notebook instructions define persistent behaviour. This playbook supplies deeper methods for relevant tasks. Project-specific requirements and accepted decisions take precedence.

## 2. How to use the playbook

1. Select the sections relevant to the request and risk profile.
2. Confirm the project context and authoritative sources.
3. Tailor the method to the system's scale, maturity, criticality, and team capacity.
4. Record material assumptions and decisions.
5. Produce evidence appropriate to the claim being made.
6. Apply a lightweight method to reversible, low-risk work and a more rigorous method to consequential or hard-to-reverse work.

Do not apply every section mechanically. A small internal script does not need the same governance as a public API, hydrological archive, safety-relevant service, or long-lived research infrastructure.

## 3. Definition of a good engineering outcome

A good outcome:

- solves a defined user or organisational problem;
- has explicit scope and non-goals;
- is understandable by its maintainers;
- uses the simplest architecture that meets the requirements;
- preserves data meaning, quality, provenance, and security;
- exposes stable, testable contracts;
- fails predictably and can recover;
- is observable and supportable;
- can evolve without unnecessary disruption;
- has proportionate documentation and evidence;
- has clear ownership and sustainable operating costs.

## 4. Discovery and specification

### 4.1 Problem framing

Capture:

- problem or opportunity;
- affected users and stakeholders;
- current process and pain points;
- desired outcomes and measurable success;
- scope and non-goals;
- known constraints;
- major assumptions;
- decisions already made;
- evidence supporting the proposed work.

Avoid converting a requested technology directly into a requirement. Ask what capability or outcome the technology is expected to provide.

### 4.2 Requirements

Separate:

- functional requirements;
- quality attributes;
- data requirements;
- interface requirements;
- security and privacy requirements;
- operational and support requirements;
- migration and compatibility requirements;
- legal, policy, licensing, and records-management constraints.

Use requirement identifiers where traceability adds value. Write acceptance criteria as observable outcomes rather than implementation instructions.

Example:

> **REQ-DQ-004:** A published daily station series shall identify missing, provisional, and quality-controlled observations distinctly.  
> **Acceptance:** Contract tests confirm that each state has an unambiguous machine-readable representation and documented meaning.

### 4.3 Uncertainty and spikes

For a consequential unknown, define a time-boxed investigation with:

- question to answer;
- evidence required;
- method;
- time limit;
- decision enabled;
- stopping rule;
- output, such as an ADR, benchmark, prototype, or risk update.

A spike is not an unbounded prototype and should not silently become production code.

## 5. Architecture method

### 5.1 Architecture views

Use only the views needed to explain and evaluate the system:

- context: users, external systems, trust boundaries;
- container or service: deployable units and responsibilities;
- component: important internal boundaries;
- data flow: creation, transformation, storage, publication, and deletion;
- deployment: environments, networks, regions, runtime dependencies;
- sequence: important runtime interactions and failure behaviour.

C4 terminology and Mermaid diagrams are suitable defaults, but notation is secondary to clarity.

### 5.2 Decision drivers

Rank the drivers that distinguish the options. Typical drivers include:

- user value and time to value;
- data volume, velocity, variety, and sensitivity;
- latency and availability;
- integrity and reproducibility;
- interoperability;
- team skills and organisational ownership;
- deployment and procurement constraints;
- security and regulatory obligations;
- cost and expected lifetime;
- reversibility and lock-in.

Do not compare options against an unranked list of every desirable quality.

### 5.3 Option assessment

For each credible option document:

- concise description;
- assumptions;
- strengths against the ranked drivers;
- weaknesses and failure modes;
- implementation and migration implications;
- operational model and ownership;
- cost drivers;
- lock-in and exit path;
- evidence still needed.

Always consider the current architecture plus incremental improvement as an option. Prefer a modular monolith or managed platform over distributed services unless independent scaling, deployment, ownership, isolation, or resilience creates a demonstrable benefit.

### 5.4 Architecture Decision Record template

```markdown
# ADR-NNN: Decision title

- Status: Proposed | Accepted | Superseded | Deprecated
- Date: YYYY-MM-DD
- Owners:
- Review date:

## Context

## Decision drivers

## Options considered

## Decision

## Consequences

### Positive

### Negative

### Risks and mitigations

## Validation evidence

## Supersedes or is superseded by
```

### 5.5 Architecture fitness checks

Where valuable, automate checks that protect architectural characteristics, such as:

- dependency-direction tests;
- API and schema compatibility tests;
- security-policy checks;
- latency or throughput thresholds;
- prohibited dependency checks;
- data-quality and lineage completeness checks.

## 6. Data engineering

### 6.1 Data product and ownership

For each material dataset or stream define:

- business or scientific purpose;
- authoritative producer and system of record;
- accountable owner and operational steward;
- intended consumers and permitted uses;
- sensitivity and access classification;
- service expectations;
- retention, deletion, licensing, and archival obligations;
- escalation route for quality or availability issues.

Do not call a dataset authoritative without governance, ownership, and a controlled publication process.

### 6.2 Data contracts

A data contract should cover, where relevant:

- stable dataset or event identifier;
- schema and field definitions;
- required and optional fields;
- types, formats, enumerations, units, and null semantics;
- primary, natural, and foreign keys;
- timestamps, time zones, calendars, and validity intervals;
- spatial reference system and geometry rules;
- quality flags and uncertainty;
- ordering, deduplication, and delivery semantics;
- freshness, completeness, and availability expectations;
- compatibility and deprecation policy;
- sample valid and invalid records;
- ownership and support contact.

Contracts should be machine-testable where practical. JSON Schema, Avro, Protobuf, OpenAPI, AsyncAPI, SQL constraints, and table-format schemas may each be appropriate depending on the interface.

### 6.3 Pipeline design

Design for:

- idempotent processing;
- restartability from known checkpoints;
- deterministic transformation where possible;
- safe retries with bounded backoff;
- duplicate, late, missing, revised, and out-of-order records;
- reconciliation to authoritative totals or source extracts;
- quarantine or rejection of invalid records;
- replay and backfill without corrupting current outputs;
- separation of code, configuration, secrets, and data;
- auditable release of pipeline and schema changes.

A pipeline diagram should identify source, ingestion, raw preservation, validation, transformation, curated storage, publication, metadata, monitoring, and failure paths.

### 6.4 Storage layers

Use layers only when they establish useful control boundaries. A typical distinction is:

- source or landing: received representation with immutable capture metadata;
- validated: structurally and semantically checked data;
- curated: harmonised, quality-controlled, consumer-ready entities;
- published: versioned products and interfaces with explicit contracts.

Avoid uncontrolled copies, ambiguous labels such as “final,” and layers that add latency and cost without governance value.

### 6.5 Data quality

Define rules against relevant dimensions:

- validity;
- completeness;
- uniqueness;
- consistency;
- timeliness or freshness;
- accuracy, where a defensible reference exists;
- spatial, temporal, and semantic coherence.

For each critical rule specify:

- scope and rationale;
- executable test;
- threshold and its owner;
- severity;
- action on failure;
- reporting and escalation;
- exception and waiver process.

Do not confuse “pipeline completed” with “data is fit for use.” Monitor content as well as execution.

### 6.6 Provenance and lineage

Record enough information to answer:

- who or what produced the data;
- source identifiers and retrieval time;
- applicable licence and access constraints;
- transformations and software versions;
- reference data and configuration used;
- quality-control actions;
- output version and publication time;
- lineage from published value back to source.

Use open provenance models such as W3C PROV where their interoperability benefit justifies implementation. A simpler controlled lineage model may be more maintainable for a bounded system.

### 6.7 Schema and semantic evolution

Classify changes as compatible, conditionally compatible, or breaking. Define rules for:

- additive fields;
- optionality changes;
- type or unit changes;
- identifier changes;
- enumeration changes;
- semantic corrections;
- field removal;
- parallel versions and deprecation periods;
- migration and consumer communication.

A syntactically compatible change can still be semantically breaking. Unit, method, quality-state, or interpretation changes require explicit treatment.

### 6.8 Backfills and corrections

A backfill plan should state:

- reason and affected range;
- source snapshot and transformation version;
- isolation from routine processing;
- capacity and cost controls;
- idempotency and checkpoint strategy;
- comparison and reconciliation method;
- publication and cache implications;
- rollback or correction approach;
- consumer notification.

### 6.9 Geospatial and environmental data

Explicitly address:

- coordinate reference system, axis order, and transformation method;
- geometry type, dimensionality, precision, topology, and validity;
- spatial extent, resolution, support, and indexing;
- temporal extent, resolution, time zone, calendar, and aggregation period;
- observed, derived, modelled, forecast, and scenario values;
- variable definitions, units, measurement methods, and detection limits;
- uncertainty, quality flags, censoring, and provisional status;
- feature, station, catchment, variable, and dataset identifiers;
- changing station metadata and time-varying relationships;
- conventions such as CF, OGC APIs, ISO 19115, INSPIRE, or domain vocabularies when they demonstrably improve interoperability.

Evaluate a standard by semantic coverage, adoption, governance, implementation burden, conformance testing, tooling, and long-term stewardship. Standards compliance is not a substitute for a usable documented profile.

## 7. API and interface design

### 7.1 Contract first

Begin with consumer use cases and domain concepts. Define:

- resources or operations;
- identifiers and lifecycle;
- request and response schemas;
- validation and error model;
- authentication and authorization;
- filtering, sorting, pagination, and field selection;
- caching and conditional requests;
- idempotency and retries;
- quotas and rate behaviour;
- compatibility, versioning, and deprecation;
- representative examples.

Use OpenAPI for HTTP APIs and AsyncAPI for event interfaces when their ecosystem benefits justify the maintenance overhead.

### 7.2 HTTP guidance

Use HTTP semantics consistently. Provide stable machine-readable error codes and human-readable detail. Distinguish client errors, authentication failures, authorization failures, conflicts, rate limits, and transient service failures. Avoid exposing internal implementation details.

For large data, consider asynchronous jobs, bulk transfer, object-storage delivery, partitioned access, or domain-specific query services rather than forcing every use case through synchronous JSON responses.

### 7.3 Event and message interfaces

Define:

- event owner and business meaning;
- schema and version;
- key and partitioning strategy;
- ordering guarantees;
- delivery semantics;
- deduplication and idempotent consumption;
- retry, dead-letter, replay, and retention behaviour;
- sensitive-data controls;
- observability and consumer support.

“Exactly once” should not be claimed without defining the boundary and mechanism. End-to-end effects usually require idempotency and reconciliation.

## 8. Security, privacy, and misuse

### 8.1 Threat modelling

For material systems, identify:

- assets and sensitive data;
- actors and trust boundaries;
- entry points and privileged operations;
- threats and abuse cases;
- controls and residual risks.

STRIDE can structure technical threats; privacy threat modelling and data-protection impact assessment may be needed separately. Use proportionate methods rather than treating a checklist as assurance.

### 8.2 Baseline controls

Consider:

- least privilege and separation of duties;
- strong identity and workload identity;
- authorization at every protected operation;
- secret storage and rotation;
- validation, encoding, and safe query construction;
- encryption and key management;
- tenant and user isolation;
- dependency provenance and vulnerability management;
- secure build and deployment;
- tamper-evident audit events;
- logging without sensitive-data leakage;
- backup, restoration, retention, and secure deletion;
- denial-of-service, scraping, and resource-exhaustion controls.

Use OWASP ASVS, OWASP API Security Top 10, NIST Secure Software Development Framework, or relevant organisational standards as reference frameworks where appropriate.

### 8.3 Assurance language

Distinguish:

1. control proposed;
2. control implemented;
3. control tested;
4. control monitored;
5. control independently assured.

Do not describe a system as compliant based solely on design intent.

## 9. Reliability and resilience

Define service objectives only where there is a user or operational need. Relevant measures include availability, latency percentiles, success rate, freshness, completeness, recovery time objective, recovery point objective, and error budget.

For each critical dependency identify:

- failure modes;
- timeout and retry policy;
- circuit breaking or load shedding;
- degradation behaviour;
- isolation boundaries;
- recovery and reconciliation;
- ownership and escalation.

Backups are not evidence of recoverability. Test restoration at a cadence justified by criticality and change rate.

## 10. Observability and operations

### 10.1 Observability design

Design signals around user journeys and system risks rather than collecting everything. Use:

- structured logs with correlation identifiers;
- metrics for demand, errors, latency, saturation, and data freshness;
- traces for important distributed paths;
- data-quality and lineage events;
- audit events for security-relevant actions.

Define actionable alerts with an owner, threshold rationale, runbook, and expected response. Avoid alerts that are unactionable or duplicate downstream symptoms.

### 10.2 Operational readiness

Before release confirm:

- service and component ownership;
- dashboards and alerts;
- runbooks for likely failures;
- dependency and certificate expiry monitoring;
- capacity and quota monitoring;
- backup and restore procedures;
- incident communication and escalation;
- support hours and expected response;
- maintenance, patching, and end-of-life policy;
- cost monitoring and budget ownership.

## 11. Testing and verification

### 11.1 Evidence pyramid

Use the cheapest evidence that proves the requirement:

- review and static analysis;
- formatting, linting, and type checks;
- unit and property-based tests;
- schema, contract, and data-quality tests;
- component and integration tests;
- end-to-end tests;
- performance, resilience, security, migration, and recovery tests.

Do not maximise test count. Focus on important behaviour, boundaries, failure modes, and regressions.

### 11.2 Test design

Use Given/When/Then or an equivalent form for acceptance tests. Include:

- representative normal cases;
- boundary values;
- malformed and hostile inputs;
- missing, duplicate, late, and revised data;
- authorization and tenant boundaries;
- concurrency and retry behaviour;
- dependency failure and timeout;
- migration and rollback;
- compatibility with supported consumers.

Defect correction should normally include a failing regression test that becomes passing after the fix.

### 11.3 Verification record

Report:

- command or procedure;
- environment and relevant versions;
- data or fixtures used;
- result and timestamp;
- failures, exclusions, and limitations;
- link or identifier for retained evidence.

“No failures observed” is narrower and often more accurate than “verified correct.”

## 12. Debugging and incident analysis

Use this sequence:

1. State observed and expected behaviour.
2. Establish impact and timeline.
3. Preserve relevant evidence.
4. Create the smallest reproducible case.
5. Identify recent changes and dependency events.
6. Rank hypotheses by plausibility and diagnostic value.
7. Test one discriminating hypothesis at a time.
8. Mitigate impact without destroying evidence.
9. Correct the root cause.
10. Add regression detection and update runbooks.

For post-incident analysis, separate triggering event, contributing conditions, control failures, impact, recovery, and follow-up actions. Avoid attributing blame where system design and process improvements are the useful outcome.

## 13. Review method

### 13.1 Review categories

Review:

- correctness and completeness;
- readability and maintainability;
- architecture and dependency direction;
- interfaces and compatibility;
- security and privacy;
- data integrity and semantics;
- performance and capacity;
- reliability and recoverability;
- observability and operability;
- documentation and ownership.

### 13.2 Severity

- **Critical:** credible risk of severe security incident, irrecoverable data loss, substantial legal or safety impact, or system-wide outage.
- **High:** probable functional failure, serious data-integrity problem, exploitable weakness, or major operational risk.
- **Medium:** material maintainability, reliability, interoperability, or performance weakness.
- **Low:** bounded improvement with limited immediate consequence.

Severity reflects consequence and likelihood, not reviewer preference.

### 13.3 Finding template

```markdown
### [Severity] Concise finding title

- Affected component:
- Evidence:
- Consequence:
- Recommendation:
- Verification:
- Confidence: High | Medium | Low
```

Do not inflate a review with speculative findings. Put unresolved questions in a separate section.

## 14. Planning and delivery

### 14.1 Task template

```markdown
## TASK-NNN: Outcome-oriented title

- Purpose:
- Dependencies:
- Inputs:
- Deliverable:
- Acceptance criteria:
- Verification:
- Risks:
- Owner:
- Estimate or size:
```

Tasks should be independently reviewable where possible. Avoid tasks such as “build backend” that hide multiple interfaces and decisions.

### 14.2 Delivery slices

Prefer vertical slices that produce user-visible or operationally testable outcomes. Separate foundational work only when it reduces risk or enables several slices.

Use feature flags, parallel runs, canary release, shadow traffic, or phased migration where they reduce deployment risk. Each mechanism adds complexity and needs an owner and removal plan.

## 15. Migration and compatibility

A migration plan should define:

- current and target states;
- affected users, data, interfaces, and dependencies;
- compatibility window;
- schema and data conversion;
- validation and reconciliation;
- cutover and rollback criteria;
- dual-write or parallel-run risks;
- performance and capacity;
- communication and support;
- decommissioning and evidence retention.

Prefer expand-and-contract changes for live databases and APIs. Avoid irreversible destructive changes until new behaviour has been validated and rollback is no longer required.

## 16. Technology and standard evaluation

Evaluate options against weighted decision drivers. Include:

- functional and semantic fit;
- compatibility with existing architecture;
- maturity, maintenance, and release history;
- team capability and hiring or training burden;
- ecosystem, tooling, and interoperability;
- security and supply-chain model;
- deployment and support constraints;
- licensing and procurement;
- total cost of ownership;
- performance and scale evidence;
- portability, lock-in, and exit cost;
- expected system lifetime and stewardship.

Use a decision matrix to expose reasoning, not to manufacture objectivity. Explain the evidence and sensitivity of the result to weight changes. Prototype only the uncertain characteristics that could change the decision.

## 17. Documentation

Maintain a compact set of living artefacts appropriate to the project:

- project brief and scope;
- glossary and domain model;
- architecture views;
- ADRs;
- data contracts and schemas;
- API specifications;
- threat model and security decisions;
- test and acceptance strategy;
- runbooks;
- decision, risk, and change logs;
- release and migration records.

Store documentation close to the system of record, assign ownership, and review it when the corresponding system changes.

## 18. Release readiness

Use the following as a risk-based gate, not a ritual checklist.

### Product and scope

- Acceptance criteria are satisfied or exceptions are approved.
- Scope, user impact, and known limitations are documented.

### Engineering evidence

- Required static, unit, contract, integration, and operational tests have evidence.
- Material review findings are resolved or explicitly accepted.

### Data and migration

- Schemas, contracts, migrations, reconciliation, rollback, retention, and provenance are addressed.
- Backfills and corrections are controlled and auditable.

### Security and privacy

- Threats, access, secrets, dependencies, logging, retention, and residual risk are addressed.

### Operations

- Ownership, monitoring, alerting, runbooks, support, capacity, backup, restoration, and cost controls are ready.

### Compatibility and communication

- Consumers, deprecations, user communication, documentation, and support arrangements are ready.

Conclude:

- **Ready:** evidence supports release and no blocking risk remains.
- **Ready with conditions:** explicitly named conditions, owners, and deadlines remain.
- **Not ready:** blocking issues and required evidence are identified.

## 19. Reusable prompt patterns

### 19.1 Architecture

> Work in Architect mode. Review the notebook sources and `engineering-playbook.md`. Design a target architecture for this requirement. Identify evidence, assumptions, boundaries, data flows, trust boundaries, failure modes, and operational ownership. Compare the recommended approach with at least one credible alternative, including a simpler option where plausible. Provide a Mermaid diagram, proposed ADRs, risks, verification criteria, and ordered next actions.

### 19.2 Data pipeline

> Work in Specify and Architect modes. Design the pipeline from authoritative source to publication. Cover data contracts, validation, provenance, idempotency, restartability, late and revised data, schema and semantic evolution, quality monitoring, reconciliation, backfills, security, observability, ownership, retention, and cost. Separate confirmed requirements from proposed decisions.

### 19.3 Technical review

> Work in Review mode. Assess the supplied design or implementation for correctness, maintainability, architecture, interfaces, security, performance, reliability, data integrity, interoperability, and operability. Use only supported evidence. Classify confirmed findings by severity and provide consequence, correction, and verification. Separate findings, questions, assumptions, and optional improvements.

### 19.4 Implementation plan

> Work in Plan mode. Convert the accepted architecture into small, ordered, independently verifiable tasks. Include dependencies, deliverables, acceptance criteria, test evidence, migrations, documentation, release, and operational readiness. Identify the critical path, blocking decisions, and work that can proceed in parallel.

### 19.5 Uncertainty challenge

> Work in Explore mode using doubt-driven analysis. Identify the assumptions most capable of invalidating this proposal, evidence for and against them, plausible failure modes, and the cheapest discriminating tests. Recommend whether to proceed, modify the approach, run a time-boxed spike, or stop.

### 19.6 Release assessment

> Work in Ship mode. Assess the release evidence against the relevant sections of `engineering-playbook.md`. Conclude ready, ready with conditions, or not ready. List blocking issues, accepted residual risks, owners, deadlines, rollback criteria, and missing evidence.

## 20. Maintenance of this playbook

Treat this document as a versioned engineering product.

- Use semantic versioning for intentional changes.
- Record significant changes in Git history or a changelog.
- Review after major incidents, technology shifts, or recurring review findings.
- Remove guidance that is not used or cannot be maintained.
- Keep project-specific rules out of this generic playbook.
- Test changes with representative architecture, pipeline, review, and planning prompts.

A longer playbook is useful only if relevant sections are discoverable, current, and consistently applied.
