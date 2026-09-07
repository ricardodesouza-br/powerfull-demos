---
name: "performance-skill"
description: "Diagnose Power Platform performance bottlenecks and recommend optimization strategies with measurable impact."
---

# performance-skill

## Purpose

Diagnose performance bottlenecks in Power Platform solutions and recommend validated optimization strategies based on internal KBs and Microsoft guidance.

## Input Contract

```json
{
  "query": "[User issue description]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing]",
  "add_context": "[Optional additional details]"
}
```

## Output Contract (SKILL SPECIFIC)
  
Return ONLY valid JSON:

```json
{
  "probable_causes": [],
  "validation_tasks": [],
  "recommended_actions": [],
  "monitoring_actions": [],
  "best_practices": [],
  "overall_confidence": "High | Medium | Low",
  "requires_escalation": ["true | false"],
  "sources": []
}
```

## KB Orchestration Pattern

Use internal knowledge bases through role-based reasoning.

### Role Mapping (SKILL-SPECIFIC)
  
Primary role:

- Troubleshooting  

Supporting roles:

- Best Practices
- Governance & Constraints

### Role Selection Rules

- Use **Troubleshooting** to drive decisions and identifying fixes
- Use **Best Practices** for performance and maintainability
- Use **Governance & Constraints** for security and policy compliance
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

### Field Mapping

Map each output field to KB roles:

- "probable_causes" → Troubleshooting
- "validation_tasks" → Troubleshooting
- "recommended_actions" → Troubleshooting
- "monitoring_actions" → Governance & Constraints
- "best_practices" → Best Practices
- "overall_confidence" → Troubleshooting
- "requires_escalation" → Troubleshooting
- "sources" → Troubleshooting

### Object Shapes

"probable_causes": [
  {
    "cause": "",
    "category": "",
    "likelihood": "High | Medium | Low",
    "impact": "High | Medium | Low",
    "priority_score": "",
    "ranking_position": "",
    "confidence": "High | Medium | Low",
    "evidence": "",
    "kb_reference": "",
    "correlations": [
      {
       "related_cause": "",
        "relationship": "Amplifies | DependsOn | Co-occursWith",
        "effect": "",
        "severity_multiplier": "Low | Medium | High"
      }
    ]
  }
]

"validation_tasks": [
  {
    "related_cause": "",
    "task": "",
    "target": "",
    "expected_result": "",
    "interpretation": ""
  }
]

"recommended_actions": [
  {
    "related_cause": "",
    "type": "Quick Fix | Optimization | Architectural | Escalation",
    "effort": "Low | Medium | High",
    "risk": "Low | Medium | High",
    "actions": []
  }
]

"monitoring_actions": [
  {
    "metric": "",
    "target": "",
    "method": "",
    "success_criteria": ""
  }
]

"best_practices": []

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
