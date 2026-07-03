# Powerfull Demos

Repository with sample implementations for **Power Platform** and **AI Agents** hosted on **M365 Copilot**, **Copilot Studio** and **Azure AI Foundry**, created specifically to help **makers**, **developers** and **solution archictects** test platform components features through medium to complex case scenarios.

## Demo categories

This repo groups demos into three folders:

- **`Apps/`**: sample applications (Power Apps / app experiences)
- **`Agents/`**: Copilot Studio / AI Agent patterns and specialist skills
- **`Automation/`**: Power Automate / automation scenarios

## How to use demos

For each demo:

1. Open the demo folder’s **`README.md`**.
2. Follow the **setup + execution instructions** (instructions and/or scripts).
3. Review **artifacts** (when present). Some demos include solution files and/or deployable assets; others are documentation/script-only.
4. Watch the **YouTube video** linked from that demo README.

## Demo list

### Agents

| Demo | What you get | Artifacts available? | Demo README |
| --- | --- | --- | --- |
| Power Platform Specialist Copilot | Coordinator + specialist skills pattern (troubleshooting, architecture, solutioning, performance, licensing) | Not specified (check demo README) | [`Agents/Power Platform Specialist/README.md`](./Agents/Power%20Platform%20Specialist/README.md) |

### Apps

No demos added yet.

### Automations

No demos added yet.

---

## Concepts

> **Warning:** Concepts are handled (and validated) **within each demo**. Always follow the specific assumptions, prerequisites, and setup documented in the demo’s own `README.md`.

## FAQ

> **Warning:** FAQ answers may vary by demo (connections, environments, prerequisites, and artifacts). Treat each demo `README.md` as the source of truth.

- *Where do I find setup steps?*
  - In each demo folder’s `README.md`.
- *Do demos include solution files?*
  - Sometimes. Check the demo section for “Artifacts available?”.
- *Where is the demo video?*
  - Linked from each demo’s `README.md`.

## Security

> **Warning:** Security handling (secrets, connections, data exposure, and compliance constraints) is **handled on a per-demo basis**. Do not reuse demo configuration blindly.

See `SECURITY.md` for the full text.

General guidance (demo-specific details live in each demo README):

- Never commit secrets/credentials.
- Use environment-specific connections/keys.

## Testing

> **Warning:** Testing approach differs per demo. Each demo will define its own validation steps and expected outputs.

- Smoke-test instructions: included per demo.
- Expected outputs/artifacts: included per demo.

## Release

> **Warning:** Release notes and expectations vary by demo/folder. Any compatibility notes are defined in the relevant demo README.

This repo may use GitHub Releases/Tags for bundling demo updates.

## Licensing

This repository is licensed under the **MIT License**.

See `LICENSE.md` for the full text.

## Contributing

Contributions are welcome via **Pull Requests**.

### How to contribute

- Create a PR with:
  - a new demo folder under `Apps/`, `Agents/`, or `Automation/` **(if adding a demo)**
  - updated `README.md` content inside that demo folder
  - a link to the required YouTube video in the demo folder `README.md`

See `CONTRIBUTING.md` for the full text.

> **Warning:** Demo behavior, prerequisites, and setup are handled per demo—so PRs should focus on demo-local correctness and documentation.
