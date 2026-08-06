# Context Library

Context Library (CL) is a lightweight, Git-based approach to maintaining reusable context for collaboration between humans and AI assistants and agents.

It treats context as a project asset: explicit, versioned, reviewable and controlled by people, rather than tied to a specific AI tool or provider.

CL uses Markdown as its canonical format and Git as its source of truth.

## Structure

Context is organised into four scopes:

| Scope | Purpose |
| --- | --- |
| `core/` | Mandatory reusable rules and principles |
| `playbooks/` | Reusable specialised knowledge loaded when relevant |
| `project/` | Project-specific knowledge, decisions and constraints |
| `user/` | Optional collaboration context and user preferences |

`AGENTS.md` files act as discovery mechanisms that tell AI assistants and agents how to locate and load the context applicable to their work.

## Principles

Context Library is based on a small set of principles:

- people control canonical context;
- changes require human validation;
- context is discovered and loaded progressively;
- only context relevant to the current work should be loaded;
- reusable knowledge should remain independent of individual projects;
- external content is subject to an explicit trust boundary;
- provenance and licensing must remain traceable;
- provider-specific mechanisms must not become the canonical source of knowledge;
- simplicity is preferred until real-world use demonstrates the need for additional mechanisms.

The knowledge matters more than the structure used to store it.

## Status

Context Library is experimental and under active development.

The current structure is already intended for use in real-world projects. Its design will be validated and evolved through the experience gained from using it.

Its architecture and conventions may change as practical experience reveals what works, what does not and what should be replaced by emerging standards.

## Documentation

See [`OVERVIEW.md`](OVERVIEW.md) for an introduction to the model.

The project's design, decisions and constraints are maintained in [`.context/project/PROJECT.md`](.context/project/PROJECT.md).

## Licence

Original Context Library content is licensed under the Creative Commons Attribution-ShareAlike 4.0 International licence (CC BY-SA 4.0).

Third-party or adapted content may be subject to different licensing and attribution requirements.

See [`LICENSE`](LICENSE) for the full licence text.