
# Copilot Studio Skill Authoring Guide

## Overview

This repository contains the **standardized approach for creating and maintaining specialist skills** used by Copilot Studio agents in Power Platform scenarios.

Skills are **domain-specific reasoning components** that:

- Analyze structured input from a Coordinator agent
- Use internal Knowledge Bases (KBs)
- Return **structured JSON outputs**
- Enable the Coordinator to generate high-quality, user-friendly responses

## Architecture Model

The solution follows a **layered architecture**

- *User → Coordinator Agent → Specialist Skill → Knowledge Bases → Coordinator → Response*

### Responsibilities

| Component | Responsibility |
| ---------- | ---------------- |
| Coordinator Agent | Intent classification, context gathering, skill routing, response synthesis |
| Specialist Skills | Domain reasoning and structured output |
| Knowledge Bases (KBs) | Source of truth (Troubleshooting, Best Practices, Governance, etc.) |

## Skill Authoring

Skills must follow the standards defined in:

- Skills Master Template.md
- Copilot Studio Skill Authoring Guide.md

These documents define:

- Required structure
- KB orchestration model
- Output contracts
- Best practices
- Validation rules

## Skill Registry

The Skill Registry is used as a governance artifact to manage skills lifecycle and consistency.
Purpose

- Track skill metadata (name, version, owner)
- Define KB role mappings
- Maintain input/output contracts
- Document test scenarios and validation
- Support versioning and change tracking

### Usage

The Skill Registry is:

- NOT used at runtime by the agent
- Used by architects for:
  - Design
  - Validation
  - Maintenance
  - Governance

## Skill Design Principles

All skills must follow these core principles:

### 1. Single Responsibility

- One skill per request (by default)
- Single responsibility (domain-specific)
- JSON-first structured output
- No user-facing formatting or conversational behavior
- Powered by internal Knowledge Bases and Microsoft documentation

### 2. One Skill per Request

The Coordinator should typically call **one skill per request**, ensuring:

- Focused reasoning
- Higher accuracy
- Reduced hallucination

### 3. Structured Output (JSON-first)

Skills must return:

- **Machine-readable JSON**
- No user-facing formatting
- No Markdown or explanations

The **Coordinator is responsible** for:

- Formatting
- Explanations
- User interaction

### 4. KB-Driven Reasoning

Skills must:

- Prefer **internal KBs**
- Use **Microsoft documentation for validation**
- Extract knowledge using structured sections (e.g., Cause, Solution)

## KB Orchestration Model

### KB Roles

All skills use a shared set of **KB roles**:

| Role | Purpose |
| ----- | -------- |
| Diagnosis | Identify root cause |
| Resolution | Provide fixes |
| Component Selection | Choose platform features |
| Architecture Guidance | Structure solution design |
| Best Practices | Improve quality and performance |
| Governance & Constraints | Apply policies (DLP, environments, security) |
| Licensing | Validate license requirements |

### Role Mapping (Per Skill)

Each skill must define:

- ✅ **Primary Role (mandatory, 1 only)**
- ✅ **Supporting Roles (max 2–3)**

#### Example: Troubleshooting Skill

Primary Role:

Diagnosis

Supporting Roles:

- Resolution
- Best Practices
- Governance & Constraints

### Source Prioritization

- Internal KB → **Primary source**
- Microsoft Learn → **Validation & enrichment**

If conflict exists:

- Prioritize Microsoft documentation for technical accuracy
- Preserve internal policies where applicable

### KB Selection Rules

- Do NOT re-rank SharePoint search results
- Select documents based on role relevance
- Extract relevant **sections**, not entire documents
- Prefer:
  - Specific scenarios (e.g., "Flow Runs Failing")
  - Structured sections (Cause, Solution)

Avoid:

- Generic sections (Overview, Introduction)

## Standard Skill Structure

### Metadata

```markdown
### name: "<skill-name>"
description: "<short description>"
```

### Purpose

Clear description of what the skill does
1–2 sentences only

### Input Contract

```json
{
  "query": "",
  "query_type": "",
  "add_context": ""
}
```

### Output Contract (MANDATORY)

```json
{
  "confidence": "High | Medium | Low",
  "requires_escalation": false,
  "sources": []
}
```

### KB Orchestration Pattern

Include:

- KB roles
- Role mapping
- Selection rules
- Usage constraints

### Core Requirements

Define:

- What the skill must produce
- How roles influence output
- Validation expectations

### Output Field Mapping

Map fields to roles. Example:

- diagnosis → Diagnosis role
- resolution_paths → Resolution role
- prevention → Best Practices role
- monitoring → Governance role

### Confidence Guidelines

High → Strong KB match + validated
Medium → Partial KB match
Low → Weak KB match or ambiguity

### Output Rules

- Return ONLY JSON
- No explanations
- No Markdown
- No conversational text

### Output Constraints

- Max 3 items per list
- Keep responses concise
- Use structured objects (not paragraphs)

### Reference Rules

Structured in sources only:

```json
{
  "title": "",
  "url": "",
  "type": "InternalKB | MicrosoftLearn",
  "section": ""
}
```

Do NOT use:

- Inline references
- Citation markers ([1], [2])

### Error Handling

If context is insufficient:

```json
{
  "confidence": "Low",
  "requires_escalation": false,
  "sources": []
}
```

## Best Practices

### ✅ Use Role-Based Reasoning

- Always reason using KB roles, not KB names.

### ✅ Keep Prompts Lean

Due to Copilot Studio instruction limits:

- Avoid verbose explanations
- Avoid step-by-step procedural logic
- Prefer compact directives

### ✅ Prefer Section-Level Extraction

Use:

- Cause → Diagnosis
- Solution → Resolution

Avoid generic document summarization.

### ✅ Limit KB Usage

- Maximum 2–3 KBs per response
- Avoid mixing unrelated KB domains

### ✅ Separate Reasoning and Communication

- Skill → structured reasoning
- Coordinator → formatted response

### ✅ Define Determinism

Always include:

- Confidence rules
- Output constraints
- Field-role mapping

## Validation Checklist (Before Publishing)

### Prompt Design

- Purpose is clear
- Input/output contracts defined
- JSON-only output enforced

### KB Orchestration

- Primary role defined
- Supporting roles ≤ 3
- Roles aligned with skill purpose

### Source Behavior

- Internal KB prioritized
- External validation defined
- Section selection rules present

### Determinism

- Confidence rules defined
- Output constraints enforced
- Field-role mapping defined

### Copilot Studio Compatibility

- Under 8K instruction limit
- No conversational logic
- No UI formatting instructions

## Testing Guidelines

Each skill must be tested with:

- Clear Scenario → Expect High confidence
- Ambiguous Scenario → Expect Medium/Low confidence
- Missing Context → Expect safe fallback output
- Cross-Domain Scenario → Validate supporting role usage

## Skill Registry Integration

All skills must have a corresponding Skill Registry entry, including:

- Version
- Owner
- Status
- Role mapping
- KB mapping
- Test scenarios
- Change log

The Skill Registry is used for:

- Governance
- Versioning
- Testing
- Maintenance

## Templates

The following templates are stored on this folder:

- **Skill Generator Prompt**: Can accelerate the creation of new skills using standardized instructions.
- **Skills Master Template**: Template instructions for new skills.

## Final Notes

This framework enables:

- Scalable skill creation
- High-quality reasoning
- Consistent architecture
- Maintainable Copilot systems

Follow this guide for all new skills to ensure consistency across the solution.
