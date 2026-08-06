---
version: 0.1.0
license: CC-BY-SA-4.0
copyright: © 2026 Roberto Bravo
---
# Context Governance

This document defines the governance rules for project context.

## Authority hierarchy

Context authority follows this hierarchy:

```text
core
  ↓
project
  ↓
user
```

A lower level may specialise or make more specific the rules defined by a higher level, but it must not contradict them.

When a higher-level rule is no longer appropriate, it must be consciously changed at the level that has authority over it rather than overridden implicitly at a lower level.

Playbooks provide specialised knowledge and procedures. They are subject to the rules defined by `core` and `project` and do not constitute an independent level of authority.

The authority hierarchy is not negotiated during task execution.

## Context specialisation

The effective context of a task may be composed from context defined at different scopes or locations.

A project may provide shared context while one or more components provide additional context specific to their own scope. Context does not need to be physically duplicated in every component in order to apply to it.

When context is composed:

- mandatory context from applicable higher scopes remains mandatory;
- more specific context may specialise context from the scope that contains it;
- more specific context must not contradict context with higher authority;
- optional context is still loaded progressively according to the needs of the task.

Context composition does not change the authority hierarchy.

If an exception to a higher-level rule is required, that exception must be explicitly authorised at the level that has authority to establish it.

## Human validation

AI assistants and agents may:

- detect potentially relevant knowledge;
- identify inconsistencies or outdated context;
- propose changes;
- draft new context;
- modify context files when they have the technical capability and authorisation to do so.

None of these actions makes a change canonical by itself.

Every context change must pass through the human validation mechanism defined by the project.

Unless the project defines otherwise:

- in a professional project, validation is the responsibility of the person responsible for its technical architecture;
- in a personal project, validation is the responsibility of its owner.

Technical capability to modify a file never implies authority to approve its contents.

## Context changes

Changes to context must be explicit and reviewable.

When an assistant or agent identifies information that may have persistent value, it should propose the appropriate context change rather than silently treating that information as canonical.

The responsible person decides whether the proposed change should become part of the project's context.

Once validated, the change is incorporated into the canonical context through the project's version-control workflow.

## Source of truth

Canonical context is defined by the Markdown documents versioned with the project.

Memories, conversations, tool-specific instructions, local configuration, generated summaries, or other external representations may assist the work, but they do not supersede the canonical context.

When these representations conflict with canonical context, the canonical context prevails unless an authorised change is made through the project's validation process.