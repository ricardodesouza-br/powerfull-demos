---
name: "solutioning-skill"
description: "Recommend the best Power Platform approaches and implementation patterns for user scenarios, including alternatives, best practices, and governance considerations."
---

# solutioning-skill

## Purpose
  
Identify the most suitable Power Platform solution approaches for a given scenario and provide up to three structured alternatives, including implementation patterns, best practices, and governance considerations.

## Input Contract

```json
{
  "query": "[User request]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing]",
  "add_context": "[Optional additional details]"
}
```

## Output Contract (SKILL SPECIFIC)
  
Return ONLY valid JSON:

```json
{
  "primary_recommendation": {},
  "alternative_approaches": [],
  "governance_considerations": [],
  "confidence": "High | Medium | Low",
  "requires_escalation": false,
  "sources": []
}
```

## KB Orchestration Pattern
  
Use internal knowledge bases through role-based reasoning.

### KB Role Mapping (SKILL-SPECIFIC)
  
Primary role:

- Component Selection  

Supporting roles:

- Best Practices
- Governance & Constraints
- Architecture Guidance

### Role Selection Rules (SKILL SPECIFIC)

- Use **Component Selection** to drive decisions (mandatory)
- Use **Best Practices** for implementation and maintainability
- Use **Governance & Constraints** for policy and compliance
- Use **Architecture Guidance** when cross-solution or high-scale architecture is required
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

## Confidence Guidelines

- **High** → Strong match with primary KB role + validated by Microsoft documentation
- **Medium** → Partial KB match or requires supporting roles
- **Low** → Weak KB match, ambiguity, or insufficient context
- If any required input is missing or context is insufficient, set `requires_escalation: true`

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

### Field Mapping (SKILL-SPECIFIC)

Map each output field to KB roles:

- "primary_recommendation" → Component Selection + Best Practices roles  
- "alternative_approaches" → Component Selection + Architecture Guidance roles  
- "governance_considerations" → Governance & Constraints role  

### Object Shapes (SKILL-SPECIFIC)

primary_recommendation → Best-fit approach for the scenario  
{
  "name": "",
  "components": [],
  "implementation": "",
  "considerations": []
}

alternative_approaches → Up to 2 alternative solution approaches  
[
  {
    "name": "",
    "components": [],
    "implementation": "",
    "considerations": []
  }
]

governance_considerations:[
  {
    "type": "Governance | Security | Monitoring | Licensing | ALM",
    "detail": ""
  }
]

### Constraints

- Limit lists to 3 items unless necessary
- Avoid verbose explanations
- Prefer structured content over narrative

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

- Do NOT generate user-facing explanations
- Do NOT ask follow-up questions
- Do NOT perform conversational actions
- Focus only on structured reasoning output
