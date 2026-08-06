---
version: 0.1.0
license: CC-BY-SA-4.0
copyright: © 2026 Roberto Bravo
---
# Knowledge Management

This document defines how persistent knowledge is identified, evaluated and maintained within project context.

## Persistent knowledge

Context should contain knowledge that is useful beyond the immediate task.

During normal work, assistants and agents should identify information that may have persistent value, including:

- decisions;
- changes in criteria;
- new constraints;
- technical conclusions;
- relevant domain knowledge;
- inconsistencies or contradictions;
- outdated assumptions;
- knowledge required for future work;
- recurring patterns or conventions.

Not every observation, conversation or task result should become context.

Information should be incorporated only when retaining it is expected to improve future understanding, decisions or work.

## Knowledge capture

Knowledge capture should be part of the normal workflow rather than a separate documentation activity.

When potentially persistent knowledge is identified, the assistant or agent should:

1. determine the appropriate context scope;
2. identify whether an existing document should be updated or a new document is justified;
3. propose the specific change and its location;
4. submit the change to the project's human validation process.

Knowledge must not be silently promoted to canonical context.

## Knowledge sources

Sources used to discover knowledge are not automatically sources of truth.

Possible sources include:

- existing code;
- previous documentation;
- production systems;
- manuals;
- tickets;
- interviews;
- conversations;
- external documentation;
- observed behaviour;
- historical project context.

These sources may be incomplete, contradictory, outdated or incorrect.

Assistants and agents may analyse, compare and correlate them, but information discovered from them remains provisional until validated.

## Conflicting information

When different sources provide conflicting information, the conflict must be made explicit.

An assistant or agent should not silently choose one interpretation and treat it as canonical.

Where possible, it should:

1. identify the conflicting sources;
2. describe the relevant discrepancy;
3. determine whether additional evidence can resolve it;
4. propose a resolution when appropriate;
5. request human validation before incorporating the resolution into canonical context.

Existing canonical context remains authoritative until a validated change replaces it.

## Existing behaviour

Existing behaviour does not automatically constitute a requirement.

The presence of functionality, behaviour, conventions or limitations in an existing system is evidence about that system, not proof that they should be preserved.

When reconstructing, replacing or evolving a system, observed behaviour must be evaluated before it is promoted to a requirement.

## Context maintenance

Context should evolve when the knowledge required to work correctly changes.

Assistants and agents should identify context that appears to be:

- outdated;
- contradicted by validated knowledge;
- incomplete in a way that affects current work;
- duplicated unnecessarily;
- no longer useful.

They should propose the smallest appropriate change rather than rewriting context unnecessarily.

Git provides the historical record. Context documents should describe the current validated understanding unless preserving an older state is itself useful for current work.

## Deprecation

Context Library does not require a general lifecycle status for every document.

Information should be explicitly marked as deprecated, superseded, transitional or pending removal only when that status is relevant to current or future work.

Historical information that is no longer operationally relevant should normally remain available through version control rather than being preserved in active context.

## Obsolete knowledge

Context must represent the current understanding of the project.

When an assistant or agent identifies context that may be obsolete, it should:

1. identify the affected context;
2. determine what newer information appears to supersede it;
3. assess whether the existing context should be updated, replaced or removed;
4. propose the specific change and its location;
5. submit the change through the project's human validation mechanism.

Obsolete context must not be preserved merely for historical reference when it can mislead future work.

Obsolete or historical knowledge should only be retained when it remains relevant to current or future work.

When retained, it must be clearly identified as obsolete or historical and explain why it is still relevant.

Do not silently resolve contradictions between current and potentially obsolete context.

## System observation

Assistants and agents may derive potentially useful knowledge by observing the system they are working with.

Observations may come from sources such as:

- source code;
- configuration;
- runtime behaviour;
- logs and errors;
- tests;
- infrastructure;
- existing documentation;
- generated artefacts.

Observed information must not automatically be treated as canonical context.

When an observation appears to reveal persistent knowledge that is not represented in the current context, the assistant or agent should:

1. distinguish the observed fact from any interpretation or inference derived from it;
2. check whether the knowledge is already represented in context;
3. identify contradictions with existing context;
4. determine whether the knowledge has persistent value;
5. propose the specific context change and its location when appropriate;
6. submit the change through the project's human validation mechanism.

When evidence is incomplete or ambiguous, uncertainty must be preserved rather than converted into a canonical assertion.

System observation complements maintained context; it does not silently override it.