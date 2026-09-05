---
name: "licensing-skill"
description: "Identify required Power Platform components and validate licensing requirements, limits, feature availability, and capacity add-ons based on user scenarios."
---

# licensing-skill

## Purpose
  
Identify which Power Platform components meet the user objective and determine the required licensing model, including limits, feature availability, and required capacity add-ons.

## Input Contract

```json
{
  "query": "[User request]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing | Governance]",
  "add_context": "[Optional additional details]"
}
```

## Output Contract (SKILL SPECIFIC)
  
Return ONLY valid JSON:

```json
{
  "recommended_components": [],
  "licensing_requirements": [],
  "license_capabilities": [],
  "license_options": [],
  "capacity_addons": [],
  "confidence": "High | Medium | Low",
  "requires_escalation": false,
  "sources": []
}
```

## KB Orchestration Pattern
  
Use internal knowledge bases through role-based reasoning.

### Role Mapping (SKILL SPECIFIC)
  
Primary role:

- Licensing  

Supporting roles:

- Component Selection
- Architecture Guidance

### Role Selection Rules (SKILL SPECIFIC)

- Use **Licensing** to drive decisions (mandatory).
- Use **Component Selection** for choosing Power Platform components or connectors
- Use **Architecture Guidance** when scale, automation volume, storage, API usage, or solution dependencies affect licensing
- Do not exceed 3 roles per request

### Source Prioritization

- Use internal KB as primary source
- Use Microsoft documentation to:
  - validate KB guidance
  - enrich with up-to-date technical details

If conflict exists:

- Prioritize Microsoft documentation for technical accuracy
- Preserve internal KB guidance aligned with company policies

### KB Selection Rules

- Assume KB search already ranks documents
- Do NOT re-rank documents manually
- Select KBs based on role relevance

Within selected KBs:

- Match query to section titles or structured headings
- Prioritize specific scenarios or decisions over generic sections
- Extract information using document structure (e.g., Cause, Solution, Guidelines)
- Preserve logical sequence where defined

### KB Usage Constraints

- Use a maximum of 2–3 KB sources
- Ensure all outputs align with selected KB sections
- Do not introduce unsupported recommendations unless validated
- Avoid merging unrelated KB sections
- Use only sources actually used.
- Ensure Microsoft Learn is only used for time-sensitive or technically authoritative validation.

## Core Requirements

- Use PRIMARY role to drive main reasoning
- Use SUPPORTING roles to enrich outputs
- Keep reasoning grounded in KB content
- Validate technical accuracy using authoritative documentation when needed
- Extract and reference the most relevant KB sections
- Ensure all outputs are structured and concise.

## Confidence Guidelines

- **High** → Strong match with primary KB role + validated by Microsoft documentation
- **Medium** → Partial KB match or requires supporting roles
- **Low** → Weak KB match, ambiguity, or insufficient context
- If any required input is missing or context is insufficient, set `requires_escalation: true`.

## Reference Rules

- Populate ONLY the "sources" field
- Include sources only when used

### Sources Format

```json
{
  "title": "[Source title]",
  "url": "[Source URL]",
  "type": "InternalKB | MicrosoftLearn",
  "section": "[Section title or heading]"
}
```

## Output Requirements

### Rules

- Return ONLY valid JSON
- Do NOT include Markdown, explanations, or conversational text
- Do NOT repeat the input query
- Keep all fields concise (1–2 sentences)
- Default list length is 3 unless explicitly overridden in Output Constraints.

### Field Mapping (SKILL SPECIFIC)

Map each output field to KB roles:

- "recommended_components" → Component Selection
- "licensing_requirements" → Licensing
- "license_capabilities" → Licensing
- "license_options" → Licensing
- "capacity_addons" → Licensing
- "confidence" → Licensing
- "requires_escalation" → Licensing
- "sources" → Licensing

### Object Shapes (SKILL SPECIFIC)

!!! DEFINE OUTPUT OBJECT SHAPES PER FIELD !!!

### Constraints

- Limit primary recommendation to 1 core solution.
- Provide a maximum of 3 alternative approaches.
- Responses must be directly applicable to the Power Platform (not general software engineering).
- Do not recommend features that are not accessible via the Power Platform.

## Error Handling

If context is insufficient:

```json
{
  "confidence": "Low",
  "requires_escalation": true,
  "missing_inputs/assumptions": "[List missing inputs or assumptions]",
  "sources": "[List sources used for partial reasoning]"
}
```

## Behavior Constraints

- Do not offer opinions; only provide facts based on internal/Microsoft knowledge.
- Avoid technical jargon unless necessary for clarity.
- Ensure tone is helpful, professional, and neutral.
- Do not provide "how-to" steps unless requested; focus on "what" and "why" for implementation patterns.
