# Power Platform Specialist Copilot

## Version and Date

This demonstration was last updated on Jul 02, 2026.

## Overview

This folder contains the implementation and standards for the **Power Platform Specialist**, a Copilot Studio–based solution designed to support internal users with:

- Troubleshooting Power Platform issues
- Designing architecture solutions
- Recommending platform components
- Optimizing performance
- Understanding licensing considerations

The solution is built using a **Coordinator Agent + Specialist Skills architecture**, where each skill provides domain-specific reasoning supported by structured internal Knowledge Bases (KBs).

## Goals

This demo have the following goals:

- Provide a reference architecture for a Copilot Studio **multi-agent solution** that uses **skills** instead of **connected agents** that can deal with **multiple intents** on the same domain without **loosing accuracy** or **context**.
- Identify and demonstrate **best practices** for the **Capability Routing**, a **knowledge base orchestration** and **role-based reasoning** approach for multi-agent solutions to facilitate **knowledge evolution** and **knowledge reuse** across multiple skills and agents.
- Identify **limitations** on this architecture and provide guidance for **future improvements** and alternative solutions for them.

## Intended Audience

This demo is intended for **solution architects**, **developers**, and **makers** who want to understand how to implement a multi-agent solution using Copilot Studio and AI Agents, with a focus on **knowledge orchestration** and **role-based reasoning**.

## Demo Explanation

You can read about the Capability Routing concept and watch a video about this demonstration with a complete analysis of this demonstration on the following blog post.

 [`Blog do Souza - Antes do Primeiro Token`](https://ricardodesouza.com/antes-do-primeiro-token/)

## File Structure

```
Power Platform Specialist/
├── ARCHITECTURE.md          # Full architectural description
├── README.md                # This file (demo overview, setup, security)
├── Agents/
│   └── Power Platform Specialist.md  # Agent instructions (coordinator prompt)
├── KBs/                     # Knowledge Base source documents (grounding material)
└── Skills/
    ├── README.md            # Skills architecture and orchestration overview
    ├── licensing-skill.md   # Skill: licensing guidance
    ├── performance-skill.md # Skill: performance optimization
    ├── solutioning-skill.md # Skill: component recommendation
    ├── troubleshooting-skill.md # Skill: issue diagnosis
    ├── Registry/
    │   └── skill-registry.md # Central registry of all skills (contracts, mappings)
    └── Templates/
        ├── Skill Generator Prompt.md  # Prompt to draft new skills
        └── Skills Master Template.md  # Normalization template for skill files
```

## Supported Platforms & Versions

This demo was created and tested using the following Power Platform configurations:

- **Environment**
  - Region: United States
  - Release Cycle: Early Access
  - Release Channel: Montly
  - Database Version: 9.2.26064.138
- **Copilot Studio**
  - UX Version: 23.31.2

## Architecture

See `ARCHITECTURE.md` for the full architecture description.

## Limitations

### Copilot Studio

Copilot Studio **new experience** and **new agent type** are in public preview (on the date of this version) and the following limitations and/or some features/configurations that impacted some architectural and design decisions:

- Agent instructions cannot exceed 8.000 characters.
- You cannot add references to tools or knowledge on agent instructions.
- You cannot add MCP Servers as Knowledge.
- Agent always call tools before Knowledge.

### One skill invocation per user interaction

- This architecture was not designed to **handle multiple skills in a user interaction**. Instead it uses **KB roles** to call multiple Knowledge Bases (KBs) and so handle multiple intents.
- Agent recognizes the **main user intent** and calls the **skill reponsible for it** (for example performance skill). The skill can use content **from any KB role associated with it** (for example a best practice KB), but the response will be generated using the rules from the performance skill.
- The goal is to decrease instructions complexity.

## Deployment

A solution file to be imported on Power Platform is **not available**. To use this demonstration you should:

- Create the agent manually on your environment.
- Copy+Paste agent instructions
- Use the skill.md files to upload the skills or use its content to create them.
- Upload the KBs on a Sharepoint Document Library, One Drive Business Folder or on the agent itself.

## Security and Compliance

> Note: This demo is not a product-ready or production implementation.

- The demo is intended for **self testing / study only**.
- It is **not an implementation recommendation**. It’s a study case to help test Copilot Studio capabilities and limitations.
- Use the demo only as **a reference and learning material**.
- If you want to use the demo as a starting point for a real project, you must **revise** the agent and skills instructions and the KBs content to ensure they meet your **organization’s security**, **compliance**, and **governance requirements**.
- Power Platform evolves **rapidly** and **frequently**, so always use **Microsoft official documentation** to get updated content about it.
