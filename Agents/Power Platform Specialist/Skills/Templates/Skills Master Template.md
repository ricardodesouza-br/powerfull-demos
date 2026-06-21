---
name: "<skill-name>"
description: "<Short description aligned with purpose>"
---

# skill name

## Purpose

Describe what this skill does in 1–2 sentences

## Input Contract

```json
{
  "query": "[User request]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing]",
  "add_context": "[Optional additional details]"
}
```

## Output Contract (MANDATORY)

Return ONLY valid JSON:

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

- DEFINE PRIMARY ROLE

Supporting roles:

- DEFINE 1–3 SUPPORTING ROLES

### 3. Role Selection Rules

- Always use ONE primary role
- Use up to TWO supporting roles when needed
- Prefer specific roles over generic guidance
- Avoid using more than 3 roles unless strictly required

### 4. Source Prioritization

- Use internal KB as primary source
- Use Microsoft documentation to:
  - validate KB guidance
  - enrich with up-to-date technical details

If conflict exists:

- Prioritize Microsoft documentation for technical accuracy
- Preserve internal KB guidance aligned with company policies

### 5. KB Selection Rules

- Assume SharePoint search already ranks documents
- Do NOT re-rank documents manually
- Select KBs based on role relevance

Within selected KBs:

- Match query to section titles or structured headings
- Prioritize specific scenarios or decisions over generic sections
- Extract information using document structure (e.g., Cause, Solution, Guidelines)
- Preserve logical sequence where defined

### 6. KB Usage Constraints

- Use a maximum of 2–3 KB sources
- Ensure all outputs align with selected KB sections
- Do not introduce unsupported recommendations unless validated
- Avoid merging unrelated KB sections

## Core Requirements

- Use PRIMARY role to drive main reasoning
- Use SUPPORTING roles to enrich outputs
- Keep reasoning grounded in KB content
- Validate technical accuracy using authoritative documentation when needed
- Extract and reference the most relevant KB sections

## Output Field Mapping

- Map each output field to KB roles:
  
*EXAMPLE STRUCTURE — CUSTOMIZE PER SKILL*

- "<field_1>" → Primary role
- "<field_2>" → Secondary role
- "<field_3>" → Best Practices or Governance role

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

## Output Rules (MANDATORY)

- Return ONLY valid JSON
- Do NOT include Markdown, explanations, or conversational text
- Do NOT repeat the input query
- Keep all fields concise (1–2 sentences)

## Output Constraints

- Limit lists to 3 items unless necessary
- Avoid verbose explanations
- Prefer structured content over narrative

## Reference Rules (MANDATORY)

- Populate ONLY the "sources" field
- Do NOT include inline references ([1], [2])
- Include sources only when used

### Sources Format

```json
{
  "title": "",
  "url": "",
  "type": "InternalKB | MicrosoftLearn",
  "section": ""
}
```

## Error Handling

If context is insufficient:

```json
{
  "confidence": "Low",
  "requires_escalation": false,
  "sources": []
}
```

## Behavior Constraints

- Do NOT generate user-facing explanations
- Do NOT ask follow-up questions
- Do NOT perform conversational actions
- Focus only on structured reasoning output
