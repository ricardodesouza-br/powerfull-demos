---
mode: agent
description: "Scaffold a new demo folder under Apps/, Agents/, or Automation/ following the repository contribution contract."
---

# New demo scaffold

Create a new demo that satisfies the contract in [`CONTRIBUTING.md`](../../CONTRIBUTING.md) and the repo conventions in [`AGENTS.md`](../../AGENTS.md).

## Inputs to collect first

Ask the user for anything missing — do not invent values:

- **Category**: `Apps`, `Agents`, or `Automation`
- **Demo name** (Title Case with spaces — this becomes the folder name)
- **Summary** (1–3 sentences)
- **Target platforms/versions** (e.g. Copilot Studio, Power Apps, Azure AI Foundry)
- **Prerequisites** and setup requirements
- **YouTube video URL** (required by the contribution checklist — if not yet available, add a clearly marked `TBD` placeholder)
- **Artifacts**: does the demo ship solution files/scripts, or is it documentation-only?

## What to create

```text
<Category>/<Demo Name>/
├── README.md
├── Assets/      # only if the demo has assets
├── Scripts/     # only if the demo has scripts
└── Artifacts/   # only if the demo ships deployable artifacts
```

Do not create empty folders that the demo will not use.

The demo `README.md` must contain these sections, modeled on [`Agents/Power Platform Specialist/README.md`](../../Agents/Power%20Platform%20Specialist/README.md):

- `# <Demo Name>`
- `## Version and Date`
- `## Overview`
- `## Goals`
- `## Intended Audience`
- `## Demo Explanation` (with the YouTube link)
- `## File Structure`
- `## Supported Platforms & Versions`
- `## Architecture` (add a separate `ARCHITECTURE.md` if the design is non-trivial)
- `## Limitations`
- `## Deployment` (state explicitly whether a solution file is available; otherwise give manual steps)
- `## Security and Compliance`

## Then

1. Add a row to the correct table in the root [`README.md`](../../README.md) demo list, with a URL-encoded relative link (`./Agents/My%20Demo/README.md`) and the "Artifacts available?" value.
2. Confirm no secrets, credentials, tokens, or connection strings are present.
3. Remind the user that `main` is protected — this work belongs on a `feature/…` branch and goes in via PR.
4. Print the PR checklist from `CONTRIBUTING.md` with each item marked done or outstanding.
