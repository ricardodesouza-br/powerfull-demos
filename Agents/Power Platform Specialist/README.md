# Power Platform Specialist Copilot

## Overview

This repository contains the implementation and standards for the **Power Platform Specialist Copilot**, a Copilot Studio–based solution designed to support internal users with:

- Troubleshooting Power Platform issues
- Designing architecture solutions
- Recommending platform components
- Optimizing performance
- Understanding licensing considerations

The solution is built using a **Coordinator Agent + Specialist Skills architecture**, where each skill provides domain-specific reasoning supported by structured internal Knowledge Bases (KBs).

## Architecture

### High-Level Flow

- *User → Coordinator Agent → Specialist Skill → Knowledge Bases → Coordinator → Response*

### Components

| Component | Responsibility |
| ---------- | ---------------- |
| Coordinator Agent | Intent classification, context gathering, skill orchestration, response synthesis |
| Specialist Skills | Domain-specific reasoning and structured output |
| Knowledge Bases (KBs) | Internal guidance, best practices, and troubleshooting logic |

## Coordinator Agent

The **Coordinator Agent** acts as the orchestration layer of the solution.

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

## Specialist Skills

Specialist skills are domain-focused reasoning engines.

### Current Skills

| Skill           | Purpose                                      |
| --------------- | -------------------------------------------- |
| Troubleshooting | Diagnose issues and provide resolution paths |
| Architecture    | Generate solution blueprints                 |
| Solutioning     | Recommend Power Platform components          |
| Performance     | Improve performance and scalability          |
| Licensing       | Provide licensing guidance                   |

For detailed instructions about skills architecture see **skills/README.md**.

## Knowledge Bases (KBs)

The solution uses internal structured documentation as its primary knowledge source.

| Knowledge Base                             | Purpose                                                      |
| ------------------------------------------ | ------------------------------------------------------------ |
| Power Platform Troubleshooting Guide       | Diagnose issues and identify causes and solutions            |
| Power Platform Best Practices              | Provide performance, security, and operational guidance      |
| Power Platform Component & Feature Catalog | Describe platform components and capabilities                |
| Power Platform Governance Cookbook         | Define governance, DLP, security, and environment strategy   |
| Power Platform Architecture Guidelines     | Guide solution discovery and architecture blueprint creation |

### KB Orchestration Strategy

Skills use KBs through a role-based reasoning model, rather than direct document selection.

| Role                     | Purpose                                           |
| ------------------------ | ------------------------------------------------- |
| Diagnosis                | Identify root cause                               |
| Resolution               | Provide fixes                                     |
| Component Selection      | Choose platform features                          |
| Architecture Guidance    | Structure solutions                               |
| Best Practices           | Improve quality and performance                   |
| Governance & Constraints | Apply policies (DLP, security, environments, ALM) |
| Licensing                | Validate licensing requirements                   |

For detailed instructions about KB architecture and orchestration see **skills/README.md**.

## Limitations

Information not available.

## Deployment

Information not available.

## Security and Compliance

Information not available.

## Contribution Guidelines

Information not available.

## License

Information not available.
