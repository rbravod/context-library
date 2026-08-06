---
version: 0.1.0
license: CC-BY-SA-4.0
copyright: © 2026 Roberto Bravo
---
# Context Metadata

This document defines the metadata used to identify and maintain reusable context.

## Scope

Reusable context files must provide sufficient metadata to identify their version, provenance and applicable legal conditions.

This requirement applies to reusable context maintained in:

- `core/`;
- `playbooks/`;
- `user/`.

Project-specific context does not require these metadata unless the project defines a concrete need for them.

## Required metadata

Reusable context files must define:

- `version`: version of the reusable context;
- `license`: licence applicable to the content;
- `copyright`: copyright holder or required copyright notice.

When the content originates from or is based on external material, it must also define:

- `source`: source from which the content originates.

Metadata must describe the context file itself, not the project in which a copy happens to be used.

## Version

The version identifies the evolution of reusable context independently from Git history.

A newer version does not imply automatic replacement of an existing project copy.

Before updating reusable context, the current project copy and the newer source version must be compared and the change must follow the project's normal validation process.

## Provenance

When reusable context originates from or is based on external material, `source` must provide enough information to identify and locate that material.

Original content does not require a `source` field. Its repository and version-control history provide its provenance.

For third-party or adapted content, provenance must be sufficient to locate and audit the original material.

Copying or adapting content must not remove provenance or applicable attribution requirements.

## Licence and copyright

Licence information must identify the terms under which the reusable context may be copied, modified and redistributed.

Copyright information must identify the applicable copyright holder or required copyright notice.

Metadata must not be used to replace licence texts, attribution notices or other legal information that must be preserved separately.

## Representation

Reusable context metadata must be represented using YAML front matter at the beginning of the document.

The standard metadata fields are:

```yaml
---
version: 0.1.0
license: CC-BY-SA-4.0
copyright: © 2026 Roberto Bravo
---
```

When content is adapted from another source, `source` must also be included:

```yaml
---
version: 0.1.0
license: CC-BY-SA-4.0
copyright: © 2026 Roberto Bravo
source: https://example.org/original-source
---
```
