---
name: strawberryfields-index
description: This skill should be used when users ask how to use strawberryfields and the correct generated documentation skill must be selected before going deeper into source code.
---

# strawberryfields Skills Index

## Request triage by intent
- **First run / onboarding / backend choice** -> `strawberryfields-getting-started`
- **Install, dependencies, editable/dev/docs/test environment** -> `strawberryfields-build-and-install`
- **Python API usage, parameters, program/engine semantics** -> `strawberryfields-api-and-scripting`
- **Runnable scripts to adapt quickly** -> `strawberryfields-examples-and-tutorials`
- **Cross-module implementation tracing** -> `strawberryfields-code`
- **API docs template rendering/scaffolding** -> `strawberryfields-templates`
- **Output analysis and post-processing** -> `strawberryfields-analysis-and-output`
- **Contributor architecture/extension hooks** -> `strawberryfields-developer-guide`
- **Low-frequency docs/meta references** -> `strawberryfields-advanced-topics`

## Docs-first escalation order
1. Pick one best-fit topic skill from the routes above.
2. Read that skill's **Primary documentation references** first.
3. If needed, inspect that skill's `references/doc_map.md` for full topic inventory.
4. If docs still leave ambiguity, inspect that skill's `references/source_map.md` and follow ranked entry points.
5. Use targeted symbol search in source (`rg -n "<symbol_or_keyword>" strawberryfields`).

## Quick start from this folder
- Use `references/doc_map.md` for a compact overview of routing resources.
- Use `references/source_map.md` for function-level entry points when triage needs code verification.

## Core skills to prioritize for realistic simulations
- `strawberryfields-getting-started`
- `strawberryfields-build-and-install`
- `strawberryfields-api-and-scripting`
- `strawberryfields-examples-and-tutorials`
- `strawberryfields-code`

## Additional topic skills
- `strawberryfields-analysis-and-output`
- `strawberryfields-developer-guide`
- `strawberryfields-templates`
- `strawberryfields-advanced-topics`

## Documentation-first inputs
- `doc`

## Tutorials and examples roots
- `examples`

## Test roots for behavior checks
- `tests`

## Source directories for deeper inspection
- `strawberryfields`
