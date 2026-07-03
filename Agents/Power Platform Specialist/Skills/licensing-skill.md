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

### 1. KB Roles

- **Diagnosis** → Identify root cause of issues
- **Resolution** → Provide actionable fixes
- **Component Selection** → Identify suitable Power Platform features
- **Architecture Guidance** → Structure solution design and blueprints
- **Best Practices** → Improve performance, scalability, and maintainability
- **Governance & Constraints** → Apply policies (DLP, security, environments, ALM)
- **Licensing** → Validate licensing requirements and limits

### 2. Role Mapping (SKILL-SPECIFIC)
  
Primary role:

- Licensing  

Supporting roles:

- Component Selection
- Architecture Guidance

### 3. Role Selection Rules

- Always use Licensing as the primary reasoning driver
- Use Component Selection when user intent involves solution design
- Use Architecture Guidance when scale, automation volume, or data usage impacts licensing
- Trigger capacity_addons evaluation when:
  - High volume transactions or API calls are implied
  - AI Builder, Dataverse storage, or unattended RPA is referenced
  - PAYG or consumption-based scenarios are applicable

### 4. Source Prioritization

- Use internal KB as primary source
- Use Microsoft documentation to:
  - Validate licensing rules, limits, and add-ons
  - Confirm feature availability (Dataverse, premium connectors, AI Builder, RPA)
If conflict exists:
- Prioritize Microsoft documentation for licensing accuracy
- Preserve internal governance constraints if applicable

### 5. KB Selection Rules

- Select KBs focused on licensing models, entitlements, capacity, and add-ons
- Match query to structured sections (e.g., License Comparison, Limits, Capacity, Add-ons)
- Prioritize:
  - Specific license types (Per App, Per User, PAYG, Power Automate plans)
  - Feature availability (Dataverse, Premium connectors)
  - Capacity metrics (API calls, AI credits, storage, attended/unattended RPA)
- Avoid generic product overviews

### 6. KB Usage Constraints

- Use a maximum of 2–3 KB sources
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
