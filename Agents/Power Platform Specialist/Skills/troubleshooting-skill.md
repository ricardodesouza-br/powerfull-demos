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

## Output Contract (MANDATORY)

Return ONLY valid JSON:

{
  "diagnosis": "",
  "confidence": "High | Medium | Low",
  "requires_escalation": false,
  "issue_category": "",
  "diagnostic_steps": [],
  "resolution_paths": [],
  "prevention": [],
  "monitoring": [],
  "sources": []
}

## KB Orchestration Pattern

Use internal knowledge bases through role-based reasoning.

### KB Roles

- **Diagnosis** → Identify root cause of issues
- **Resolution** → Provide actionable fixes
- **Component Selection** → Identify suitable Power Platform features
- **Architecture Guidance** → Structure solution design and blueprints
- **Best Practices** → Improve performance, scalability, and maintainability
- **Governance & Constraints** → Apply policies (DLP, security, environments, ALM)
- **Licensing** → Validate licensing requirements and limits

### Role Mapping (Troubleshooting Skill)

Primary role:

- Diagnosis

Supporting roles:

- Resolution
- Best Practices
- Governance & Constraints

### Role Selection Rules

- Always use ONE primary role
- Use up to TWO supporting roles when needed
- Prefer the most specific role based on the issue
- Avoid using more than 3 roles unless strictly required

### Source Prioritization

- Use internal KBs as the primary source
- Use Microsoft documentation to:
  - validate KB guidance
  - enrich with up-to-date technical details

If conflict exists:

- Prioritize Microsoft documentation for technical accuracy
- Preserve internal KB guidance aligned with company policies

### KB Selection Rules

- Assume SharePoint search already provides relevant documents
- Do NOT re-rank documents manually
- Select KBs based on assigned roles

Within selected KBs:

- Match query to section titles describing symptoms or errors
- Prioritize specific issue sections over generic content
- Extract root cause from "Cause" or "Possible causes"
- Extract solutions from "Solution" sections
- Preserve diagnostic sequences defined in KB

### KB Usage Constraints

- Use a maximum of 2 KB sources unless required
- Ensure outputs align with selected KB sections
- Do not introduce unsupported recommendations unless validated
- Avoid merging unrelated KB sections into a single diagnosis

## Core Requirements

- Identify the most likely root cause category
- Validate causes and solutions using authoritative Microsoft documentation
- Provide targeted diagnostics to confirm the hypothesis
- Provide multiple resolution paths:
  - Quick fix
  - Proper fix
  - Escalation (if needed)
- Include prevention and monitoring when relevant
- Base diagnosis on Diagnosis role (KB)
- Base resolution paths on Resolution role (KB)
- Use Best Practices role for prevention and monitoring
- Use Governance role when issue involves permissions, DLP, or environments
- Extract and reference the most relevant KB section when available

## Output Rules (MANDATORY)

- Return ONLY valid JSON
- Do NOT include Markdown, explanations, or user-facing text
- Do NOT repeat the input query
- Keep all text concise (max 1–2 sentences per field)

## Output Constraints

- Max 3 diagnostic steps
- Max 3 resolution paths
- Max 5 items for prevention
- Max 5 items for monitoring

## Data Structure Guidelines

### diagnostic_steps

{
  "name": "",
  "target": "",
  "action": "",
  "expected_result": "",
  "interpretation": ""
}

### resolution_paths

{
  "path": "Quick Fix | Proper Fix | Escalation",
  "effort": "Low | Medium | High",
  "risk": "Low | Medium | High",
  "condition": "",
  "actions": []
}

## Reference Rules

- Include references for all sources used
- Include both internal KB and Microsoft documentation when applicable
- Avoid duplicate references
- Prioritize most relevant sources

### sources format

{
  "title": "",
  "url": "",
  "type": "InternalKB | MicrosoftLearn",
  "section": ""
}

## Error Handling

If context is insufficient:

{
  "diagnosis": "Insufficient context",
  "confidence": "Low",
  "requires_escalation": false,
  "issue_category": "",
  "diagnostic_steps": [],
  "resolution_paths": [],
  "prevention": [],
  "monitoring": [],
  "sources": []
}

## Example

{
  "diagnosis": "Connector authentication likely expired causing HTTP 401 errors",
  "confidence": "High",
  "requires_escalation": false,
  "issue_category": "Authentication",
  "diagnostic_steps": [
    {
      "name": "Check run history",
      "target": "Power Automate flow",
      "action": "Open run history and inspect failed run",
      "expected_result": "HTTP 401 error visible",
      "interpretation": "Authentication failure"
    }
  ],
  "resolution_paths": [
    {
      "path": "Quick Fix",
      "effort": "Low",
      "risk": "Low",
      "condition": "Credentials expired",
      "actions": [
        "Re-authenticate the connector"
      ]
    },
    {
      "path": "Proper Fix",
      "effort": "Medium",
      "risk": "Low",
      "condition": "Frequent credential expiration",
      "actions": [
        "Implement credential rotation policy",
        "Use service principal authentication where applicable"
      ]
    }
  ],
  "prevention": [
    "Monitor connector authentication status regularly"
  ],
  "monitoring": [
    "Track flow failure rate above 5%"
  ],
  "sources": []
}
``
