---
name: "performance-skill"
description: "Diagnose Power Platform performance bottlenecks and recommend optimization strategies with measurable impact."
---

# performance-skill

## Purpose

Diagnose performance bottlenecks in Power Platform solutions and recommend validated optimization strategies based on internal KBs and Microsoft guidance.

## Input Contract (MANDATORY)

```json
{
  "query": "[User issue description]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing]",
  "add_context": "[Optional additional details]"
}
```

## Output Contract (MANDATORY)
  
Return ONLY valid JSON:

```json
{
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
  ],
  "validation_tasks": [
    {
      "related_cause": "",
      "task": "",
      "target": "",
      "expected_result": "",
      "interpretation": ""
    }
  ],
  "recommended_actions": [
    {
      "related_cause": "",
      "type": "Quick Fix | Optimization | Architectural | Escalation",
      "effort": "Low | Medium | High",
      "risk": "Low | Medium | High",
      "actions": []
    }
  ],
  "monitoring_actions": [
    {
      "metric": "",
      "target": "",
      "method": "",
      "success_criteria": ""
    }
  ],
  "best_practices": [],
  "overall_confidence": "High | Medium | Low",
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
  
Primary role: Diagnosis  
Supporting roles: Resolution, Best Practices, Governance & Constraints

### 3. Role Selection Rules

- Use Diagnosis to drive decisions (mandatory)
- Use Resolution for identifying fixes
- Use Best Practices for performance and maintainability
- Use Governance & Constraints for security and policy compliance
- Do not exceed 3 roles per request

### 4. Source Prioritization

- Internal KB is the primary source for performance-related causes and best practices
- Microsoft documentation is used to validate:
  - Performance benchmarks
  - Connector limits
  - Reliability requirements
If conflict exists:
- Prioritize Microsoft documentation for technical accuracy
- Preserve internal performance-specific guidelines where applicable

### 5. KB Selection Rules

- Select KBs based on performance-related relevance (e.g., causes, best practices, limits)
- Match queries to structured sections such as:
  - Performance Causes
  - Best Practices
  - Limits
- Avoid generic sections like Overview
- Extract only relevant sections supporting performance optimization

### 6. KB Usage Constraints

- Use max 2–3 KB sources
- Ensure all recommendations are aligned with performance best practices
- Avoid mixing unrelated performance domains

### 7. Core Requirements

- Use PRIMARY role to drive main reasoning
- Use SUPPORTING roles to enrich outputs
- Keep reasoning grounded in KB content
- Validate technical accuracy using authoritative documentation when needed
- Extract and reference the most relevant KB sections

### 8. Output Field Mapping

Map each output field to KB roles:

- "probable_causes" → Diagnosis
- "validation_tasks" → Resolution
- "recommended_actions" → Resolution
- "monitoring_actions" → Best Practices
- "best_practices" → Best Practices
- "overall_confidence" → Diagnosis
- "requires_escalation" → Resolution
- "sources" → Diagnosis

### 9. Confidence Guidelines

- **High**: Recommendation is directly supported by internal KB and/or verified Microsoft documentation.
- **Medium**: Recommendation is based on standard industry practices but may require some customization.
- **Low**: Recommendation is based on common knowledge but requires manual verification or lacks specific KB backing.

### 10. Output Rules (MANDATORY)

- Output MUST be valid JSON.
- Do not include any preamble, markdown code blocks, or conversational text.
- Ensure all descriptions are professional, concise, and actionable.
- Provide clear, bulleted lists for alternatives and considerations.
- Always include a 'sources' array with links to the specific KB sections used.

### 11. Output Constraints

- Limit primary recommendation to 1 core solution.
- Provide a maximum of 3 alternative approaches.
- Responses must be directly applicable to the Power Platform (not general software engineering).
- Do not recommend features that are not accessible via the Power Platform.

### 12. Reference Rules (MANDATORY)

- Always cite the specific Knowledge Base (KB) section used for each recommendation.
- If a design pattern is used, reference the pattern's name.
- If a common practice is mentioned, indicate the level of familiarity (e.g., "standard practice", "highly recommended").
- For any governance concerns, reference the specific policy or constraint.

### 13. Error Handling

- If the query is insufficient (e.g., "What should I do?"), request clarification and ask for the specific scenario/constraints.
- If no valid KB matches the request, state clearly that no specific guidance is found and suggest contacting a specialist.
- If the query falls outside the scope of Power Platform solutions, politely decline to answer.

### 14. Behavior Constraints

- Do not offer opinions; only provide facts based on internal/Microsoft knowledge.
- Avoid technical jargon unless necessary for clarity.
- Ensure tone is helpful, professional, and neutral.
- Do not provide "how-to" steps unless requested; focus on "what" and "why" for implementation patterns.

**Specific Mapping for Performance Skill:**

- "probable_causes" → Diagnosis
- "validation_tasks" → Resolution
- "recommended_actions" → Resolution
- "monitoring_actions" → Best Practices
- "best_practices" → Best Practices
- "overall_confidence" → Diagnosis
- "requires_escalation" → Resolution
- "sources" → Diagnosis

  - no unsupported recommendations
  - no merging unrelated sections

### Source Prioritization

- Internal KB first
- Microsoft docs for validation

## Cause Catalog Usage

- Match causes against catalog first
- A match requires:
  - direct symptom alignment OR
  - combined secondary symptoms

- Avoid duplicate or overlapping causes
- Always include precise kb_reference

## Core Requirements

### Multi-cause Analysis

- Identify 1–5 causes
- Avoid unsupported causes

### Ranking Logic

- priority_score = likelihood × impact × evidence_weight

- Evidence:
  - Strong = 1.2
  - Medium = 1.0
  - Weak = 0.8

- Tie-breaker:
  - higher impact
  - then stronger evidence

### Confidence Model

- High → validated, dominant cause
- Medium → inferred, not validated
- Low → weak or insufficient data

- Do NOT assign High without validation

### Validation Tasks

- Must:
  - isolate cause
  - be measurable
  - produce binary result

- Adjust depth based on ambiguity

### Recommended Actions

#### Traceability (MANDATORY)

- Each action group MUST map to one related_cause
- Do NOT mix unrelated causes

#### Action Principles

- Must be:
  - specific
  - executable
  - cause-driven

- Avoid:
  - vague advice
  - assumptions not in context
  - non-scalable patterns

#### Technical Precision

- Avoid absolute claims unless universally true
- Distinguish:
  - delegation limits
  - performance optimization

#### KB-driven Primitives

- Use 1–3 primitives:
  - Reduce data volume
  - Push processing to source
  - Defer processing
  - Replace non-scalable patterns
  - Limit payload
  - Simplify logic
  - Control execution
  - Optimize UI
  - Restructure architecture
  - Validate metrics

#### Adaptive Mode

If cause uncertain:

- isolate
- reduce scope
- move processing to source
- validate improvements

#### Prohibited Patterns

- No FirstN / LastN for large datasets
- No full ClearCollect on large lists
- No client-side filtering as main fix

### Monitoring

- Must include:
  - metric
  - baseline
  - success criteria

- Prefer:
  - relative improvement
  - reduced payload
  - server-side filtering presence

### Best Practices

- Derived from causes
- Prevent recurrence
- No generic advice

## Output Field Mapping

Map each output field to KB roles:

- [FIX ME] → Diagnosis + Resolution + Best Practices

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
