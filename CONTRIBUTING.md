# Contributing

Thanks for your interest in improving **Powerfull Demos**!

Contributions are welcome via **Pull Requests (PRs)**. This repository uses a protected `main` branch to preserve content quality, maintain traceability, and ensure all changes go through a documented review process.

## Maintainer note

This repository uses branch protection rules to ensure content quality, consistency, and traceability.

All contributions must be submitted through Pull Requests. Repository maintainers may use repository-approved administrative workflows when necessary to manage the repository while preserving the project's governance model.

## What to contribute

- New demos (add a folder under `Apps/`, `Agents/`, or `Automation/`)
- Improvements to existing demo documentation
- Fixes to demo scripts, assets, or instructions
- Updates to the curated demo list in the root `README.md` (optional but recommended)
- Corrections, clarifications, and usability improvements

## Demo folder requirements

For any new demo folder, include a `README.md` containing:

- Demo summary (1–3 sentences)
- Setup requirements and prerequisites
- Step-by-step execution instructions
- Link to the YouTube video for setup and execution
- Artifacts inventory (if any) and where they are stored

A typical structure is:

```text
Demo Folder/
├── README.md
├── Assets/
├── Scripts/
└── Artifacts/
```

## Contribution workflow

The `main` branch is protected and cannot be updated directly.

### 1. Create a working branch

If you are an external contributor, fork the repository first.

Create a branch using a descriptive name:

```text
feature/new-demo
feature/power-apps-enhancement
fix/readme-corrections
docs/update-contributing-guide
```

### 2. Make your changes

- Keep changes focused and easy to review
- Follow existing folder and naming conventions
- Update documentation when applicable
- Include all referenced scripts, files, and assets

### 3. Commit your changes

Use clear and descriptive commit messages.

Examples:

```text
Add Copilot Studio onboarding demo
Improve Power Apps setup instructions
Fix broken artifact references
Update README navigation
```

### 4. Push your branch

Push your changes to your fork or working branch.

### 5. Open a Pull Request

Create a Pull Request targeting the repository's contribution branch.

The Pull Request should clearly explain:

- What changed
- Why the change was made
- Any prerequisites or testing considerations
- Any potential impact on existing demos

### 6. Address feedback

If review comments are provided:

- Respond to feedback professionally
- Update the branch as needed
- Resolve conversations before requesting final review

### 7. Merge after approval

Changes are merged through Pull Requests only.

Direct commits or pushes to the protected `main` branch are not accepted.

## Pull Request checklist

Before submitting your Pull Request, verify:

- [ ] Demo instructions are accurate and complete (setup + execution)
- [ ] Any scripts/artifacts mentioned in the README exist in the demo folder
- [ ] No secrets, credentials, tokens, or sensitive information are committed
- [ ] The demo README includes the YouTube link
- [ ] The PR title and description clearly explain the changes
- [ ] Changes were made in a feature branch (not directly in `main`)
- [ ] Documentation has been updated where required
- [ ] Repository structure and naming conventions were followed
- [ ] Referenced files, screenshots, and assets are included
- [ ] Obsolete or duplicate content has been removed where appropriate

## Repository standards

Contributors should:

- Prefer clear, concise, and reproducible instructions
- Keep demos self-contained whenever possible
- Document prerequisites explicitly
- Avoid assumptions that are not documented in the demo
- Preserve consistency with the repository structure and style
- Ensure all external references and links are valid
- Follow existing naming conventions for folders and files

## Security guidelines

Do not commit:

- Secrets or credentials
- API keys
- Connection strings
- Access tokens
- Certificates
- Customer or confidential information
- Proprietary files that cannot be publicly distributed

If a demo requires sensitive configuration, document the setup process without including the actual secret values.

## Notes

> **Warning:** Demo-specific prerequisites, assumptions, licensing considerations, and security handling are managed within each demo. Contributors are responsible for ensuring their demo content is accurate, complete, and safe to use.
