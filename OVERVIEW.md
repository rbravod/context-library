# Context Library - Overview

Context Library (CL) is a simple way to provide structured, reusable and versioned context to people and AI agents working on a project.

It is not an AI platform, an agent framework or a replacement for project documentation.

At its core, CL is a convention for organising Markdown documents inside a repository so that both humans and AI tools can understand:

- the rules they must follow;
- the project they are working on;
- the specialised knowledge available to them;
- the preferences relevant to their collaboration.

## A useful analogy

When using ChatGPT or another AI assistant, several layers of instructions and context influence its behaviour.

CL applies a similar model to a project repository.

| AI assistant | Context Library | Purpose |
|---|---|---|
| System rules / guardrails | `core/` | Mandatory project-wide rules |
| Domain knowledge / skills | `playbooks/` | Reusable specialised knowledge |
| Project configuration | `project/` | Project-specific context |
| User preferences | `user/` | Optional collaboration context |

The analogy is conceptual rather than technical.

The AI platform still has its own system rules, which always remain outside CL and take precedence over anything stored in the repository.

## Structure

```text
.context/
├── core/
├── playbooks/
├── project/
└── user/
```

### `core/`

Contains mandatory rules and principles that apply to every task.

Examples:

- context governance;
- trust boundaries;
- knowledge management;
- working principles.

An agent must always read and follow `core/`.

### `playbooks/`

Contains reusable specialised knowledge and procedures.

Examples:

- Moodle development;
- Git workflows;
- Docker;
- architecture;
- documentation practices.

Only the playbooks relevant to the current task need to be loaded.

### `project/`

Contains context specific to the current project.

Examples:

- objectives;
- architecture;
- decisions;
- constraints;
- use cases;
- domain definitions.

This is where the agent learns what project it is actually working on.

### `user/`

Contains optional context about how a particular person prefers to work or collaborate.

Examples:

- communication preferences;
- writing style;
- working preferences;
- decision-making preferences.

A project may contain no `user/` context at all.

## How an agent uses it

The repository contains a root `AGENTS.md` that acts as the entry point.

Its purpose is not to contain all project knowledge. It tells the agent how to discover and use the available context.

A simplified flow is:

```text
Task
  ↓
AGENTS.md
  ↓
Read mandatory core/
  ↓
Identify relevant project context
  ↓
Load required playbooks
  ↓
Load relevant user context, if applicable
  ↓
Perform the task
  ↓
Human validation
```

Context should be loaded progressively rather than sending the complete project knowledge to the AI for every task.

## Human control

AI agents may read context, analyse information, propose changes and, when authorised, modify files.

They do not decide what becomes canonical project knowledge.

Changes to canonical context require human validation.

Git provides traceability and history.

## Why use it?

Without structured project context, much of the information provided to AI tools lives in conversations, individual prompts, personal memory or tool-specific configuration.

That knowledge is difficult to reuse and easy to lose.

CL moves the relevant part of that knowledge into plain Markdown files that are:

- versioned;
- reviewable;
- reusable;
- understandable by humans;
- consumable by different AI tools;
- independent of a particular AI provider.

The objective is not to give an AI agent more autonomy.

The objective is to give it better context.