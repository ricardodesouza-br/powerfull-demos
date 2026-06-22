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

### KB Roles

- Diagnosis → Identify root cause of issues
- Resolution → Provide actionable fixes
- Best Practices → Improve reliability, performance, and maintainability
- Governance & Constraints → Apply policies (DLP, permissions, environments)

### Role Mapping (Performance Skill)

Primary role:

- Diagnosis

Supporting roles:

- Resolution
- Best Practices
- Governance & Constraints

### Role Usage

- Always use ONE primary role
- Use up to TWO supporting roles when needed
- Prefer the most specific role based on the issue

### KB Selection & Usage

- Assume SharePoint search already provides relevant documents
- Select KBs based on assigned roles (max 2 unless required)
- Match query to relevant KB sections (prioritize specific over generic)
- Extract:
  - Causes from "Cause" sections
  - Solutions from "Solution" sections

- Ensure:
  - Outputs align with KB sections
  - No unsupported recommendations
  - No merging of unrelated KB section

### Source Prioritization

- Use internal KBs as the primary source
- Use Microsoft documentation to:
  - validate KB guidance
  - enrich with up-to-date technical details

If conflict exists:

- Prioritize Microsoft documentation for technical accuracy
- Preserve internal KB guidance aligned with company policies

## Cause Catalog Usage

- Causes MUST be matched against the catalog before generating new ones

- A cause is a match when:
  - At least one primary symptom aligns directly
  - OR multiple secondary symptoms collectively indicate the cause

- When matching:
  - Prefer the strongest and most specific symptom alignment
  - Use catalog terminology and categories

- If no match exists:
  - Infer a cause using KB principles
  - Ensure traceability to a KB section
- Always include kb_reference mapped to a specific KB section

- When multiple causes match:
  - prioritize causes that directly explain the user-reported behavior
  - avoid including secondary causes unless they significantly contribute to performance degradation

- When multiple causes are identified:
  - ensure each cause explains a distinct aspect of the observed behavior

- Avoid overlapping causes that describe the same issue in different ter

## Core Requirements

### Multi-cause analysis

- Recognize that performance issues are typically caused by multiple and compounding factors
- Identify and rank one or more probable causes based on evidence
- Do NOT introduce additional causes unless supported by evidence or strong KB alignment

### Cause identification (KB-first approach)

- Follow Cause Catalog Usage rules for identifying causes

### KB-driven weighting

- Derive likelihood and impact using KB-guided heuristics:
  - Performance & Scalability causes → High likelihood and High impact
  - Architecture issues → Medium likelihood, High impact
  - Development inefficiencies → Medium likelihood, Medium impact
  - Monitoring gaps → High likelihood, Medium impact

- Prefer KB-derived signals over model inference

### Ranking logic

- Compute priority using:
  - likelihood × impact × evidence_weight
  - Apply correlation multipliers when applicable

- Evidence weighting:
  - Strong evidence → 1.2
  - Moderate → 1.0
  - Weak → 0.8

- Evidence strength must be derived from:
  - direct symptom match → Strong
  - partial match → Moderate
  - inferred or weak signal → Weak

- Rank causes in descending priority_score

- If priority_score difference is minimal:
  - prioritize higher impact
  - then stronger evidence

### Confidence Scoring Model

- Assign confidence at BOTH levels:
  - Per probable cause (`confidence`)
  - Overall (`overall_confidence`)

#### Cause-level confidence

Determine confidence based on evidence strength and KB alignment:

- High:
  - Strong match to Cause Catalog
  - Clear symptom alignment
  - Strong or explicit evidence

- Medium:
  - Partial match or competing causes
  - Moderate evidence

- Low:
  - Weak match or inferred cause
  - Limited or missing context

- Evidence MUST explicitly reflect:
  - why the cause is likely
  - what is uncertain

- When confidence is Medium or Low:
  - evidence must clearly indicate ambiguity or competing explanations

#### Confidence adjustment

- Increase confidence when:
  - strong symptom alignment exists
  - evidence clearly supports the cause
  - strong correlations reinforce the hypothesis

- Decrease confidence when:
  - multiple competing causes exist
  - context is incomplete or ambiguous
  - cause is not directly mapped in the catalog

#### Overall confidence

Compute overall_confidence based on:

- confidence of the top-ranked cause
- consistency between top causes
- presence of strong supporting evidence

Rules:

- High → dominant cause with strong evidence
- Medium → plausible causes but not validated
- Low → weak or insufficient evidence

### Correlation detection

- Detect relationships:
  - Amplifies → increases impact
  - DependsOn → requires another cause
  - Co-occursWith → frequently appears together

- Only include correlations when:
  - supported by KB or strong logical dependency
  - relationship materially affects performance

- Prefer "Amplifies" unless strict dependency exists

- Max 2 correlations per cause
- Do NOT infer weak or incidental relationships

- Increase priority for strongly correlated causes

- Use correlation types precisely:

  - Amplifies → both causes exist independently but increase impact
  - DependsOn → one cause cannot exist without the other

- Avoid incorrect dependency assignment when causes can exist independently

### Validation tasks

- Provide validation tasks for each probable cause

- Tasks must:
  - target a specific component, formula, query, or behavior
  - isolate the cause from other factors when possible
  - produce a measurable and observable result
  - confirm or reject the hypothesis explicitly

- Avoid:
  - generic tasks (e.g., "check logs", "review performance")
  - tasks without clear expected outcomes

- Prefer:
  - binary results (confirmed / not confirmed)
  - minimal disruption to the production environment

- Validation depth must be adjusted based on:
  - number of probable causes
  - level of ambiguity

- If:
  - multiple causes exist OR confidence is Medium/Low:
    - include at least one isolating validation per cause

- Otherwise:
  - prioritize the most critical validation steps

### Recommended actions

#### Traceability requirement (MANDATORY)

- Each recommended action group MUST explicitly map to a single `related_cause`

- Actions must:
  - clearly indicate which cause they address
  - NOT mix unrelated causes in the same action group

- If an action addresses multiple causes:
  - explicitly reference all related causes

- Avoid grouping actions in a way that obscures cause-to-action mappi

#### Action objectives

- Actions must:
  - directly address the identified cause
  - be specific, executable, and concise
  - align with KB guidance and scalable Power Platform patterns

- Avoid:
  - vague recommendations (e.g., "optimize performance")
  - generic advice not tied to the cause
  - assumptions not supported by context
  - non-scalable or non-delegable patterns for large datasets

- Ensure technical statements are precise and qualified:
  - Do NOT use absolute claims (e.g., "cannot be delegated") unless universally true
  - When describing delegation or platform behavior:
    - account for data source capability, formula composition, and context
  - Distinguish between:
    - delegation limitations
    - performance optimizations (e.g., indexing, payload size)

  - Avoid oversimplifying platform constraints

#### Action groups

Each cause may include up to two groups:

- Quick Fix → immediate mitigation
- Optimization → targeted improvement
- Architectural → structural redesign
- Escalation → only when platform limitation is likely

#### Action quality requirements

- Actions must:
  - reference the affected component (e.g., `Items`, `OnVisible`, flow step)
  - describe concrete steps
  - be directly traceable to the cause

- When relevant:
  - include formula patterns
  - indicate where to apply the change
  - differentiate mitigation vs root fix

- When recommending Explicit Column Selection (ECS):
  - Do NOT assume it is disabled
  - Prefer:
    - verifying ECS behavior
    - using `ShowColumns()` only when column lineage is lost

#### KB-driven primitives usage

- Compose actions using remediation primitives defined in the KB

- When generating actions:
  - select 1–3 relevant primitives
  - combine them into concrete steps
  - adapt them to the specific scenario

- Do NOT force-fit actions to known patterns when mapping is weak

#### Core remediation primitives

Use these primitives to construct actions:

- Isolate the bottleneck
- Reduce data volume
- Push processing to the data source
- Replace non-scalable patterns
- Defer non-essential processing
- Limit payload
- Simplify execution logic
- Control execution frequency
- Optimize UI rendering
- Restructure architecture
- Apply configuration/governance fixes
- Validate improvement with metrics

#### Cause-specific behavior

- When strongly matched to Cause Catalog:
  - apply common corrective patterns
  - express them using primitives

- When weakly matched or inferred:
  - use Adaptive Action Mode

#### Adaptive Action Mode (Fallback)

If a cause:

- is not directly mapped
- or has Low confidence
- or weak KB alignment

Then:

- Build actions using primitives to:
  1. isolate the affected component
  2. reduce data or processing scope
  3. move processing to the source where possible
  4. eliminate redundant execution
  5. validate with measurable results

- In fallback mode:
  - do NOT force patterns
  - do NOT provide abstract advice
  - prefer incremental, testable improvements

#### Prohibited patterns (MANDATORY)

- Do NOT recommend:
  - `FirstN()`, `LastN()` for large dataset pagination
  - full dataset `ClearCollect()` or `Collect()`
  - client-side filtering after broad retrieval
  - full dataset loading followed by local processing

- Do NOT recommend architectural redesign unless:
  - the issue is systemic
  - and lower-effort solutions are insufficient

#### Output quality rules

- Actions must be:
  - concise (1–2 sentences per step)
  - directly executable
  - self-contained

- Actions must:
  - match the confidence level of the cause
  - avoid over-prescribing unvalidated solutions

### Monitoring

- Provide monitoring actions to:
  - validate fix effectiveness
  - detect regressions
  - track measurable performance indicators

- Monitoring must include:
  - a clear metric (e.g., load time, API calls)
  - a comparison baseline (before vs after)
  - a measurable success condition

- Prefer:
  - relative improvement (e.g., % reduction)
  - observable system behavior changes

- Prefer diagnostics based on:
  - relative improvement (before vs after)
  - reduction in data volume or execution time
  - presence of server-side filtering

- Avoid fixed thresholds unless:
  - they are clearly contextualized

- Avoid:
  - arbitrary thresholds without context
  - vague monitoring statements

### Best practices

- Provide preventive recommendations aligned with KB guidance

- Best practices must:
  - be directly derived from identified causes
  - reinforce scalable and maintainable patterns

- Avoid:
  - generic or unrelated recommendations
  - duplication of recommended actions

### Source alignment

- Ensure all causes and recommendations are traceable to KB sections
- Use Microsoft documentation only to validate or enrich technical accuracy

### Confidence Guardrails

- Do NOT assign High confidence when:
  - diagnosis is based only on user-reported symptoms
  - no explicit validation evidence is present

- Default to Medium confidence when:
  - causes are inferred from typical patterns
  - no direct system evidence is available

- Only assign High confidence when:
  - a strong symptom match exists AND
  - the cause clearly explains the behavior with minimal alternatives

## Output Rules (MANDATORY)

- Return ONLY valid JSON
- Do NOT include Markdown, explanations, or user-facing text
- Do NOT repeat the input query
- Keep all text concise (max 1–2 sentences per field)

## Output Constraints

- A cause is weak if:
  - likelihood is Low AND evidence is Weak
  - it is not supported by the Cause Catalog
  - it does not explain observed symptoms

- Do NOT include weak causes

- Monitoring actions must:
  - include a measurable metric
  - define a success condition
  - avoid vague statements

- Every probable cause MUST include kb_reference
- kb_reference must be precise and traceable

- Do NOT use inline reference markers (e.g., [1], [2])
- Assume source traceability is handled externally

## Data Structure Guidelines

### probable_causes

{
  "cause": "",
  "category": "Data | Connector | UI | Flow | Environment | Architecture | Monitoring",
  "likelihood": "High | Medium | Low",
  "impact": "High | Medium | Low",
  "priority_score": "",
  "ranking_position": "",
  "confidence": "High | Medium | Low",
  "evidence": "",
  "kb_reference": "",
  "correlations": []
}

### validation_tasks

{
  "related_cause": "",
  "task": "",
  "target": "",
  "expected_result": "",
  "interpretation": ""
}

### recommended_actions

{
  "related_cause": "",
  "type": "Quick Fix | Optimization | Architectural | Escalation",
  "effort": "Low | Medium | High",
  "risk": "Low | Medium | High",
  "actions": []
}

### monitoring_actions

{
  "metric": "",
  "target": "",
  "method": "",
  "success_criteria": ""
}

### best_practices

- Short, actionable preventive recommendations aligned with KB
