---
title: Power Platform Architectural Component Selection Procedure
document_type: Procedures
document_role: Component Selection
domain: LowCode
product_family: Microsoft Power Platform

owner: Low Code Team
version: 1.0.0
status: Approved
review_date: 2027-06-15

audience:
  - Solution Architect
  - Developer
  - Platform Administrator

tags:
  - architecture
  - procedures
  - governance
  - selection

related_documents:
  - docs/power-platform/pp-reference-catalog-components.md
  - docs/power-platform/pp-solution-patterns-catalog.md

---

# Power Platform Architectural Component Selection Procedure

## Purpose

This procedure defines the standard method for identifying, selecting, and validating the appropriate Power Platform components for any new solution. It ensures that architectural decisions are based on consistent criteria, minimizing technical debt and ensuring compliance with corporate standards.

## Prerequisites

- **Author Identity:** Requires active architect or lead developer involvement.
- **Requirement Definition:** A clear understanding of the business problem and desired outcome.
- **Access:** Access to the Power Platform component reference catalog and design guidelines.

## Step-by-Step Procedure

### Architectural Component Selection

#### Description

Follow this sequential workflow to identify the correct technology stack for a required business application or automation.

#### Prerequisites

- Access to the **Power Platform Component Reference Catalog**.
- Identification of the intended audience (internal, external, etc.).

#### Execution Steps

1. **Define the Audience:** Identify who will use the application (e.g., internal employees, public users, administrative staff, or automated agents).
2. **Define the Interaction Model:** Determine the primary interaction type (e.g., custom application interface, structured business application, external portal, background workflow, RPA, or conversational agent).
3. **Define the Data Pattern:** Identify the data source and relationship requirements (e.g., simple list data, relational enterprise data, external system of record, real-time virtualized data, or document-based data).
4. **Define the Automation Pattern:** Determine the execution frequency and trigger type (e.g., event-driven, scheduled, instant, human-in-the-loop, attended RPA, or unattended RPA).
5. **Validate Cross-Cutting Constraints:** Ensure the solution meets requirements for licensing, security, Data Loss Prevention (DLP), Application Lifecycle Management (ALM), monitoring, and Responsible AI (if applicable).
6. **Evaluate Pro-Code Fit:** If the solution requires a fully bespoke user experience, advanced frontend frameworks, or software engineering control, evaluate **Code Apps** before opting for Canvas/Model-Driven Apps.
7. **Evaluate UI Automation Fit:** If a task requires interacting with a web or desktop interface and no API/connector exists, compare **Desktop Flows** and **Computer Use** to determine the appropriate balance of determinism and adaptability.

#### Expected Results

- A validated technology stack selection.
- A documented architectural design for the identified components.
- A preliminary licensing and security review for the selected components.

#### Validation & Quality Gates

- **Constraint Checklist:** Verification that all cross-cutting constraints (Security, DLP, etc.) are met.
- **Licensing Review:** Initial check against the official licensing guide (Design-time indicators only).
- **Authority Approval:** Formal sign-off from the Architecture review board or the designated Product Owner.

## Troubleshooting and Error Handling

### Common Issues

- **Ambiguous Requirement:** The business requirement is too broad to select a specific component.
  - *Action:* Schedule a requirements discovery session with the business owner before proceeding.
- **Missing Licensed/Access:** Required component is not available in the target environment.
  - *Action:* Contact Platform Administration to request environment updates or alternative component suggestions.
- **Conflicting Constraints:** A required-functionality conflicts with a security or DLP constraint.
  - *Action:* Escalate to the Security and Governance team for a formal risk assessment and waiver review.

## Change Log

- **2026-08-27**:

Initial Draft

```added_only
```
