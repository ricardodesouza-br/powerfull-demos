---
title: Power Platform Best Practices
document_type: BestPractices
document_role: BestPractices
domain: LowCode
product_family: Microsoft Power Platform

owner: Low Code Team
version: 1.0
status: Approved
review_date: 2027-06-15

audience:
  - Solution Architect
  - Developer
  - Maker
  - Platform Administrator

tags:
  - architecture
  - development
  - performance
  - security
  - alm
  - monitoring

related_documents:
 - docs/power-platform/pp-reference-catalog-components.md
 - docs/power-platform/pp-solution-patterns-catalog.md
 - docs/power-platform/pp-procedures-component-selection.md
 - docs/power-platform/pp-procedures-architectural-discovery-blueprint.md

---

<!-- markdownlint-disable MD024 MD025 -->

# Power Platform Best Practices

## Purpose

This document consolidates recommended practices for designing, developing, securing, deploying, and operating Power Platform solutions.

The guidance applies to:

- Power Apps
- Power Automate
- Dataverse
- Power Pages
- Copilot Studio

## Architecture & Solution Design Principles

### Maintain Architecture Accountability

#### Recommendation

Treat AI-assisted architecture outputs as drafts that require review and approval by a qualified solution architect.

#### Practices

- Validate assumptions against stakeholder evidence.
- Assess architectural trade-offs before making recommendations.
- Confirm constraints, dependencies, and decision drivers.
- Obtain the appropriate human review before using recommendations for delivery or implementation.

#### Avoid

- Treating generated content as an approved architecture.
- Delegating architectural accountability to an AI system.

#### Why This Matters

Human accountability ensures that architectural recommendations reflect actual business, technical, security, and governance constraints.

### Apply Guidance Proportionally

#### Recommendation

Scale the depth of discovery, documentation, validation, and review to the workload's complexity, risk, business impact, data sensitivity, user scale, integration criticality, and regulatory or financial exposure.

#### Practices

- Use concise blueprints for low-risk and low-complexity workloads.
- Apply deeper analysis and stronger validation to business-critical or highly integrated workloads.
- Document the factors that drove the level of architectural rigor.
- Treat applicable organizational policies and approval requirements as authoritative regardless of blueprint size.

#### Avoid

- Applying the same documentation depth to every workload without considering risk.
- Omitting mandatory governance or security controls because a workload appears small.

#### Why This Matters

Proportionate guidance focuses effort where architectural failure would have the greatest impact without creating unnecessary process overhead.

### Capture Architectural Decisions Clearly

#### Recommendation

Document significant architectural decisions with their context, alternatives, rationale, trade-offs, constraints, and required validation.

#### Practices

- State the decision and the requirement or constraint that drove it.
- Record alternatives considered and why the selected approach was preferred.
- Identify affected Well-Architected pillars, assumptions, trade-offs, and dependencies.
- Link decisions to relevant component catalogs, solution patterns, and organizational guidance.

#### Avoid

- Recording conclusions without rationale or alternatives.
- Creating an architecture decision record repository when the governing knowledge-base model does not define one.

#### Why This Matters

Decision context makes architecture reviewable, maintainable, and easier to revisit when requirements or constraints change.

### Manage Architecture Assumptions and Risks

#### Recommendation

Make uncertainty visible and progressively refine assumptions as evidence becomes available.

#### Practices

- Distinguish confirmed facts, assumptions, risks, recommendations, and open questions.
- Ask targeted questions before proceeding when missing information could materially affect the design.
- Record the potential impact if an assumption proves false.
- Revisit unresolved assumptions during blueprint validation and architecture review.

#### Avoid

- Inventing business constraints, licensing conditions, security requirements, data classifications, or integration behavior.
- Hiding unresolved questions in apparently definitive architecture statements.

#### Why This Matters

Explicit uncertainty prevents premature commitment and helps stakeholders prioritize the validation work required to make an architecture reliable.

### Design for Reliability

#### Recommendation

Architect applications and automations to tolerate failures and minimize downtime.

#### Practices

- Prefer asynchronous designs for long-running processes.
- Implement retry policies for transient failures.
- Implement error handling in flows.
- Separate environments into Dev, Test, and Production.

#### Why This Matters

Reliable solutions reduce operational risk and improve user experience.

### Keep Solutions Simple and Modular

#### Recommendation

Design applications and automations as modular components.

#### Practices

- Break large solutions into smaller components.
- Split complex flows into multiple focused flows.
- Separate unrelated responsibilities.
- Prefer configuration over custom implementation where possible.

#### Why This Matters

Modular solutions are easier to:

- Maintain
- Test
- Scale
- Reuse

### Use the Right Tool for the Job

#### Recommendation

Select the Power Platform component best suited to the workload.

#### Practices

- Use Canvas Apps for interactive user experiences.
- Use Model-Driven Apps for complex processes.
- Use Power Automate for automation workflows.
- Use Dataverse for relational business data.
- Use Power Pages for external-facing solutions.
- Use Copilot Studio for AI agents and AI based automations.
- Use Code Apps for complex enterprise-grade requirements requiring advanced engineering control (source control, CI/CD).
- Use Power Pages for any public-facing or external-facing website requirements.
- Use Agent Flows for deterministic automation within a Copilot Studio agent experience.
- Use Computer Use only for agent-driven UI automation when no stable API or connector exists.
- Use Dataverse as the default relational store; use Virtual Tables for external data without duplication; use Dataflows for scheduled ETL.

#### Avoid

- Using Canvas Apps as background processors.
- Using flows as user interfaces.
- Using spreadsheets as enterprise databases.
- Using Computer Use for standard automation where an API or connector is available.

#### Why This Matters

Incorrect technology choices frequently become scalability bottlenecks. Proper selection ensures the platform remains maintainable and performant.

### Design for User Experience

#### Recommendation

Optimize solutions to maximize usability and adoption.

#### Practices

- Follow UI/UX best practices.
- Provide intuitive navigation.
- Ensure accessibility compliance.
- Optimize page and app load times.

#### Why This Matters

Adoption depends heavily on usability.

## Development Best Practices

### Apply Naming Standards

#### Recommendation

Use consistent naming conventions for all solution components.

#### Practices

- Use publisher prefixes.
- Use descriptive names.
- Apply consistent naming standards across environments.

#### Why This Matters

Consistent naming improves maintainability and supportability.

### Implement Source Control and ALM

#### Recommendation

Manage implementation artifacts using source control and repeatable deployment processes.

#### Practices

- Use Git repositories when team development is required.
- Store solution source in source control.
- Treat managed solutions as deployment artifacts.
- Implement repeatable deployment processes.

#### Why This Matters

Source control improves traceability, collaboration, and recovery.

### Build Defensive Solutions

#### Recommendation

Design applications and flows to handle failures gracefully.

#### Practices

- Validate inputs.
- Use error-handling patterns.
- Test failure scenarios.
- Use try-catch-finally flow patterns.

#### Why This Matters

Defensive design reduces production incidents.

### Reuse Before Rebuilding

#### Recommendation

Prefer reusable assets over duplicated implementations.

#### Practices

- Use Component Libraries.
- Use Child Flows.
- Create reusable templates.
- Centralize common logic.

#### Why This Matters

Reuse reduces maintenance effort and improves consistency.

### Maintain Documentation

#### Recommendation

Document solution architecture, business logic, and operational considerations.

#### Practices

- Comment complex logic.
- Create architecture diagrams.
- Document data flows.
- Maintain solution overviews.

#### Why This Matters

Documentation accelerates support, troubleshooting, and onboarding.

### Author Solution Blueprints Consistently

#### Recommendation

Use a consistent Solution Blueprint structure that communicates the architecture without turning the document into a detailed implementation specification.

#### Practices

- Cover the solution overview, components, data and integrations, security, ALM, licensing, decisions, governance dependencies, assumptions, risks, and diagrams.
- Use official product names and describe how major components interact.
- Include architecture diagrams that accurately represent users, applications, flows, data sources, and integrations.
- Reference organizational policies and owners instead of redefining those policies in the blueprint.
- Keep the depth of each section proportional to workload complexity and risk.

#### Avoid

- Omitting licensing, capacity, governance, or operational dependencies from architecture documentation.
- Including detailed Power Fx formulas, flow logic, plug-in designs, table schemas, backlog tasks, or operational recovery instructions unless they are necessary to explain a major architectural decision.

#### Why This Matters

Consistent blueprints make architectural intent understandable to human reviewers and AI-assisted workflows while preserving the boundary between architecture and implementation planning.

## Performance & Scalability

### Use Delegable Operations

#### Recommendation

Use delegable functions whenever processing large datasets.

#### Practices

- Prefer source-side filtering.
- Use supported delegable functions.
- Minimize client-side processing.

#### Why This Matters

Delegation improves both performance and scalability.

### Minimize Startup Processing

#### Recommendation

Load only the information necessary for the initial user interaction.

#### Practices

- Use lazy loading.
- Load data on demand.
- Defer non-critical operations.

#### Why This Matters

Reducing startup work improves user experience.

### Optimize Data Retrieval

#### Recommendation

Retrieve only the records and fields required.

#### Practices

- Filter at the source.
- Limit result sets.
- Paginate large datasets.
- Retrieve only required columns.

#### Why This Matters

Smaller payloads improve responsiveness.

### Use Parallelism Carefully

#### Recommendation

Use concurrency only when operations are independent.

#### Practices

- Validate for race conditions.
- Avoid conflicting updates.
- Measure actual performance improvements.

#### Why This Matters

Improper concurrency can introduce instability.

### Test at Production Scale

#### Recommendation

Validate solution performance using realistic datasets and workloads.

#### Practices

- Simulate production volume.
- Test concurrent users.
- Monitor bottlenecks.

#### Why This Matters

Issues often appear only at production scale.

## Security & Compliance Best Practices

### Apply Least Privilege Access

#### Recommendation

Grant only the permissions required for business responsibilities.

#### Practices

- Use role-based access control.
- Limit record visibility.
- Review permissions periodically.

#### Why This Matters

Reducing privileges lowers security risk.

### Separate Sensitive Workloads

#### Recommendation

Use dedicated environments for sensitive or regulated workloads.

#### Practices

- Apply environment-level controls.
- Use security groups.
- Define ownership clearly.

#### Why This Matters

Environment isolation reduces exposure risk.

### Govern Data Movement

#### Recommendation

Implement Data Loss Prevention (DLP) policies.

#### Practices

- Review connector usage.
- Restrict unsafe connector combinations.
- Regularly review policy effectiveness.

#### Why This Matters

DLP policies reduce accidental data leakage.

### Secure DevOps Operations

#### Recommendation

Protect deployment pipelines and service identities.

#### Practices

- Use service principals.
- Store secrets securely.
- Avoid hardcoded credentials.
- Review privileged access regularly.

#### Why This Matters

Deployment pipelines are critical security assets.

## ALM & DevOps Practices

### Build Inside Solutions

#### Recommendation

Create solution-aware assets inside Solutions.

#### Practices

- Apps inside Solutions.
- Flows inside Solutions.
- Security roles inside Solutions.
- Tables inside Solutions.

#### Why This Matters

Solutions support deployment and lifecycle management.

### Automate Deployment

#### Recommendation

Use automated deployment mechanisms whenever possible.

#### Practices

- Implement CI/CD.
- Automate validation checks.
- Automate deployment approvals.

#### Why This Matters

Automation reduces deployment risk and improves consistency.

### Run Quality Gates

#### Recommendation

Validate solutions before deployment.

#### Practices

- Run Solution Checker.
- Perform peer reviews.
- Validate security requirements.

#### Why This Matters

Quality gates reduce production defects.

### Use Environment Configuration

#### Recommendation

Separate implementation from configuration.

#### Practices

- Use connection references.
- Use environment variables.
- Avoid hardcoded values.

#### Why This Matters

Configuration portability improves deployment reliability.

## Monitoring & Maintenance

### Implement Monitoring

#### Recommendation

Monitor critical applications, automations, and environments.

#### Practices

- Configure alerts.
- Monitor failures.
- Review telemetry regularly.

#### Why This Matters

Monitoring enables proactive operations.

### Perform Periodic Reviews

#### Recommendation

Review solutions regularly for performance, security, and maintainability.

#### Practices

- Conduct architecture reviews.
- Analyze usage patterns.
- Review operational metrics.

#### Why This Matters

Solutions naturally drift from original design assumptions.

### Prepare for Recovery

#### Recommendation

Maintain backup and recovery procedures.

#### Practices

- Validate backups.
- Document recovery procedures.
- Test restoration processes.

#### Why This Matters

Recovery planning reduces business disruption.

### Stay Current

#### Recommendation

Monitor platform changes and roadmap updates.

#### Practices

- Review release plans.
- Monitor deprecations.
- Assess impact before adopting changes.

#### Why This Matters

Platform evolution can affect existing solutions.

## Governance Best Practices

### Use PPAC as the Primary Governance Experience

#### Recommendation

Use the Power Platform Admin Center as the primary experience for governance, inventory, monitoring, security, and administrative actions.

#### Practices

- Prefer native capabilities such as Inventory, Usage, Monitor, Actions, Managed Environments, environment groups, rules, delegated administration, and environment routing.
- Use APIs, CLI, connectors, or automation when scale or integration requires them.
- Use the CoE Starter Kit or custom governance solutions only for documented capability gaps, with an owner, support model, and retirement criterion.

#### Avoid

- Replacing native PPAC capabilities with custom reporting without documenting the capability gap.
- Treating a custom governance solution as authoritative when PPAC data is more current.

#### Why This Matters

A PPAC-first model reduces duplicated governance tooling and keeps administrative decisions aligned with the platform's supported control plane.

### Govern Environments by Purpose and Lifecycle

#### Recommendation

Assign every non-default environment a documented purpose, owner, lifecycle stage, region, security group, and retirement path.

#### Practices

- Separate development, test/UAT, production, sandbox, and default-environment purposes.
- Use security groups and environment roles to restrict maker and administrator access.
- Use Managed Environments, environment groups, rules, and routing where consistent controls are required at scale.
- Review inactive, duplicate, ownerless, or expired environments and retire, archive, or consolidate them.

#### Avoid

- Hosting business-critical or regulated workloads in personal, trial, or default environments.
- Creating environments without region, capacity, data-residency, ownership, and lifecycle review.

#### Why This Matters

Purpose-driven environments reduce sprawl, improve access control, and create a predictable path from development to production.

### Govern Connectors and Data Movement

#### Recommendation

Use data policies and connector classification to control data movement, increasing review requirements for custom connectors, HTTP actions, and external endpoints.

#### Practices

- Classify connectors as Business, Non-Business, or Blocked according to trust and data-movement risk.
- Apply tenant-wide baseline policies and stricter environment-level policies for sensitive workloads.
- Review authentication, endpoint, data sensitivity, ownership, support, and monitoring for custom connectors and HTTP actions.
- Make connector exceptions scoped, approved, time-bound, and subject to renewal review.

#### Avoid

- Allowing new connectors into sensitive environments without review.
- Treating endpoint filtering or advanced connector policies as a replacement for solution and security review.

#### Why This Matters

Connector governance reduces accidental data exfiltration while preserving a documented path for legitimate integrations.

### Govern AI Agents and Publishing

#### Recommendation

Apply additional governance to Copilot Studio agents, especially those using sensitive knowledge, external systems, autonomous actions, or broad publishing channels.

#### Practices

- Require business and technical owners, an approved environment, intended audience, support path, and monitoring plan for production agents.
- Review knowledge-source permissions, connectors, actions, HTTP endpoints, authentication, triggers, and publishing channels.
- Apply human checkpoints to sensitive or low-confidence actions and use audit logging where required.
- Review responsible-AI, DLP, security, and external-sharing implications before publication.

#### Avoid

- Publishing agents broadly without documented approval.
- Connecting agents to overshared knowledge sources or high-risk actions without access and impact review.

#### Why This Matters

Agent behavior and knowledge access can expand data exposure and operational impact beyond traditional app and flow boundaries.

### Maintain Inventory, Ownership, and Criticality

#### Recommendation

Use platform inventory to maintain accountability and continuity for apps, flows, agents, and environments.

#### Practices

- Assign business and technical owners to production-grade assets.
- Identify ownerless, departed-user, inactive, broadly shared, and high-usage assets.
- Classify assets as Personal Productivity, Departmental, Business-Critical, or Regulated.
- Recertify purpose, audience, environment, connectors, data sensitivity, support path, and retirement status.

#### Avoid

- Treating inventory as passive reporting without action owners.
- Allowing a critical workload to depend on a single individual account.

#### Why This Matters

Ownership and criticality information determines the level of support, monitoring, ALM, recovery, and security investment required.

### Govern Licensing, Capacity, and Exceptions

#### Recommendation

Treat licensing, capacity, and governance exceptions as design-time and operational controls that require accountable review.

#### Practices

- Review premium connectors, Dataverse database/file/log capacity, API limits, pay-as-you-go usage, and capacity add-ons.
- Link license requests to workload type, users, connectors, expected volume, criticality, and support model.
- Require exception records with justification, scope, risk, compensating controls, owners, approvers, expiration, and review cadence.
- Validate current licensing terms against the internal licensing guides before procurement or production rollout.

#### Avoid

- Treating summary licensing tables as commercial authority.
- Allowing open-ended exceptions or renewing them without updated justification.

#### Why This Matters

Early cost and exception governance prevents budget surprises, policy bypasses, and unsupported production workloads.

## Change Log

- **2026-08-27**:

- Added architecture accountability, proportionate guidance, decision documentation, assumption management, and Solution Blueprint authoring practices.

### Version 1.0.0

Initial release.
