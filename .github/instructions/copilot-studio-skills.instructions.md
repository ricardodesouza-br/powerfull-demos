---
applyTo: "Agents/**/Skills/**/*.md"
description: "Authoring rules for Copilot Studio specialist skill instruction files (*-skill.md), skill templates, and the skill registry."
---

# Copilot Studio specialist skill authoring

The authoritative guide is [`Agents/Power Platform Specialist/Skills/README.md`](../../Agents/Power%20Platform%20Specialist/Skills/README.md). These are the non-negotiable rules to apply when writing or editing files here.

## File shape

- Skill files are named `<domain>-skill.md`, lowercase kebab-case, and live directly in `Skills/`.
- Every skill file starts with YAML frontmatter containing exactly `name` and `description`, both double-quoted:

  ```yaml
  ---
  name: "governance-skill"
  description: "Recommends Power Platform governance, security, and monitoring approaches aligned with policies, architecture best practices, and licensing constraints."
  ---
  ```

- `name` must match the filename without `.md`. Do not add `version`, `owner`, `applyTo`, or other fields — that metadata belongs in the registry.
- Use [`Skills/Templates/Skills Master Template.md`](../../Agents/Power%20Platform%20Specialist/Skills/Templates/Skills%20Master%20Template.md) as the structural base. Keep its section order and headings, including the (MANDATORY) suffixes.

## Behavior contract

- A skill is a **reasoning component, not a chat participant**. It must:
  - return **valid JSON only** — no Markdown, no prose, no preamble;
  - never ask follow-up questions, classify intent, or address the user;
  - never restate the coordinator's job (clarification, formatting, synthesis).
- Input contract is always the normalized coordinator payload:

  ```json
  { "query": "", "query_type": "", "add_context": "" }
  ```

- Output contract always includes `confidence` (`High | Medium | Low`), `requires_escalation`, and `sources`. Add domain fields around those.
- `sources` entries use `{ "title": "", "url": "", "type": "InternalKB | MicrosoftLearn", "section": "" }`.

## KB orchestration

- Reason by **role**, never by hard-coded document name. Roles: Diagnosis, Resolution, Component Selection, Architecture Guidance, Best Practices, Governance & Constraints, Licensing.
- Exactly **one primary role**; at most **two supporting roles** (three only if strictly required).
- Internal KBs are primary; Microsoft documentation validates and enriches. On conflict: Microsoft docs win on technical accuracy, internal KB wins on company policy.
- Cap a response at **2–3 KB sources**. Extract sections (Cause, Solution, Guidelines) rather than summarizing whole documents. Do not manually re-rank SharePoint results.
- Map every output field to a role in the `Output Field Mapping` section.

## Constraints

- Keep the whole file under **8,000 characters** (Copilot Studio instruction limit). Trim before adding.
- Limit enumerated lists (recommendations, alternatives, resolution paths) to a maximum of 3 items.
- Define an `Error Handling` fallback for insufficient context using the current template's shape (`confidence: "Low"`, `requires_escalation: true`, missing inputs/assumptions listed).

## Registry

Any new or renamed skill requires a matching entry in [`Skills/Registry/skill-registry.md`](../../Agents/Power%20Platform%20Specialist/Skills/Registry/skill-registry.md) in the **same change**, using the `Skill Entry Template` fields (`skill_name`, `version`, `status`, `primary_role`, `supporting_roles`, `input_contract`, `output_contract`, `test_scenarios`, `last_updated`, `change_log`, …). Register skills under `###` headings.

If the coordinator ([`Agents/Power Platform Specialist/Agents/Power Platform Specialist.md`](../../Agents/Power%20Platform%20Specialist/Agents/Power%20Platform%20Specialist.md)) needs to route to the skill, add the intent and the `<SkillName>.Invoke(query, add_context)` mapping there too.

## Validation before finishing

- Frontmatter valid, `name` matches filename.
- JSON blocks are syntactically valid (a past bug shipped `"add_context: "` with the colon inside the key).
- Character count under 8,000.
- Registry updated; coordinator routing updated if applicable.
- Test scenarios cover: clear scenario, ambiguous scenario, missing context, cross-domain scenario.
