---
title: Power Platform Governance Procedures
document_type: Procedures
document_role: Governance & Constraints
domain: LowCode
product_family: Microsoft Power Platform
owner: Low Code Team
version: 1.0.0
status: Approved
review_date: 2027-06-15
audience:
  - Platform Administrator
  - Solution Architect
  - Environment Administrator
  - Security and Compliance Team
tags:
  - governance
  - procedures
  - compliance
  - environments
  - security
related_documents:
  - pp-best-practices-catalog.md
  - pp-reference-catalog-governance.md
  - pp-reference-catalog-components.md
---

<!-- markdownlint-disable MD024 MD025 -->

# Power Platform Governance Procedures

## Purpose

This document provides repeatable procedures for reviewing, approving, operating, and recertifying Power Platform governance controls. Apply the procedures proportionally to workload criticality, data sensitivity, user scale, integration risk, and regulatory exposure.

## Prerequisites

- Access to the Power Platform Admin Center and the applicable environment or tenant settings.
- Named business and technical owners for the workload under review.
- The applicable governance reference entries, solution documentation, inventory data, and licensing guidance.
- Participation from platform, security/compliance, business, and environment administrators when the workload risk requires it.

## Step-by-Step Procedure

### Governance Validation Review

#### Description

Use this procedure for production-readiness reviews, recurring governance checks, and workload recertification.

#### Execution Steps

1. Confirm the environment purpose, lifecycle, region, security group, business owner, and technical owner.
2. Confirm the workload criticality tier, data sensitivity, intended audience, and support model.
3. Review data policies, connector classifications, custom connectors, HTTP actions, and external knowledge sources.
4. Review identity, least privilege, Conditional Access, audit logging, monitoring, and escalation controls.
5. Review ALM evidence: managed solutions, pipeline or release process, version, approvals, backup, and rollback plan.
6. Review inventory status, sharing scope, usage, ownership, capacity, premium licensing, and known exceptions.
7. Record each unchecked control as a remediation action, approved risk acceptance, or time-bound exception.
8. Obtain the required business, platform, and security approvals and store the review evidence with the workload record.

#### Expected Results

- A completed governance review with evidence and named action owners.
- A documented decision to approve, remediate, accept risk, or block the workload.

#### Validation & Quality Gates

- No business-critical or regulated workload operates without owners, support, monitoring, and an approved environment.
- Exceptions have scope, justification, compensating controls, approvers, expiration, and review cadence.

### Environment Request and Approval

#### Description

Use this procedure before creating a non-default environment for development, testing, sandbox use, or production hosting.

#### Execution Steps

1. Capture the business purpose, workload, requested environment type, region, data sensitivity, expected users, and lifecycle stage.
2. Identify business and technical owners, support expectations, security group membership, and expected capacity.
3. Select the required data policies, Managed Environment settings, environment group, routing behavior, and ALM path.
4. Review licensing, capacity, data residency, security, and compliance implications.
5. Obtain platform approval and security/compliance approval when required by the risk tier.
6. Create the environment with the approved name, region, security group, policies, owners, and lifecycle metadata.
7. Record the environment in inventory and communicate its purpose and maker guidance.

#### Expected Results

- An environment created only for an approved purpose with documented owners, controls, and retirement criteria.

### Environment Lifecycle and Retirement

#### Description

Use this procedure to review inactive, duplicate, ownerless, expired, or obsolete environments and to retire them safely.

#### Execution Steps

1. Identify candidate environments from inventory, usage, ownership, capacity, and lifecycle metadata.
2. Confirm whether active applications, flows, agents, integrations, or data remain in the environment.
3. Notify owners and business stakeholders and define a retention or migration period where required.
4. Export or back up required solutions and data according to the workload’s recovery requirements.
5. Migrate supported workloads to the approved destination or document an approved exception.
6. Remove access and retire, archive, reset, or delete the environment using the approved administrative process.
7. Update inventory, ownership records, capacity reporting, and related documentation.

#### Validation & Quality Gates

- No environment is deleted without an owner review, dependency check, and documented retention decision.

### DLP and Connector Review

#### Description

Use this procedure before enabling a new connector or changing a data policy in a production or sensitive environment.

#### Execution Steps

1. Classify the connector as Business, Non-Business, or Blocked based on trust and data-movement risk.
2. Review the connector’s data sources, authentication, endpoint, data sensitivity, and business owner.
3. Assess whether the connector can mix with existing connectors under the applicable policy scope.
4. For custom connectors or HTTP actions, review API ownership, authentication, endpoint filtering, support, and monitoring.
5. Assess design-time and runtime impact on existing apps and flows before changing policy.
6. Approve, restrict, block, or time-limit the request and record the decision.
7. Review exceptions before expiration and remove them when the requirement ends.

#### Expected Results

- A traceable connector or policy decision with classification, scope, owner, rationale, and review date.

### Production Readiness and Agent Approval

#### Description

Use this combined gate before publishing a production application, flow, or Copilot Studio agent.

#### Execution Steps

1. Confirm the production environment, business and technical owners, criticality tier, audience, and support path.
2. Verify managed solution deployment, testing evidence, release version, approval, backup, rollback, and monitoring.
3. For agents, review knowledge sources, connectors, actions, HTTP endpoints, triggers, authentication, publishing channels, and human checkpoints.
4. Review security, DLP, audit logging, responsible-AI controls, and external-sharing implications.
5. Confirm capacity, licensing, request limits, and operational thresholds.
6. Approve publication, require remediation, or record a time-bound exception.
7. Record the production decision and communicate operational ownership.

#### Validation & Quality Gates

- Broad, external, autonomous, or high-impact agent publishing requires documented approval.
- Sensitive knowledge sources are reviewed for access scope and oversharing risk.

### Ownership and Inventory Recertification

#### Description

Use this procedure to maintain discoverability, continuity, and accountability for apps, flows, agents, and environments.

#### Execution Steps

1. Use PPAC Inventory as the starting point for the asset review.
2. Identify ownerless assets, departed-user ownership, inactive makers, broad sharing, high usage, and criticality mismatches.
3. Confirm business owner, technical owner, purpose, audience, environment, connectors, data sensitivity, support path, and retirement status.
4. Transfer ownership or assign accountable owners using the approved administrative process.
5. Reclassify criticality and update monitoring, ALM, backup, licensing, and support requirements.
6. Promote production-grade assets out of the default environment when appropriate.
7. Record unresolved issues as actions or time-bound exceptions and schedule follow-up.

### Licensing and Capacity Review

#### Description

Use this procedure to review premium usage, capacity pressure, API limits, pay-as-you-go consumption, and license requests.

#### Execution Steps

1. Identify the apps, flows, agents, environments, connectors, Dataverse capacity, and business units driving consumption.
2. Compare current and forecast usage with available licenses, capacity, request limits, and budget thresholds.
3. Confirm the workload owner, criticality, expected volume, connector requirements, and support model.
4. Validate the current internal Power Platform and Copilot Studio licensing guides.
5. Optimize, consolidate, archive, purchase capacity, or approve the appropriate license based on evidence.
6. Record cost owner, cost center, threshold, decision, and recurring review date.

#### Expected Results

- A documented capacity and licensing decision based on current internal guidance, not stale source-table assumptions.

### Exception Management

#### Description

Use this procedure when a valid business requirement cannot meet the standard governance baseline.

#### Execution Steps

1. Submit an exception record containing ID, affected control, business justification, scope, duration, risk, compensating controls, owners, and approvers.
2. Platform validates technical alternatives, PPAC capabilities, expected operational impact, and removal options.
3. Security and compliance review data sensitivity, exposure, logging, monitoring, and regulatory impact.
4. The business owner accepts residual risk and confirms accountability.
5. The designated approver grants, rejects, or requests changes.
6. Monitor the exception and review it before expiration.
7. Remove, renew with updated justification, or convert the exception into a standard governed pattern.

#### Validation & Quality Gates

- No exception remains active after expiration without formal renewal.
- Repeated exceptions trigger review of the baseline control or solution design.

## Troubleshooting and Error Handling

### Common Issues

- **Incomplete ownership:** Pause approval and assign business and technical owners.
- **Policy conflict:** Review alternative connectors, environment scope, or compensating controls with platform and security teams.
- **Missing licensing or capacity:** Do not approve production use until current entitlement and capacity are validated.
- **Unresolved high-risk finding:** Remediate, obtain a documented risk acceptance, or block the workload.

## Change Log

- **2026-08-27**: Initial Draft
