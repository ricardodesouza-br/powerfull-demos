---
name: new-specialist-skill
description: "Create or update a Copilot Studio specialist skill for a Power Platform Specialist style agent. Use when asked to add a new skill, author a skill file, generate a *-skill.md, define KB role mapping, design a skill output contract, or register a skill in the skill registry."
---

# New specialist skill

Authors a production-ready specialist skill instruction file for the **Coordinator Agent + Specialist Skills** architecture, and wires it into the registry and coordinator.

## Reference material (read before writing)

| File | Why |
| --- | --- |
| `Agents/Power Platform Specialist/Skills/README.md` | Authoritative authoring guide, design principles, validation checklist |
| `Agents/Power Platform Specialist/Skills/Templates/Skill Master Template.md` | Current structural template — copy its headings and order |
| `Agents/Power Platform Specialist/Skills/Templates/Skill Generator Prompt.md` | The interview checklist this skill automates |
| `Agents/Power Platform Specialist/Skills/governance-skill.md` | Best worked example (custom output object shapes) |
| `Agents/Power Platform Specialist/Skills/Registry/skill-registry.md` | Entry template + existing entries |
| `Agents/Power Platform Specialist/ARCHITECTURE.md` | Layering model and extensibility rules |

Also apply `.github/instructions/copilot-studio-skills.instructions.md`.

## Step 1 — Gather inputs

Ask the user (use the ask-questions tool if available) for anything not already supplied. Do not guess:

1. **Skill name** — lowercase kebab-case, ending in `-skill`.
2. **Description** — one sentence, goes in frontmatter.
3. **Purpose** — 1–2 sentences.
4. **Supported intent** — one of: Solution, Troubleshooting, Architecture, Performance, Licensing, Governance.
5. **Primary KB role** — exactly one of: Diagnosis, Resolution, Component Selection, Architecture Guidance, Best Practices, Governance & Constraints, Licensing.
6. **Supporting KB roles** — 1–2 (3 max only if justified).
7. **Primary + supporting internal KBs** — from `KBs/`.
8. **Output fields** — the domain-specific fields beyond `confidence` / `requires_escalation` / `sources`, including nested object shapes.
9. **Domain rules** — e.g. max 3 resolution paths, must include monitoring, must include assumptions and risks.

## Step 2 — Write the skill file

Create `Agents/<demo>/Skills/<skill-name>.md`:

- Frontmatter: only `name` and `description`, both double-quoted; `name` must equal the filename stem.
- Reproduce the template's sections in order: `Purpose`, `Input Contract (MANDATORY)`, `Output Contract (MANDATORY)`, `KB Orchestration Pattern` (subsections 1–6), `Core Requirements`, `Output Field Mapping`, `Confidence Guidelines`, `Output Rules (MANDATORY)`, `Output Constraints`, `Reference Rules (MANDATORY)` + `Sources Format`, `Error Handling`, `Behavior Constraints`.
- Replace every placeholder. No `DEFINE …`, `<field_1>`, or `EXAMPLE STRUCTURE` text may remain.
- Input contract is always `{ "query", "query_type", "add_context" }`.
- Output contract is JSON-only and always ends with `confidence`, `requires_escalation`, `sources`.
- Map each output field to a KB role in `Output Field Mapping`.

## Step 3 — Enforce the behavior contract

The skill must **not**:

- emit Markdown, prose, greetings, or explanations;
- ask clarifying questions or classify intent (coordinator owns that);
- reference more than 2–3 KB sources, or re-rank SharePoint results;
- exceed 3 items in any recommendation/alternative/resolution list.

The skill must:

- prefer internal KBs, using Microsoft documentation to validate and enrich (Microsoft docs win on technical accuracy; internal KB wins on company policy);
- extract sections rather than summarize whole documents;
- define a low-confidence fallback returning `confidence: "Low"`, `requires_escalation: true`, and the missing inputs/assumptions.

## Step 4 — Register and route

1. Add a `###` entry to `Skills/Registry/skill-registry.md` using the `Skill Entry Template` fields (`skill_name`, `display_name`, `purpose`, `owner`, `version`, `status`, `intent_supported`, `requires_coordinator`, `primary_role`, `supporting_roles`, `primary_kb`, `supporting_kbs`, `kb_usage_rules`, `input_contract`, `output_contract`, `confidence_guidelines`, `escalation_supported`, `output_format`, `output_constraints`, `validation_checklist`, `test_scenarios`, `last_updated`, `change_log`, `notes`). Start new skills at version `1.0.0`, status `Active`.
2. If the coordinator must route to it, add the intent + required context questions + `<SkillName>.Invoke(query, add_context)` mapping in `Agents/<demo>/Agents/<Agent Name>.md`.
3. Mention the skill in `Skills/README.md` and `ARCHITECTURE.md` only if those files enumerate skills.

## Step 5 — Validate

Report each check explicitly:

- [ ] Frontmatter parses; `name` matches filename.
- [ ] All JSON blocks are syntactically valid (watch for the `"add_context: "` misplaced-colon bug).
- [ ] File is under **8,000 characters** — measure it (`wc -m "<path>"`), don't estimate.
- [ ] Exactly one primary role; ≤2 supporting roles.
- [ ] No conversational or Markdown-output instructions.
- [ ] Registry entry added; coordinator routing updated if applicable.
- [ ] Four test scenarios documented: clear, ambiguous, missing context, cross-domain.

## Notes

- Paths contain spaces — quote them in every shell command.
- Do not rename or reformat neighbouring files to "normalize" naming; the mixed convention is intentional.
