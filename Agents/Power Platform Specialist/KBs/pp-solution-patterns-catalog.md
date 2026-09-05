---
title: Power Platform Solution Patterns
document_type: SolutionPatterns
domain: LowCode
product_family: Microsoft Power Platform

owner: Low Code Team
version: 1.0.0
status: Approved
review_date: 2027-06-15

audience:
  - Solution Architect
  - Developer
  - Maker
  - Platform Administrator

tags:
  - architecture
  - patterns
  - trade-offs
  - selection

related_documents:
  - docs/power-platform/pp-reference-catalog-components.md
  - docs/power-platform/pp-best-practices-catalog.md
  - docs/power-platform/pp-procedures-component-selection.md

---

# Power Platform Solution Patterns

## Purpose

This document defines reusable architectural patterns for selecting the correct Power Platform components based on common business scenarios. Use these patterns to evaluate trade-offs between technologies and ensure the chosen solution aligns with enterprise standards for scalability, security, and maintainability.

## Pattern Definitions

The following patterns cover the most common architectural decision points within the Power Platform ecosystem.

### Canvas Apps vs. Code Apps

#### Intent

Determine whether a solution requires the rapid deployment of a customized business interface or the full control of a professional software engineering model.

#### Implementation

- Use **Canvas Apps** for rapid, low-code iteration where the primary goal is a tailored task experience or mobile interaction.
- Use **Code Apps** when the solution requires a fully bespoke UI, advanced frontend frameworks (e.g., React, Vue), or complex client-side logic that exceeds the capabilities of Canvas components.

#### Trade-offs

| Factor | Canvas Apps | Code Apps |
| --- | --- | --- |
| **Development Speed** | High (Rapid iteration) | Moderate (Requires professional SDLC) |
| **Customization** | Moderate (Component-based) | High (Code-first control) |
| **Maintenance** | Low-code managed | Standard software engineering |

#### Guardrails

- Avoid Code Apps when requirements can be met with Canvas Apps or Model-Driven Apps.
- Avoid Canvas Apps for high-complexity, multi-layered enterprise application logic.

#### Why This Matters

Selecting the right model ensures that the development effort remains proportionate to the requirement. Canvas Apps provide speed for standard business tasks, while Code Apps offer the engineering control required for high-scale, bespoke experiences.

### Model-Driven Apps vs. Code Apps

#### Intent

Evaluate whether the solution requires a data-centric, standardized UI (Model-Driven) or a custom-developed, high-UX interactive experience (Code Apps).

#### Implementation

- Use **Model-Driven Apps** for process-focused solutions, complex data-modeling, and standard CRM-like interactions where the UI should be automatically generated from the Dataverse schema.
- Use **Code Apps** when the primary value is a highly bespoke screen layout, advanced UX, or software-centric design that cannot be achieved within the standardized Model-Driven framework.

#### Trade-offs

| Factor | Model-Driven Apps | Code Apps |
| --- | --- | --- |
| **Implementation Basis** | Data-model driven | Design-centric |
| **Development Model** | Low-code/Configuration | Pro-code/Frameworks |
| **UI Control** | Standardized/Controlled | Fully Customizable |

#### Guardrails

- Avoid Code Apps when the solution can be met with Model-Driven Apps.
- Avoid Model-Driven Apps for cases where a fully bespoke, non-standard UI is the primary requirement.

#### Why This Matters

Model-Driven Apps provide the fastest route for data-centric, role-based processes. Code Apps are reserved for scenarios where standard, data-driven UI patterns are insufficient for the required experience.

### Cloud Flows vs. Agent Flows

#### Intent

Determine whether a workflow should be a general-purpose, standalone automation (Cloud Flow) or a specialized, conversational, agent-coupled interaction (Agent Flow).

#### Implementation

- Use **Cloud Flows** for standard, multi-step, system-to-system automation, scheduled jobs, and high-volume data processing.
- Use **Agent Flows** only when the automation is initiated by, embedded in, or tightly coupled to a Copilot Studio agent experience and requires reasoning-based interaction.

#### Trade-offs

| Factor | Cloud Flows | Agent Flows |
| --- | --- | --- |
| **Integration Type** | System-to-System | Conversational / Agentic |
| **Execution Trigger** | API, Event, Schedule | Agent Query, Conversational Context |
| **Access Model** | Flow-centric | Agent-centric |

#### Guardrails

- Do not use Agent Flows for general enterprise background automation; use Cloud Flows instead.
- Do not use Cloud Flows for high-frequency, agent-coupled interactions that require Copilot Studio context.

#### Why This Matters

Flows should be designed based on their primary activator. Cloud Flows remain the standard for enterprise-wide automation; Agent Flows are for the specific needs of AI-driven, conversational experiences.

### Desktop Flows vs. Computer Use

#### Intent

Compare the choice between deterministic, script-based Robotic Process Automation (Desktop Flows) and agentic, vision-based UI automation (Computer Use).

#### Implementation

- Use **Desktop Flows** for repeated, deterministic RPA tasks where the execution path is stable and can be scripted reliably.
- Use **Computer Use** when an agent must interact with a website or desktop application through visual perception and reasoning, typically when no reliable API or connector exists.

#### Trade-offs

| Factor | Desktop Flows | Computer Use |
| --- | --- | --- |
| **Automation Model** | Deterministic / Scripted | Reasoning / Visual |
| **UI Interaction** | Fixed UI elements | Visual perception/Dynamic Interaction |
| **Use Case** | High-volume, repetitive tasks | Low-frequency, variable UI tasks |

#### Guardrails

- Use Desktop Flows whenever a reliable API or connector is available.
- Use Computer Use only as a last resort when no stable API, connector, or flow-based integration can meet the requirement.

#### Why This Matters

Desktop Flows offer predictable, high-volume execution. Computer Use provides flexibility for non-standard interfaces but requires stronger governance, credential controls, and human-in-the-loop checkpoints due to its dynamic nature.

## Common Pattern Comparisons

### Interaction Type Comparison

| Scenario | Primary Recommendation | Secondary Recommendation |
| --- | --- | --- |
| **High-Volume Batch** | Cloud Flows | Desktop Flows |
| **Human-in-the-Loop** | Cloud Flows | Canvas Apps |
| **Multi-Turn Conversational** | Copilot Studio | Canvas Apps |
| **Legacy System Processing** | Desktop Flows | Cloud Flows |

## Change Log

- **2026-08-27**: Initial Draft
