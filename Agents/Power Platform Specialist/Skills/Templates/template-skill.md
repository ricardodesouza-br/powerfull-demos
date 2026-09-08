---
name: "<skill-name>"
description: "<Short description aligned with purpose>"
---

<!--
AUTHORING INSTRUCTIONS:
1. Replace all [brackets] with specific information.
2. Keep the metadata in the YAML front matter accurate.
3. Maintain the heading hierarchy (H1, H2, H3, H4).
4. Do not remove existing sections unless they are not applicable to this skill.
5. Do not remove existent rules or guidelines unless they are not applicable to this skill.
6. Identify as "Skill Specific" new sections or rules.
7. Remove helpful authoring instructions before publishing.
8. Update the Change Log.
9. Review Markdown diagnostics in VS Code.
-->

# skill name

## Purpose

[Describe what this skill does in 1–2 sentences]

## Input Contract

```json
{
  "query": "[User request]",
  "query_type": "[Diagnosis | Resolution | Component Selection | Architecture Guidance | Best Practices | Governance & Constraints | Licensing]",
  "add_context": "[Optional additional details]"
}
```

## Output Contract (SKILL SPECIFIC)

Return ONLY valid JSON:

[Sample output contract for this skill, including all required fields and their types. Use JSON schema or a similar format to define the structure.]

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

### KB Role Mapping (SKILL SPECIFIC)

Primary role:

[DEFINE PRIMARY ROLE]

Supporting roles:

[DEFINE 1–3 SUPPORTING ROLES]

### Role Selection Rules (SKILL SPECIFIC)

- Use [Primary Role] to drive decisions (mandatory).
- Use [Supporting Role 1] for [specific purpose].
- Use [Supporting Role 2] for [specific purpose].
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
  
[EXAMPLE STRUCTURE — CUSTOMIZE PER SKILL]

- "<field_1>" → Primary role
- "<field_2>" → Secondary role
- "<field_3>" → Secondary role

<!-- INSTRUCTIONS FOR SKILL AUTHORS:
- Ensure all output fields are typed (e.g., String, Array, Object)
- Provide a default/empty fallback value for every field
- Define the max cardinality for any list fields
- Ensure consistency between:
  - diagnosis ↔ Diagnosis role
  - resolution ↔ Resolution role
  - prevention ↔ Best Practices role
  - monitoring ↔ Governance role
  - design ↔ Architecture role
-->

### Object Shapes (SKILL SPECIFIC)

[EXAMPLE STRUCTURE — CUSTOMIZE PER SKILL]

!!! DEFINE OUTPUT OBJECT SHAPES PER FIELD !!!

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
