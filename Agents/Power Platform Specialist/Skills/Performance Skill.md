---
name: "performance-skill"
description: "Diagnose Power Platform performance bottlenecks and recommend optimization strategies with measurable impact."
---

# performance-skill

## Purpose

Diagnose performance bottlenecks in Power Platform solutions and recommend validated optimization strategies based on internal KBs and Microsoft guidance.

## Input Contract

{
  "query": "[User issue description]",
  "query_type": "[Solution | Troubleshooting | Architecture | Performance | Licensing]",
  "add_context": "[Optional additional details]"
}

## Output Contract (MANDATORY)

Return ONLY valid JSON:

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

## KB Orchestration Pattern

Use internal knowledge bases through role-based reasoning.

### KB Roles

- Diagnosis → Identify root cause of issues
- Resolution → Provide actionable fixes
- Best Practices → Improve reliability, performance, and maintainability
- Governance & Constraints → Apply policies

### Role Mapping

Primary role: Diagnosis  
Supporting roles: Resolution, Best Practices, Governance

### Role Usage

- Always use ONE primary role
- Use up to TWO supporting roles
- Prefer the most specific role

### KB Selection & Usage

- Select relevant KB sections (max 2 sources)
- Prioritize specific sections over generic ones

- Extract:
  - Causes from "Cause"
  - Solutions from "Solution"

- Ensure:
  - alignment with KB
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

## Output Rules

- Return ONLY JSON
- No explanations
- Max 1–2 sentences per field

## Output Constraints

- Max 5 causes
- Max 2 validation tasks per cause
- Max 2 action groups per cause
- Max 5 monitoring actions
- Max 7 best practices

- Do NOT include weak causes

- All items must map to related causes
- No inline citations

## Error Handling

If insufficient context:

{
  "probable_causes": [],
  "validation_tasks": [],
  "recommended_actions": [],
  "monitoring_actions": [],
  "best_practices": [],
  "overall_confidence": "Low",
  "requires_escalation": false,
  "sources": []
}
