---
name: "licensing-skill"
description: "Identify required Power Platform components and validate licensing requirements, limits, feature availability, and capacity add-ons based on user scenarios."
---

# licensing-skill

## Purpose
  
Identify which Power Platform components meet the user objective and determine the required licensing model, including limits, feature availability, and required capacity add-ons.

## Input Contract

{
  "query": "[User request]",
  "query_type": "[Solution | Architecture | Licensing]",
  "add_context": "[Optional additional details such as expected scale, connectors, automation, or data sources]"
}

## Output Contract (MANDATORY)
  
Return ONLY valid JSON:{
  "recommended_components": [],
  "licensing_requirements": [],
  "license_capabilities": [],
  "license_options": [],
  "capacity_addons": [],
  "confidence": "High | Medium | Low",
  "requires_escalation": false,
  "sources": []
}

## KB Orchestration Pattern
  
Use internal knowledge bases through role-based reasoning.

### 1. KB Roles Applicable for this Skill

Primary role:

- Licensing  

Supporting roles:

- Component Selection
- Architecture Guidance

### 2. Internal KB Metadata Mapping

Use internal KB metadata to identify documents associated with each KB role.

| KB Role | Preferred `KB Roles` value | `Keyword` values | Typical `Product` values |
| --- | --- | --- | --- |
| **Licensing** | Licensing | license, licensing comparison, entitlements, limits, capacity, add-ons | All Products, Copilot Studio/M365 Copilot |
| **Component Selection** | Component Selection | Power Apps, Power Automate, Copilot Studio, Power Pages, AI Builder, Dataverse, Copilot Credits, component capability matrix, connector classification, premium features, standard features | All Products |
| **Architecture Guidance** | Architecture Guidance | Architecture, Solution Blueprint, Architecture discovery, Governance, Security, compliance, ALM, licensing dependencies, scale assumptions, API/storage capacity, solution topology | All Products |

### 3.  Role Selection and Metadata Retrieval Rules

- Always use **Licensing** as the primary reasoning driver.
- When internal KB returns documents with `KB Roles = Licensing`,  use those documents first.
- Use **Component Selection** documents when the request requires **choosing Power Platform components or connectors**.
- Use **Architecture Guidance** documents when scale, automation volume, storage, API usage, or solution dependencies affect licensing.
- Prefer documents whose `Product` metadata matches the requested Power Platform product.
- Prefer `Keyword` values relevant to the request:
  - License Comparison for license-model selection
  - Limits for API, run, transaction, or entitlement questions
  - Add-on for AI Builder, Dataverse capacity, RPA, or additional capacity questions
  - Design Guidance for multi-component licensing dependencies
- Use a maximum of 2–3 retrieved internal documents.
- A document matching the primary role and product is preferred over a generic document.
- Do not select documents by filename, folder hierarchy, or manual re-ranking of SharePoint results.

### 4. Source Prioritization

- Use internal KB as **primary source**
- Use Microsoft documentation to:
  - Validate licensing rules, limits, and add-ons
  - Confirm feature availability (Dataverse, premium connectors, AI Builder, RPA)
If conflict exists:
  - Prioritize Microsoft documentation for licensing accuracy
  - Preserve internal governance constraints if applicable
- Treat internal KB metadata as the document-classification source.
- Use only metadata returned by the search result or supported by the retrieval configuration.
- If metadata is not available in the retrieved result, use the document content and the SharePoint ranking; do not infer undocumented role assignments.
- Validate time-sensitive licensing claims with Microsoft documentation.
- Match the request to relevant document sections, such as License Comparison, Limits, Capacity, or Add-ons.
- Prefer specific licensing, entitlement, capacity, and add-on sections over generic product overviews.
- Extract relevant sections rather than relying on the full document.

### 5. KB Usage Constraints

- Ensure alignment with selected licensing and add-on scenarios
- Do not infer unsupported licensing or add-on combinations
- Avoid mixing unrelated product domains

## Core Requirements

- Use Licensing role to:
  - Determine required licenses based on scenario
  - Validate limits (transactions, runs, API calls)
  - Identify feature availability per license
  - Identify when capacity add-ons are required
- Use Component Selection to:
  - Map user goals to Power Platform components
- Use Architecture Guidance to:
  - Identify multi-license dependencies
  - Determine when base licensing is insufficient without add-ons
- Always:
  - Distinguish included vs additional capacity
  - Highlight dependencies between licenses and add-ons
  - Provide alternative license paths when applicable

### Extended Scope

- Include guidance on how to check or validate assigned licenses
- Include observable indicators (premium connectors, Dataverse access)

## Output Field Mapping

- "recommended_components" → Component Selection role  
- "licensing_requirements" → Licensing role  
- "license_capabilities" → Licensing role  
- "license_options" → Architecture Guidance role  
- "capacity_addons" → Licensing + Architecture Guidance roles  

Field definitions:

- recommended_components → Power Platform components required (e.g., Power Apps, Power Automate, Dataverse)
- licensing_requirements → Required licenses or combinations to support the scenario
- license_capabilities → Key limits and features (e.g., premium connectors, Dataverse access, API limits)
- license_options → Alternative license models providing similar capabilities
- capacity_addons → Required or recommended add-ons (e.g., AI Builder credits, Dataverse storage, unattended RPA, additional API capacity)

## Confidence Guidelines

- **High** → Clear mapping of licenses and add-ons validated with documentation
- **Medium** → Multiple valid combinations or partial uncertainty on capacity needs
- **Low** → Missing scale/context or unclear requirements

## Output Rules (MANDATORY)

- Return ONLY valid JSON
- Do NOT include Markdown, explanations, or conversational text
- Do NOT repeat the input query
- Keep all fields concise (1–2 sentences)

## Output Constraints

- Limit lists to 3 items unless necessary
- Avoid verbose explanations
- Prefer structured entries (short phrases or lightweight objects)

## Reference Rules (MANDATORY)

- Populate ONLY the "sources" field
- Include sources only when used

### Sources Format

{
  "title": "",
  "url": "",
  "type": "InternalKB | MicrosoftLearn",
  "section": ""
}

## Error Handling
  
If context is insufficient:{
  "recommended_components": [],
  "licensing_requirements": [],
  "license_capabilities": [],
  "license_options": [],
  "capacity_addons": [],
  "confidence": "Low",
  "requires_escalation": false,
  "sources": []
}

## Behavior Constraints

- Do NOT generate user-facing explanations
- Do NOT ask follow-up questions
- Do NOT troubleshoot issues
- Do NOT estimate costs
- Focus strictly on licensing validation, component mapping, and add-ons identification
