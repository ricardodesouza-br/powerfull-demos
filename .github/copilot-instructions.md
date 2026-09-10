# Copilot Instructions

## Repository purpose

`powerfull-demos` is a documentation-first collection of self-contained demonstrations for Microsoft Power Platform and AI agents hosted on M365 Copilot, Copilot Studio, and Azure AI Foundry. The primary audiences are makers, developers, and solution architects.

Demos are organized by category:

- `Apps/` — app experiences and Power Apps demonstrations.
- `Agents/` — Copilot Studio and AI agent patterns.
- `Automation/` — Power Automate and automation demonstrations.

The repository currently contains the `Agents/Power Platform Specialist/` demo. `Apps/` and `Automation/` may be referenced by the root documentation but are not necessarily present yet.

## Working conventions

- Treat each demo directory as independently understandable and follow its local `README.md` as the source of truth for prerequisites, setup, execution, artifacts, compatibility, and security.
- Keep changes focused. Do not introduce application scaffolding, package managers, or deployment automation unless the requested demo requires it.
- Preserve the existing directory and naming conventions, including spaces in demo names and the category folders `Apps/`, `Agents/`, and `Automation/`.
- Use Markdown links with URL-encoded spaces when linking to paths containing spaces.
- Update the relevant demo README whenever changing its files, setup, supported versions, artifacts, or behavior. Update the root `README.md` when adding or materially changing a demo.
- Do not invent artifacts, commands, prerequisites, videos, platform versions, or deployment instructions. If information is unavailable, state that clearly and direct the reader to the demo owner or official Microsoft documentation.

## Power Platform Specialist demo

The main demo is a Copilot Studio reference implementation under `Agents/Power Platform Specialist/`:

- `Agents/Power Platform Specialist/Agents/Power Platform Specialist.md` — coordinator-agent instructions.
- `Agents/Power Platform Specialist/Skills/` — specialist skill prompts and authoring guidance.
- `Agents/Power Platform Specialist/Skills/Registry/skill-registry.md` — lifecycle and governance registry; it is not a runtime dependency.
- `Agents/Power Platform Specialist/Skills/Templates/` — templates and generation guidance for new skills.
- `Agents/Power Platform Specialist/KBs/` — grounding and reference documents.
- `Agents/Power Platform Specialist/ARCHITECTURE.md` — architecture and orchestration model.

The architecture is conceptually: user → coordinator agent → one or more specialist skills → knowledge bases → coordinator response. Existing documentation describes a coordinator plus domain skills for solutioning, troubleshooting, architecture, performance, licensing, and governance.

When modifying a skill:

- Preserve single responsibility and the established coordinator/skill separation.
- Keep skill output machine-readable and JSON-first; user-facing formatting belongs to the coordinator.
- Define or preserve the primary KB role and supporting-role mappings in accordance with the authoring guide.
- Keep the skill registry entry synchronized with skill metadata, status, role mappings, KB mappings, test scenarios, and change history.
- Check Copilot Studio instruction-size and preview/runtime limitations documented by the demo before adding prompt text.
- Prefer internal KB content for grounding and use current official Microsoft documentation to validate platform-specific facts.

## Documentation and validation

This repository has no detected package manifest, source-code build system, or automated test command. Do not claim that a build or test passed unless a relevant command is added or explicitly provided by the demo.

For documentation-only changes, validate by:

1. Checking Markdown headings, lists, tables, and fenced blocks.
2. Checking relative links and referenced files, especially paths containing spaces.
3. Confirming that setup, artifact, security, and compatibility statements match the local demo files.
4. Searching for stale names, broken references, unresolved placeholders, and accidental secrets.
5. Reporting validation as documentation review when no executable test exists.

## Security and source handling

- Never commit secrets, credentials, tokens, connection strings, personal data, or environment-specific access details.
- Follow `SECURITY.md` and the security guidance in the affected demo README.
- Treat demo content as study/reference material, not production implementation advice, unless the local documentation explicitly says otherwise.
- For current Power Platform, Copilot Studio, licensing, governance, or Azure AI Foundry behavior, prefer official Microsoft documentation over assumptions or stale repository text.

## Contribution workflow

- Work on a descriptive branch; do not update protected `main` directly.
- Keep commits and pull requests focused and explain prerequisites, validation, and compatibility impact.
- New demos require a local `README.md` with a summary, prerequisites, step-by-step instructions, video link, and artifact inventory as specified in `CONTRIBUTING.md`.
- Before proposing a change, inspect the affected demo's README, architecture/instructions, skills, KBs, and registry entries rather than relying only on the root README.
