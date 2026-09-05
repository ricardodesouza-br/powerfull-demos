---
title: Power Platform Governance Reference Catalog
document_type: ReferenceCatalogs
domain: LowCode
product_family: Microsoft Power Platform
owner: Low Code Team
version: 1.0.0
status: Approved
review_date: 2027-06-15
audience:
  - Solution Architect
  - Platform Administrator
  - Security and Compliance Team
  - Environment Administrator
tags:
  - governance
  - security
  - compliance
  - environments
  - connectors
  - ownership
related_documents:
  - pp-best-practices-catalog.md
  - pp-procedures-governance.md
  - pp-reference-catalog-components.md
---

<!-- markdownlint-disable MD025 -->

# Power Platform Governance Reference Catalog

## Purpose

This catalog defines the governance terms, classifications, roles, decision points, and naming patterns used to manage Power Platform at enterprise scale. It complements the component reference catalog: this document describes how the platform is governed, while the component catalog describes what the components do.

## Governance Roles Catalog

| Role | Primary Responsibilities |
| --- | --- |
| Platform Team | Defines tenant-wide policies, manages Power Platform Admin Center settings, owns environment strategy, and monitors platform risk. |
| Environment Administrator | Manages assigned environments, security groups, makers, capacity, and operational controls within approved boundaries. |
| Maker | Builds within guardrails, follows naming and ALM practices, documents ownership, and requests exceptions when required. |
| Business Owner | Owns business value, criticality, user adoption, compliance impact, and continuity of production assets. |
| Security and Compliance Team | Reviews sensitive scenarios, validates data-protection controls, and approves exceptions for regulated workloads. |

## Connector Classification Catalog

| Classification | Meaning | Typical Treatment |
| --- | --- | --- |
| Business | Trusted connectors approved for organizational data. | May be used within the approved business trust boundary. |
| Non-Business | Connectors not approved for business-data mixing or carrying elevated data-movement risk. | Do not combine with Business connectors in the same app or flow. |
| Blocked | Connectors prohibited by policy. | Prevent use in the applicable tenant or environment scope. |

Apply tenant-wide baseline policies first, then stricter environment or environment-group policies where workload sensitivity requires them. Review new connectors before allowing them in sensitive environments.

## Environment Type Catalog

| Environment Type | Purpose | Governance Expectation |
| --- | --- | --- |
| Development | Build and unit-test applications, flows, and solutions. | Restricted maker group; unmanaged development artifacts allowed. |
| Test / UAT | Integration testing and user acceptance. | QA and selected business users; representative test data. |
| Production | Live workloads for end users. | Admin-managed access; managed solutions and approved release process. |
| Sandbox / Trial | Prototyping and experimentation. | DLP guardrails, limited support expectation, and lifecycle review. |
| Default | Personal productivity and low-risk experimentation. | Not a production hosting location; review high-usage or broadly shared assets. |

## Managed Environment Feature Catalog

| Feature | Governance Use |
| --- | --- |
| Usage insights and weekly digest | Identify adoption, high-use assets, makers, and emerging governance issues. |
| Sharing limits | Restrict broad application sharing without review. |
| Solution checker enforcement | Apply quality and performance analysis before solution import where supported. |
| Environment groups and rules | Apply consistent controls to related environments. |
| Environment routing | Direct maker-created work toward governed personal developer environments. |
| Maker welcome messages | Explain environment purpose, safe usage, and escalation paths. |

Validate licensing and entitlement requirements before enabling Managed Environments broadly.

## Criticality Tier Catalog

| Tier | Typical Use | Minimum Governance Expectations |
| --- | --- | --- |
| Personal Productivity | Individual productivity or experimentation. | Default-environment guardrails and limited connectors. |
| Departmental | Team or department process support. | Named owners, appropriate environment, and periodic review. |
| Business-Critical | Operationally important process used by many users. | Business and technical owners, ALM, monitoring, backup, and support model. |
| Regulated | Sensitive, compliance-bound, or externally exposed workload. | Security review, strict data policies, audit logging, access review, and exception control. |

## Cost Governance Decision Catalog

| Decision Area | Review Question | Governance Action |
| --- | --- | --- |
| Premium connectors | Does the solution require premium or custom connectors? | Validate licensing impact before production approval. |
| Dataverse capacity | Is database, file, or log growth approaching its threshold? | Clean up, archive, consolidate, or request capacity. |
| API and flow limits | Are flows repeatedly reaching request or action limits? | Optimize the design or select the appropriate license. |
| Pay-as-you-go | Is consumption variable or difficult to forecast? | Require a budget owner, threshold, and recurring review. |

Licensing and capacity entries are design-time indicators only. Validate current terms against the internal [Power Platform Licensing Guide](../../Power-Platform-Licensing-Guide-August-2026.pdf) and [Microsoft Copilot Studio Licensing Guide](../../Microsoft-Copilot-Studio-Licensing-Guide-August.pdf) before procurement, deployment, or production rollout.

## Advanced Protection Control Catalog

| Control | Use When | Required Governance |
| --- | --- | --- |
| Tenant isolation | Cross-tenant connector access must be restricted or explicitly approved. | Maintain allow lists and review cross-tenant connection reports. |
| Guest and B2B governance | External users access environments, apps, data, or knowledge sources. | Coordinate with Microsoft Entra access reviews and Conditional Access. |
| Customer-managed key | Regulated workloads require customer control of Dataverse encryption keys. | Define key ownership, rotation, revocation, and recovery procedures. |
| Customer Lockbox | Microsoft support access to customer data requires customer approval. | Define approvers, response expectations, and audit review. |

## Naming Convention Catalog

| Asset Type | Pattern | Example |
| --- | --- | --- |
| Environment | `PP-[BU/Function]-[Workload]-[Region]-[Lifecycle]` | `PP-FIN-ExpenseMgmt-BR-DEV` |
| Data policy | `DLP-[Scope]-[Sensitivity]-[Purpose]` | `DLP-Prod-Restricted-Finance` |
| Security group | `SG-PP-[Environment]-[Role]` | `SG-PP-FIN-ExpenseMgmt-PROD-Admins` |
| Solution | `[Domain].[Capability].[SolutionType]` | `Finance.ExpenseApproval.CanvasApp` |
| Pipeline | `PIPE-[Workload]-[Stages]` | `PIPE-ExpenseMgmt-DEV-TEST-PROD` |
| Agent | `AGT-[Domain]-[Purpose]-[Audience]-[Lifecycle]` | `AGT-IT-Helpdesk-Internal-UAT` |
| Exception | `EXC-[Control]-[Workload]-[ExpirationYYYYMM]` | `EXC-DLP-ExpenseMgmt-202612` |

Use stable business terms, consistent lifecycle values, and region identifiers where data residency or support ownership matters. Avoid personal names in asset names; store ownership in metadata and inventory.

## Exception Record Catalog

| Field | Required Content |
| --- | --- |
| Exception ID | Control, workload, and expiration using the approved naming pattern. |
| Control or policy | Affected data policy, connector, environment, security, licensing, or monitoring control. |
| Business justification | Why the baseline cannot be followed and what outcome depends on the exception. |
| Scope and duration | Environments, assets, connectors, users, start date, expiration, and review cadence. |
| Risk and compensating controls | Data sensitivity, exposure, monitoring, access restriction, logging, approval gates, and rollback. |
| Owners and approvers | Business, technical, platform, security/compliance, and renewal owners. |

## Change Log

- **2026-08-27**: Initial Draft
