# AGENTS.md

Guidance for AI coding agents working in **Powerfull Demos** — a documentation-and-assets repository of Power Platform / Copilot Studio / Azure AI Foundry demo implementations.

## What this repo is (and is not)

- **Content repo, not a software project.** There is no `package.json`, build, test runner, or CI. Deliverables are Markdown, PDFs (KBs), CSVs (evals), and images.
- **No build/lint/test commands exist.** Do not invent or run them. "Testing" means manually validating documented steps and the eval CSVs.
- Demos live under three top-level categories: `Apps/`, `Agents/`, `Automation/`. Only `Agents/` exists today.

## Repository map

| Path | Purpose |
| --- | --- |
| [`README.md`](./README.md) | Repo entry point + curated demo list table |
| [`CONTRIBUTING.md`](./CONTRIBUTING.md) | Branch/PR workflow, demo folder requirements, PR checklist |
| [`SECURITY.md`](./SECURITY.md) | Vulnerability reporting; security is handled per-demo |
| `Agents/Power Platform Specialist/` | The flagship demo (see its own docs below) |

Demo-local docs are the **source of truth** — read them before answering anything about a demo:

- [`Agents/Power Platform Specialist/README.md`](./Agents/Power%20Platform%20Specialist/README.md) — overview, supported platform versions, limitations, manual deployment steps
- [`Agents/Power Platform Specialist/ARCHITECTURE.md`](./Agents/Power%20Platform%20Specialist/ARCHITECTURE.md) — Coordinator + Specialist Skills design, instruction layering, KB roles
- [`Agents/Power Platform Specialist/Skills/README.md`](./Agents/Power%20Platform%20Specialist/Skills/README.md) — **authoritative skill authoring guide** (design principles, KB orchestration, validation checklist)
- [`Agents/Power Platform Specialist/Skills/Registry/skill-registry.md`](./Agents/Power%20Platform%20Specialist/Skills/Registry/skill-registry.md) — every skill must be registered here

## Core architecture concept

Do not blur these layers. They are the whole point of the demo:

```text
User → Coordinator Agent → Specialist Skill → Knowledge Bases → Coordinator → Response
```

- **Coordinator** (`Agents/Power Platform Specialist/Agents/Power Platform Specialist.md`) owns intent classification, clarifying questions, routing, and *all* user-facing formatting.
- **Specialist skills** (`Skills/*-skill.md`) do domain reasoning and return **JSON only** — never Markdown, prose, or follow-up questions.
- **KBs** (`KBs/*.pdf`) are consumed through *roles* (Diagnosis, Resolution, Component Selection, Architecture Guidance, Best Practices, Governance & Constraints, Licensing), not by hard-coded filename.

## Conventions

- **Paths contain spaces.** Always quote them in shell commands and URL-encode them in Markdown links (`Power%20Platform%20Specialist`).
- **File naming is intentionally mixed** — match the neighbours, don't normalize:
  - Skills & registry: lowercase kebab-case (`governance-skill.md`, `skill-registry.md`)
  - Templates, demo folders, KBs, images: Title Case with spaces
  - Evals: `PPlatSpecialist-<Topic>-Eval.csv`
- **Copilot Studio hard limits** shape the content: agent instructions and skill instructions must stay under **8,000 characters**. Keep authored prompts lean; prefer trimming over appending.
- Eval CSVs use exactly two columns: `question,expectedResponse`. Some rows are in Portuguese (pt-BR) — preserve the source language of existing rows.
- Do not commit secrets, credentials, tokens, connection strings, or customer data (see `CONTRIBUTING.md`).

## Editing rules

- When adding a demo, follow the folder contract in [`CONTRIBUTING.md`](./CONTRIBUTING.md) (`README.md` with summary, prerequisites, step-by-step execution, YouTube link, artifact inventory) **and** add a row to the demo list table in the root `README.md`.
- When adding or changing a specialist skill, follow `.github/instructions/copilot-studio-skills.instructions.md` and update the skill registry in the same change.
- `main` is protected. Work on a feature branch (`feature/…`, `fix/…`, `docs/…`) and open a PR. Current working branch is `develop`.

## Known inconsistencies (don't "fix" silently, flag them)

- Root `README.md` links `LICENSE.md`; the actual file is `LICENSE`.
- `governance-skill.md` exists but has no entry in `skill-registry.md`.
- The coordinator routes an `ArchitectureDesign` skill, but no `architecture-skill.md` file exists.
- Two overlapping templates exist: `Skills Master Template.md` and `Skill Master Template (New).md` — the `(New)` one is the current standard.
