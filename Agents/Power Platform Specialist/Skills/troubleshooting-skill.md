---
name: "troubleshooting-skill"
description: "Diagnose Power Platform issues and return structured diagnostic and resolution data."
---

# troubleshooting-skill

## Purpose

Diagnose Power Platform issues and provide structured diagnostic steps, resolution paths, and preventive guidance.

## Input Contract

{
  "query": "[User issue description]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing]",
  "add_context": "[Optional additional details]"
}

## Output Contract (SKILL SPECIFIC)

Return ONLY valid JSON:

{
  "diagnosis": "",
  "confidence": "High | Medium | Low",
  "requires_escalation": ["true | false"],
  "issue_category": "",
  "diagnostic_steps": [],
  "resolution_paths": [],
  "prevention": [],
  "monitoring": [],
  "sources": []
}

## KB Orchestration Pattern

Use internal knowledge bases through role-based reasoning.

### KB Role Mapping (SKILL SPECIFIC)
  
Primary role:

- Troubleshooting

Supporting roles:

- Best Practices
- Architecture Guidance
- Governance & Constraints

### Role Selection Rules

- Use **Troubleshooting** to identifying fixes and drive decisions (mandatory)
- Use **Best Practices** for performance and maintainability
- Use **Governance & Constraints** for security and policy compliance
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
- Ensure all outputs are structured and concise.

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

### Field Mapping (SKILL SPECIFIC)

Map each output field to KB roles:

- "diagnosis" → Troubleshooting
- "confidence" → Troubleshooting
- "requires_escalation" → Troubleshooting
- "issue_category" → Troubleshooting
- "diagnostic_steps" → Troubleshooting
- "resolution_paths" → Troubleshooting
- "prevention" → Best Practices and Architecture Guidance
- "monitoring" → Best Practices and Governance & Constraints
- "sources" → Troubleshooting

### Object Shapes

"diagnosis": ""

"confidence": "High | Medium | Low"

"issue_category": [
  "Performance",
  "Licensing",
  "Architecture",
  "Security",
  "Governance",
  "Integration",
  "Data Management",
  "User Experience"
]

"diagnostic_steps": [
  { Step 1: "Description of the first diagnostic step" },
  { Step 2: "Description of the second diagnostic step" }
]

"resolution_paths": [
  Path 1: "Description of the first resolution path",
  Path 2: "Description of the second resolution path"
]

"prevention": [
  "Best practice 1: Description of the first preventive measure",
  "Best practice 2: Description of the second preventive measure"
  ]

"monitoring": [
  "Monitoring practice 1: Description of the first monitoring measure",
  "Monitoring practice 2: Description of the second monitoring measure"
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
  "requires_escalation": "true",
  "missing_inputs/assumptions": "[List missing inputs or assumptions]",
  "sources": "[List sources used for partial reasoning]"
}
```

## Behavior Constraints

- Do NOT generate user-facing explanations
- Do NOT ask follow-up questions
- Do NOT perform conversational actions
- Focus only on structured reasoning output
