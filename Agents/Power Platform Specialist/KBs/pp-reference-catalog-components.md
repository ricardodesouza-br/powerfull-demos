---
title: Power Platform Component Reference Catalog
document_type: ReferenceCatalogs
document_role: Architecture Guidance
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
  - reference
  - platform
  - licensing

related_documents:
  - docs/power-platform/pp-best-practices-catalog.md
  - docs/power-platform/pp-solution-patterns-catalog.md
  - docs/power-platform/pp-procedures-component-selection.md


---

# Power Platform Component Reference Catalog

## Purpose

This catalog provides a comprehensive reference for Microsoft Power Platform components, including definitions, identification of preferred use cases, and technical capability comparisons. Use this reference during the discovery and design phases of a solution to ensure the correct building blocks are selected for the required business outcomes.

## Component Definitions

Use this section to understand the primary purpose and capabilities of each Power Platform offering.

### Canvas Apps

**Best For:** Highly customized, task-oriented user interfaces and interaction-heavy mobile/web experiences.

| Attribute | Details |
| --- | --- |
| **Design Model** | Drag-and-drop canvas; provides pixel-perfect control over layout and interactive elements. |
| **Data Sources** | Supports 900+ connectors, including SharePoint, Excel, Dataverse, SQL, and more. |
| **Licensing** | Standard M365 for basic connectors; Premium required for Dataverse or premium connectors. |

### Model-Driven Apps

**Best For:** Structured data-centric applications, automated business processes, and complex relational data management.

| Attribute | Details |
| --- | --- |
| **Design Model** | Automatically generated, responsive UI based on the Dataverse table schema. |
| **Data Sources** | Requires Microsoft Dataverse. |
| **Licensing** | Requires Power Apps Premium license for Dataverse integration. |

### Code Apps

**Best For:** Complex enterprise applications requiring advanced engineering controls, custom frontend frameworks (React, Vue), and full software development lifecycle management.

| Attribute | Details |
| --- | --- |
| **Development Model** | Code-first development using standard IDEs, source control, and CI/CD pipelines. |
| **User Experience** | Fully customized, professional-grade web application experience. |
| **Data Sources** | Dataverse, Power Platform connectors, Azure SQL, SharePoint, and external APIs. |
| **Licensing** | Requires Power Apps Premium; additional licensing depends on specific services consumed. |

### Power Apps Component Framework (PCF)

**Best For:** Extending the UI of existing Canvas or Model-Driven Apps with custom-coded controls (e.g., specialized charts, interactive maps).

| Attribute | Details |
| --- | --- |
| **Technology** | TypeScript / JavaScript; React support. |
| **Licensing** | Included with the hosting application; no additional license required. |

### Power Automate - Cloud Flows

**Best For:** Cloud-based, event-driven, or scheduled automation of processes, data, and system-to-system integrations.

| Attribute | Details |
| --- | --- |
| **Trigger Types** | Automated (Event), Scheduled, Instant (Manual), or High-Volume. |
| **Licensing** | M365 for standard; Premium plan required for premium connectors or high-volume needs. |

### Power Automate - Desktop Flows (RPA)

**Best For:** Automating manual, repetitive tasks in legacy systems or web applications where no reliable API or connector exists.

| Attribute | Details |
| --- | --- |
| **Execution Modes** | Attended (User-present) or Unattended (Bot-only). |
| **Licensing** | Per-user RPA license; Unattended RPA requires an additional per-bot/machine add-on. |

### Process Advisor

**Best For:** Identifying automation opportunities and inefficiencies by analyzing and visualizing existing human-led business processes.

| Attribute | Details |
| --- | --- |
| **Key Capabilities** | Task recording, process visualization, analytics dashboards, and mining reports. |
| **Licensing** | Premium features; may require per-user license or add-ons. |

### Dataverse

**Best For:** Providing a secure, scalable, and relational data platform for enterprise-grade applications.

| Attribute | Details |
| --- | --- |
| **Key Features** | Relational storage, Business Rules, Security Roles, Audit Logs, and automated Data Logic. |
| **Licensing** | Included with Power Apps/Automate Premium; Limited "Dataverse for Teams" available on M365. |

### Power Pages

**Best For:** Public-facing or external-facing websites (customers, partners, public) built on top of Dataverse data.

| Attribute | Details |
| --- | --- |
| **Key Capabilities** | Responsive web portal templates, custom HTML/CSS/JS, and identity-based access (Web Roles). |
| **Licensing** | Per-site capacity; additional capacity for high-traffic usage. |

### Microsoft Copilot Studio

**Best For:** Creating and orchestrating conversational AI agents (copilots) for querying knowledge, performing actions, and reasoning across data.

| Attribute | Details |
| --- | --- |
| **Core Features** | Conversational flow design, LLM integration, Plugin/Tool actions, and Agent Flows. |
| **Licensing** | Premium capability; requires Microsoft 365 Copilot or specific Copilot Credits. |

### Connectors

**Best For:** Integrating the Power Platform with over 900 external services (SharePoint, SQL, Salesforce, etc.).

| Attribute | Details |
| --- | --- |
| **Standard** | Included in basic licenses (SharePoint, Outlook, etc.). |
| **Premium** | Require Premium license (SQL, SAP, Salesforce, etc.). |

### AI Builder

**Best For:** Embedding pre-built or custom-trained AI models (OCR, Prediction, Sentiment Analysis) directly into Apps and Flows.

| Attribute | Details |
| --- | --- |
| **Model Types** | Prebuilt (Invoice, Business Card) or Custom (Prediction, Object Detection). |
| **Licensing** | Consumes Copilot Credits per operation. |

## Requirement to Component Mapping

Use this matrix to identify the preferred platform based on the primary business requirement.

| Requirement | Preferred Component | Key Considerations |
| --- | --- | --- |
| **Internal Task Experience** | Canvas Apps | Use for tailored UI; avoid for public-facing access. |
| **Structured Business Process** | Model-Driven Apps | Best for data-centric processes and row-level security. |
| **Enterprise Custom Software** | Code Apps | Choose when advanced engineering control is required. |
| **External Portal / Public Access** | Power Pages | Required for any external-facing website or public access. |
| **Conversational Assistant** | Copilot Studio | The primary platform for multi-turn conversational AI. |
| **Embedded AI / Prediction** | AI Builder | Best for specific model-based tasks inside an app/flow. |
| **Workflow & Automation** | Cloud Flows | Standard for API-based, event-driven, or scheduled jobs. |
| **Legacy System Automation** | Desktop Flows | Use ONLY when no stable API/connector is available. |
| **Relational Data Store** | Dataverse | The standard for enterprise relational data and security. |
| **Shared Interaction/Knowledge** | Copilot Studio | For any requirement involving AI-driven conversational loops. |

## Capability Comparisons

### Component Selection Comparison

| Attribute | Canvas Apps | Model-Driven Apps | Code Apps |
| --- | --- | --- | --- |
| **Primary Use** | Custom UI / Task experience | Process-centric / Data-centric | Advanced Engineering / Pro-Code |
| **Design Basis** | Drag-and-drop Canvas | Data-model generated UI | Code-first IDE / Web Frameworks |
| **Implementation** | Low-code/Maker-led | Data-heavy / Admin-led | Professional Software Engineer |
| **Best For** | High-fidelity UI, Mobile interaction | CRM, Case Mgmt, Records | Complex Apps, Custom UI, Heavy logic |

## Common Attributes

### Technical Comparison

| Attribute | Canvas Apps | Model-Driven Apps | Code Apps |
| --- | --- | --- | --- |
| **Data Access** | Multi-source (Power Platform) | Dataverse-centric | Dataverse/SQL/API/Shared |
| **Scalability** | High (with proper design) | High (Native to Dataverse) | High (App Tier dependent) |
| **Identity** | Microsoft Entra ID | Microsoft Entra ID | Microsoft Entra ID |

## Change Log

- **2026-08-27**: Initial Draft
