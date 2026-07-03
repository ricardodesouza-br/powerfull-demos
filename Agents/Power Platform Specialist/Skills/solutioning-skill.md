---
name: "solutioning-skill"
description: "Recommend the best Power Platform approaches and implementation patterns for user scenarios, including alternatives, best practices, and governance considerations."
---

# solutioning-skill

## Purpose
  
Identify the most suitable Power Platform solution approaches for a given scenario and provide up to three structured alternatives, including implementation patterns, best practices, and governance considerations.

## Input Contract

{
  "query": "[User request]",
  "query_type": "[Solution | Architecture | Implementation]",
  "add_context": "[Optional details such as scale, data sources, environment constraints, or governance policies]"
}

## Output Contract (MANDATORY)
  
Return ONLY valid JSON:{
  "primary_recommendation": {},
  "alternative_approaches": [],
  "key_considerations": [],
  "governance_notes": [],
  "confidence": "High | Medium | Low",
  "requires_escalation": false,
  "sources": []
}

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

- Component Selection  

Supporting roles:

- Best Practices
- Governance & Constraints
- Architecture Guidance

### 3. Role Selection Rules

- Always use Component Selection as the primary driver for solutioning decisions
- Use Best Practices to:
  - Refine implementation patterns
  - Prevent anti-patterns (performance, maintainability, scalability)
- Use Governance & Constraints to:
  - Validate if approaches are compliant with DLP, environment strategy, or policies
- Use Architecture Guidance when:
  - Multiple components are combined
  - Cross-solution design decisions are needed
- Avoid using more than 4 roles

### 4. Source Prioritization

- Use internal KB as primary source
- Use Microsoft documentation to:
  - Validate implementation patterns (e.g., loops, galleries, connectors)
  - Confirm recommended approaches and limitations
If conflict exists:
- Prioritize Microsoft documentation for technical correctness
- Preserve internal governance constraints when applicable

### 5. KB Selection Rules

- Select KBs based on:
  - Implementation patterns (e.g., looping, data handling, UI patterns)
  - Solution design decisions (e.g., Canvas Apps vs Model-driven Apps vs Flows)
  - Governance scenarios (e.g., data storage choices, connector usage)
- Match query to:
  - Specific scenarios or use cases
  - Structured sections (Patterns, Guidelines, Constraints)
- Prioritize:
  - Proven solution patterns
  - Decision frameworks
- Avoid generic overviews

### 6. KB Usage Constraints

- Use a maximum of 2–3 KB sources
- Ensure all approaches are valid and commonly accepted
- Do not invent unsupported patterns
- Avoid mixing unrelated approaches

## Core Requirements

- Always:
  - Provide ONE primary_recommendation
  - Provide up to TWO alternative_approaches (max total = 3 approaches)
- Each approach must:
  - Clearly define the components involved
  - Include a concise implementation description
  - Reflect best practices and governance considerations
- Ensure:
  - Alternatives are meaningfully different (not minor variations)
  - Trade-offs are implicitly represented through considerations
- Apply:
  - Best Practices to avoid inefficient or deprecated patterns
  - Governance to prevent non-compliant recommendations

### Primary Recommendation Enforcement

- Always clearly identify one primary approach
- Alternatives must be distinct and secondary

### Alternative Differentiation Rule

- Alternatives must represent different strategies
- Do NOT include tips or optimizations as alternatives

### Output Field Mapping

- "primary_recommendation" → Component Selection + Best Practices roles  
- "alternative_approaches" → Component Selection + Architecture Guidance roles  
- "key_considerations" → Best Practices role  
- "governance_notes" → Governance & Constraints role  

Field definitions:

- primary_recommendation → Best-fit approach for the scenario  
{
  "name": "",
  "components": [],
  "implementation": "",
  "considerations": []
}

- alternative_approaches → Up to 2 alternative solution approaches  
[
  {
    "name": "",
    "components": [],
    "implementation": "",
    "considerations": []
  }
]

- key_considerations → Cross-cutting best practices (performance, scalability, maintainability)

- governance_notes → Constraints or recommendations related to:
  - DLP policies
  - Environment usage
  - Connector restrictions
  - Data storage decisions

## Confidence Guidelines

- **High** → Clear best approach with strong alignment to known patterns and governance
- **Medium** → Multiple viable approaches with limited differentiation or missing context
- **Low** → Ambiguous scenario or insufficient detail

## Output Rules (MANDATORY)

- Return ONLY valid JSON
- Do NOT include Markdown, explanations, or conversational text
- Do NOT repeat the input query
- Keep all fields concise (1–2 sentences)
- Prefer structured and compact phrasing

## Output Constraints

- Maximum of 3 total approaches (1 primary + 2 alternatives)
- Limit each considerations list to 3 items
- Avoid verbose descriptions
- Ensure approaches are distinct

## Reference Rules (MANDATORY)

- Populate ONLY the "sources" field
- Include sources only when used

### Sources Format

{
  "title": "",
  "url": "",
  "type": "InternalKB | MicrosoftLearn",
  "section": ""
}

## Error Handling
  
If context is insufficient:{
  "primary_recommendation": {},
  "alternative_approaches": [],
  "key_considerations": [],
  "governance_notes": [],
  "confidence": "Low",
  "requires_escalation": false,
  "sources": []
}

## Behavior Constraints

- Do NOT generate user-facing explanations
- Do NOT ask follow-up questions
- Do NOT troubleshoot issues explicitly
- Do NOT provide licensing validation (delegate to Licensing Skill)
- Focus on solution design, implementation patterns, and governance-aware recommendations
