# Power Platform Specialist Demo Architecture

## Purpose and scope

This document describes the architecture used by the **Power Platform Specialist** demo, with focus on how the solution works behind:

- User inputs
- Coordinator-agent instructions
- Specialist-skill instructions
- Knowledge Base (KB) grounding

> **Public demo note:** This architecture is a reference design for study/testing. It is not a production-ready implementation.

## High-level flow

- *User → Coordinator Agent → Specialist Skill → Knowledge Bases → Coordinator → Response*

## End-to-end request lifecycle

1. **User request received**: User submits a question/problem in natural language.
2. **Coordinator analysis**: Coordinator classifies intent and checks if additional context is needed.
3. **Context package creation**: Coordinator structures the request into a normalized payload.
4. **Skill routing**: Coordinator routes to the most relevant specialist skill.
5. **Skill reasoning with KB grounding**: Skill applies instruction logic and consults KB material.
6. **Response synthesis**: Coordinator consolidates skill output into a user-facing response.

## Architecture components

| Component | Responsibility |
| ---------- | ---------------- |
| User Layer | Provides problem statement and follow-up context |
| Coordinator Agent | Intent classification, context gathering, skill orchestration, response synthesis |
| Specialist Skills | Domain-specific reasoning and structured output |
| Knowledge Bases (KBs) | Internal guidance, best practices, and troubleshooting logic |

## Instruction layering model

The design uses layered instructions so behavior stays consistent and extensible:

1. **User instruction layer**: Defines the request objective and business context.
2. **Coordinator instruction layer**: Controls intent classification, routing policy, and response composition.
3. **Specialist skill instruction layer**: Encodes domain reasoning patterns per skill.
4. **KB grounding layer**: Supplies factual/reference material to support skill decisions.

This layering reduces prompt ambiguity and keeps domain logic reusable.

## Coordinator agent design

The **Coordinator Agent** acts as the orchestration layer.

### Responsibilities

- Classify user intent:
  - Solution
  - Troubleshooting
  - Architecture
  - Performance
  - Licensing
- Request additional context when needed
- Prepare a structured context package:

```json
{
  "query": "",
  "query_type": "",
  "add_context": ""
}
```

- Route the request to the appropriate specialist skill
- Synthesize a final, user-friendly response

## Specialist skills design

Specialist skills are domain-focused reasoning units.

### Current skills

| Skill | Purpose |
| --------------- | -------------------------------------------- |
| Troubleshooting | Diagnose issues and provide resolution paths |
| Architecture | Generate solution blueprints |
| Solutioning | Recommend Power Platform components |
| Performance | Improve performance and scalability |
| Licensing | Provide licensing guidance |

For detailed skills architecture, see [`Skills/README.md`](./Skills/README.md).

## Knowledge base (KB) design

The solution uses structured internal documentation as primary grounding.

| Knowledge Base | Purpose |
| ------------------------------------------ | ------------------------------------------------------------ |
| Power Platform Troubleshooting Guide | Diagnose issues and identify causes and solutions |
| Power Platform Best Practices | Provide performance, security, and operational guidance |
| Power Platform Component & Feature Catalog | Describe platform components and capabilities |
| Power Platform Governance Cookbook | Define governance, DLP, security, and environment strategy |
| Power Platform Architecture Guidelines | Guide solution discovery and architecture blueprint creation |

### KB orchestration strategy

Skills use KBs through a role-based reasoning model (not direct document pick-only behavior).

| Role | Purpose |
| ------------------------ | ------------------------------------------------- |
| Diagnosis | Identify root cause |
| Resolution | Provide fixes |
| Component Selection | Choose platform features |
| Architecture Guidance | Structure solutions |
| Best Practices | Improve quality and performance |
| Governance & Constraints | Apply policies (DLP, security, environments, ALM) |
| Licensing | Validate licensing requirements |

For KB and orchestration details, see [`Skills/README.md`](./Skills/README.md).

## Skill authoring and standardization

Skill definitions are standardized with reusable templates and prompts:

- Skill generator prompt:
  - [`Skills/Templates/Skill Generator Prompt.md`](./Skills/Templates/Skill%20Generator%20Prompt.md)
- Master skill structure template:
  - [`Skills/Templates/Skills Master Template.md`](./Skills/Templates/Skills%20Master%20Template.md)
- Skill registry area:
  - [`Skills/Registry/`](./Skills/Registry/)

### Template usage flow

1. Draft a skill using the generator prompt.
2. Normalize structure/content with the master template.
3. Add/update skill artifacts in the skills folder structure.
4. Validate alignment with coordinator routing categories.

## Extensibility model

To add a new specialist skill:

1. Define the new domain intent and expected outputs.
2. Author the skill using the templates above.
3. Add/adjust KB references needed by the new domain.
4. Update coordinator routing logic/categories.
5. Document usage in `Skills/README.md`.

## Boundaries and non-goals

- This demo architecture is for **reference and learning**.
- It does not prescribe production security/compliance implementation.
- Demo-specific hardening, governance, and operations must be defined per project before real-world use.
