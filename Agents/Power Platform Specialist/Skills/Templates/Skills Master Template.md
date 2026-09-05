---
name: "<skill-name>"
description: "<Short description aligned with purpose>"
---

# skill name

## Purpose

Describe what this skill does in 1–2 sentences

## Input Contract (MANDATORY)

```json
{
  "query": "[User request]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing | Governance]",
  "add_context": "[Optional additional details]"
}
```

## Output Contract (MANDATORY)

Return ONLY valid JSON:

*EXAMPLE STRUCTURE — CUSTOMIZE PER SKILL*

```json
{
  "<field_1>": "",
  "<field_2>": "",
  "confidence": "High | Medium | Low",
  "requires_escalation": false,
  "sources": []
}
```

## KB Orchestration Pattern

Use internal knowledge bases through role-based reasoning.

### KB Role Mapping for this skill

Primary role:

*!!! DEFINE PRIMARY ROLE !!!*

Supporting roles:

- *!!! DEFINE 1–3 SUPPORTING ROLES !!!*

### Role Selection Rules

- Always use ONE primary role
- Use up to TWO supporting roles when needed
- Prefer specific roles over generic guidance
- Avoid using more than 3 roles unless strictly required
- Use the canonical roles: Diagnosis, Resolution, Component Selection, Architecture Guidance, Best Practices, Governance & Constraints, Licensing.
- Use the `query_type` of `[Solution | Troubleshooting | Architecture | Performance | Licensing | Governance]` for coordinated-led routing, but identify and use the 7 canonical roles for internal KB-based reasoning.

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

## Output Field Mapping

- Map each output field to KB roles:
  
*EXAMPLE STRUCTURE — CUSTOMIZE PER SKILL*

- "<field_1>" → Primary role
- "<field_2>" → Secondary role
- "<field_3>" → Best Practices or Governance role
- Ensure all output fields are typed (e.g., String, Array, Object)
- Provide a default/empty fallback value for every field
- Define the max cardinality for any list fields
- Ensure consistency between:
  - diagnosis ↔ Diagnosis role
  - resolution ↔ Resolution role
  - prevention ↔ Best Practices role
  - monitoring ↔ Governance role
  - design ↔ Architecture role

## Confidence Guidelines

- **High** → Strong match with primary KB role + validated by Microsoft documentation
- **Medium** → Partial KB match or requires supporting roles
- **Low** → Weak KB match, ambiguity, or insufficient context
- If any required input is missing or context is insufficient, set `requires_escalation: true`.

## Output Rules (MANDATORY)

- Return ONLY valid JSON
- Do NOT include Markdown, explanations, or conversational text
- Do NOT repeat the input query
- Keep all fields concise (1–2 sentences)
- Default list length is 3 unless explicitly overridden in Output Constraints.

## Output Constraints

- Limit lists to 3 items unless necessary
- Avoid verbose explanations
- Prefer structured content over narrative

## Reference Rules (MANDATORY)

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
