---
name: strawberryfields-developer-guide
description: This skill should be used for Strawberry Fields contributor workflows, architecture navigation, and extension hooks across compilers, backends, and device constraints.
---

# strawberryfields: Developer Guide

## High-Signal Playbook
### Route conditions
- Use this skill for contributor architecture, extension points, and implementation-level development workflow questions.
- Route end-user circuit authoring to `strawberryfields-getting-started` or `strawberryfields-api-and-scripting`.
- Route packaging and dependency setup issues to `strawberryfields-build-and-install`.

### Triage questions
- Is the change in frontend (`Program`, `Engine`, `ops`) or backend/compiler internals?
- Is the task a bug fix, test update, or extension of supported operations/devices?
- Which backend(s) and compiler(s) are affected?
- Which existing tests are the closest behavioral contract?

### Canonical workflow
1. Start with `doc/development/development_guide.rst` and `doc/code/sf_compilers.rst` / `doc/code/sf_backends.rst`.
2. Locate ownership boundaries (`strawberryfields/program.py`, `strawberryfields/engine.py`, `strawberryfields/compilers/compiler.py`, backend classes).
3. Implement minimal, targeted changes at the correct abstraction layer.
4. Validate with focused tests before broad test runs.
5. Report the exact module boundary and behavior contract changed.

### Minimal inspection commands
```bash
rg -n "class Compiler|def compile|def decompose" strawberryfields/compilers/compiler.py
rg -n "class BaseBackend|def begin_circuit|def state" strawberryfields/backends/base.py
rg -n "def run\(|def _run\(" strawberryfields/engine.py
pytest tests/frontend/compilers/test_compiler.py -q
```

### Pitfalls and fixes
- Editing backend-specific behavior when frontend contract is the real issue.
- Skipping compiler validation for device-constrained programs.
- Changing behavior without updating or adding nearest-scope tests.

### Validation checkpoints
- Behavior is covered by at least one focused test module.
- Compiler/backend/frontend boundaries remain explicit after changes.
- New behavior is consistent with device parameter validation logic.

## Primary documentation references
- `doc/development/development_guide.rst`
- `doc/development/research.rst`
- `doc/development/release_notes.md`
- `doc/development/migration_guides.rst`
- `doc/code/sf_compilers.rst`
- `doc/code/sf_backends.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If ambiguity remains after docs, inspect `references/source_map.md`.
- Cite exact file paths in responses.

## Source entry points for unresolved issues
- `strawberryfields/compilers/compiler.py` (`Compiler.compile`, `Compiler.decompose`, `Compiler.update_params`, `Compiler.add_loss`)
- `strawberryfields/backends/base.py` (`BaseBackend.begin_circuit`, `BaseBackend.state`, measurement methods)
- `strawberryfields/device.py` (`Device.validate_parameters`, `Device.create_program`)
- `strawberryfields/tdm/program.py` (`TDMProgram.context`, `TDMProgram.unroll`, `TDMProgram.assert_modes`)
- `strawberryfields/io/blackbird_io.py` (`from_blackbird`, `to_blackbird`)
- `strawberryfields/logger.py` (`create_logger`, `logging_handler_defined`)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields`).
