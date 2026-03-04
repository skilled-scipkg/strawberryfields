---
name: strawberryfields-advanced-topics
description: This skill should be used for Strawberry Fields metadata and low-frequency reference topics (index, requirements, citations, migration notes) that are not direct simulation workflow questions.
---

# strawberryfields: Advanced Topics

## High-Signal Playbook
### Route conditions
- Use this skill for docs index navigation, bibliography/citation requests, requirements metadata, and migration-reference questions.
- Route install/runtime blockers to `strawberryfields-build-and-install`.
- Route first runnable simulations to `strawberryfields-getting-started`.
- Route API behavior and debugging to `strawberryfields-api-and-scripting` or `strawberryfields-code`.

### Canonical workflow
1. Start with `doc/index.rst`, `doc/zreferences.rst`, and `doc/references.bib`.
2. For dependency/version metadata, cross-check `doc/requirements.txt`, `requirements.txt`, and `setup.py`.
3. For package metadata and citation behavior, verify `strawberryfields/__init__.py` and `strawberryfields/_version.py`.
4. For device-spec metadata questions, inspect `strawberryfields/device.py`.
5. Validate with one local metadata command before answering.

### Minimal metadata check
```bash
python - <<'PY'
import strawberryfields as sf
print(sf.version())
sf.cite()
PY
```

### Validation checkpoints
- Reported version matches `strawberryfields/_version.py`.
- Citation text comes from `sf.cite()` behavior, not inferred prose.
- Requirements claims are consistent across `setup.py` and requirements files.

## Primary documentation references
- `doc/index.rst`
- `doc/zreferences.rst`
- `doc/references.bib`
- `doc/requirements.txt`
- `doc/development/migration_guides.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If documentation still leaves ambiguity, inspect `references/source_map.md`.
- Cite exact file paths in responses.

## Source entry points for unresolved issues
- `strawberryfields/__init__.py` (`version`, `about`, `cite`)
- `strawberryfields/_version.py` (`__version__`)
- `strawberryfields/device.py` (`Device.validate_target`, `Device.validate_parameters`, `Device.create_program`)
- `strawberryfields/io/blackbird_io.py` (`from_blackbird`, `to_blackbird`)
- `strawberryfields/io/xir_io.py` (`from_xir`, `to_xir`)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields doc`).
