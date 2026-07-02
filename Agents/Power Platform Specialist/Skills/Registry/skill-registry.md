# Skill Registry

## Purpose

This registry tracks all skills in `Skills/` and standardizes ownership, intent mapping, KB usage, contracts, validation, and lifecycle status.

## Skill Entry Template

- skill_name:
- display_name:
- purpose:
- owner:
- version:
- status: Draft | Test | Active | Deprecated
- intent_supported:
- requires_coordinator: true
- primary_role:
- supporting_roles:
- primary_kb:
- supporting_kbs:
- kb_usage_rules:
  - SharePoint ranks files; do not manually re-rank all KBs
  - Select KB by role relevance
  - Select the most relevant section within the KB
  - Prefer specific sections over generic sections
  - Validate internal KB guidance with Microsoft documentation when needed
- input_contract:
  {
    "query": "",
    "query_type": "",
    "add_context": ""
  }
- output_contract:
  {
    "confidence": "High | Medium | Low",
    "requires_escalation": false,
    "sources": []
  }
- confidence_guidelines:
  - High: strong primary KB match + validated
  - Medium: partial primary KB match or supporting-role reliance
  - Low: weak KB match, ambiguity, or insufficient context
- escalation_supported:
- output_format: JSON
- output_constraints:
  - no markdown
  - no narrative text
  - concise structured fields only
- validation_checklist:
  - purpose defined
  - role mapping reviewed
  - KB mappings reviewed
  - output contract reviewed
  - confidence logic reviewed
  - test scenarios executed
- test_scenarios:
  - clear scenario
  - ambiguous scenario
  - missing context
  - edge case
- last_updated:
- change_log:
- notes:

## Registered Skills

### troubleshooting-skill

- skill_name: troubleshooting-skill
- display_name: Troubleshooting Skill
- purpose: Diagnose Power Platform issues and provide structured resolution paths.
- owner: Power Platform Specialist Team
- version: 1.0.0
- status: Active
- intent_supported:
  - Troubleshooting
- requires_coordinator: true
- primary_role: Diagnosis
- supporting_roles:
  - Resolution
  - Best Practices
  - Governance & Constraints
- primary_kb: Power Platform Troubleshooting Guide
- supporting_kbs:
  - Power Platform Best Practices
  - Power Platform Governance Cookbook
- kb_usage_rules:
  - SharePoint ranks files; do not manually re-rank all KBs
  - Select KB by role relevance
  - Select the most relevant section within the KB
  - Prefer specific sections over generic sections
  - Validate internal KB guidance with Microsoft documentation when needed
- input_contract:
  {
    "query": "",
    "query_type": "Troubleshooting",
    "add_context": ""
  }
- output_contract:
  {
    "confidence": "High | Medium | Low",
    "requires_escalation": false,
    "sources": []
  }
- confidence_guidelines:
  - High: strong primary KB match + validated
  - Medium: partial primary KB match or supporting-role reliance
  - Low: weak KB match, ambiguity, or insufficient context
- escalation_supported: true
- output_format: JSON
- output_constraints:
  - no markdown
  - no narrative text
  - concise structured fields only
- validation_checklist:
  - purpose defined
  - role mapping reviewed
  - KB mappings reviewed
  - output contract reviewed
  - confidence logic reviewed
  - test scenarios executed
- test_scenarios:
  - clear scenario
  - ambiguous scenario
  - missing context
  - edge case
- last_updated: 2026-07-02
- change_log:
  - 2026-07-02: Initial registry entry created.
- notes: Aligned with coordinator routing and role-based KB orchestration.

### solutioning-skill

- skill_name: solutioning-skill
- display_name: Solutioning Skill
- purpose: Recommend Power Platform components based on business and technical requirements.
- owner: Power Platform Specialist Team
- version: 1.0.0
- status: Active
- intent_supported:
  - Solution
- requires_coordinator: true
- primary_role: Component Selection
- supporting_roles:
  - Architecture Guidance
  - Governance & Constraints
  - Licensing
- primary_kb: Power Platform Component & Feature Catalog
- supporting_kbs:
  - Power Platform Governance Cookbook
  - Power Platform Architecture Guidelines
- kb_usage_rules:
  - SharePoint ranks files; do not manually re-rank all KBs
  - Select KB by role relevance
  - Select the most relevant section within the KB
  - Prefer specific sections over generic sections
  - Validate internal KB guidance with Microsoft documentation when needed
- input_contract:
  {
    "query": "",
    "query_type": "Solution",
    "add_context": ""
  }
- output_contract:
  {
    "confidence": "High | Medium | Low",
    "requires_escalation": false,
    "sources": []
  }
- confidence_guidelines:
  - High: strong primary KB match + validated
  - Medium: partial primary KB match or supporting-role reliance
  - Low: weak KB match, ambiguity, or insufficient context
- escalation_supported: true
- output_format: JSON
- output_constraints:
  - no markdown
  - no narrative text
  - concise structured fields only
- validation_checklist:
  - purpose defined
  - role mapping reviewed
  - KB mappings reviewed
  - output contract reviewed
  - confidence logic reviewed
  - test scenarios executed
- test_scenarios:
  - clear scenario
  - ambiguous scenario
  - missing context
  - edge case
- last_updated: 2026-07-02
- change_log:
  - 2026-07-02: Initial registry entry created.
- notes: Focuses on capability matching, not implementation deployment.

### performance-skill

- skill_name: performance-skill
- display_name: Performance Skill
- purpose: Identify and recommend performance and scalability improvements for Power Platform solutions.
- owner: Power Platform Specialist Team
- version: 1.0.0
- status: Active
- intent_supported:
  - Performance
- requires_coordinator: true
- primary_role: Best Practices
- supporting_roles:
  - Diagnosis
  - Architecture Guidance
  - Governance & Constraints
- primary_kb: Power Platform Best Practices
- supporting_kbs:
  - Power Platform Troubleshooting Guide
  - Power Platform Architecture Guidelines
- kb_usage_rules:
  - SharePoint ranks files; do not manually re-rank all KBs
  - Select KB by role relevance
  - Select the most relevant section within the KB
  - Prefer specific sections over generic sections
  - Validate internal KB guidance with Microsoft documentation when needed
- input_contract:
  {
    "query": "",
    "query_type": "Performance",
    "add_context": ""
  }
- output_contract:
  {
    "confidence": "High | Medium | Low",
    "requires_escalation": false,
    "sources": []
  }
- confidence_guidelines:
  - High: strong primary KB match + validated
  - Medium: partial primary KB match or supporting-role reliance
  - Low: weak KB match, ambiguity, or insufficient context
- escalation_supported: true
- output_format: JSON
- output_constraints:
  - no markdown
  - no narrative text
  - concise structured fields only
- validation_checklist:
  - purpose defined
  - role mapping reviewed
  - KB mappings reviewed
  - output contract reviewed
  - confidence logic reviewed
  - test scenarios executed
- test_scenarios:
  - clear scenario
  - ambiguous scenario
  - missing context
  - edge case
- last_updated: 2026-07-02
- change_log:
  - 2026-07-02: Initial registry entry created.
- notes: Includes optimization guidance with governance-aware constraints.

## licensing-skill

- skill_name: licensing-skill
- display_name: Licensing Skill
- purpose: Provide licensing guidance and validate licensing constraints for proposed solutions.
- owner: Power Platform Specialist Team
- version: 1.0.0
- status: Active
- intent_supported:
  - Licensing
- requires_coordinator: true
- primary_role: Licensing
- supporting_roles:
  - Component Selection
  - Governance & Constraints
- primary_kb: Power Platform Component & Feature Catalog
- supporting_kbs:
  - Power Platform Governance Cookbook
- kb_usage_rules:
  - SharePoint ranks files; do not manually re-rank all KBs
  - Select KB by role relevance
  - Select the most relevant section within the KB
  - Prefer specific sections over generic sections
  - Validate internal KB guidance with Microsoft documentation when needed
- input_contract:
  {
    "query": "",
    "query_type": "Licensing",
    "add_context": ""
  }
- output_contract:
  {
    "confidence": "High | Medium | Low",
    "requires_escalation": false,
    "sources": []
  }
- confidence_guidelines:
  - High: strong primary KB match + validated
  - Medium: partial primary KB match or supporting-role reliance
  - Low: weak KB match, ambiguity, or insufficient context
- escalation_supported: true
- output_format: JSON
- output_constraints:
  - no markdown
  - no narrative text
  - concise structured fields only
- validation_checklist:
  - purpose defined
  - role mapping reviewed
  - KB mappings reviewed
  - output contract reviewed
  - confidence logic reviewed
  - test scenarios executed
- test_scenarios:
  - clear scenario
  - ambiguous scenario
  - missing context
  - edge case
- last_updated: 2026-07-02
- change_log:
  - 2026-07-02: Initial registry entry created.
- notes: Responses should highlight uncertainty when licensing context is incomplete.
