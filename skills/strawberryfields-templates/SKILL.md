---
name: strawberryfields-templates
description: This skill should be used when users ask about templates in strawberryfields; it prioritizes documentation references and then source inspection only for unresolved details.
---

# strawberryfields: Templates

## High-Signal Playbook
### Route conditions
- Use this skill for API-doc rendering structure (`autosummary` templates), module/package doc-page scaffolding, and docs-generation formatting issues.
- Route runtime API behavior to `strawberryfields-api-and-scripting`.
- Route install/build environment issues to `strawberryfields-build-and-install`.
- Route contributor architecture questions to `strawberryfields-developer-guide`.

### Triage questions
- Is the issue in module pages, class pages, or autosummary tables?
- Is the template from `doc/_templates/autosummary_core` or `doc/_templates/autosummary`?
- Is a module/package missing docstrings or autosummary directives in source?
- Was the new docs page added to `doc/index.rst` toctree?
- Did `make docs` fail at template render time or at autodoc import time?
- Is the expected heading prefix `sf.` being produced?

### Canonical workflow
1. Identify affected template family (`autosummary_core` vs `autosummary`).
2. Check Jinja placeholders and title composition in the relevant template file.
3. Confirm source module/package docstrings and autosummary blocks exist (`doc/development/development_guide.rst`).
4. Ensure corresponding `doc/code/sf_<module_or_package>.rst` file exists.
5. Ensure `doc/index.rst` includes the page in the API toctree.
6. Build docs (`make docs`) and verify generated output page structure.

### Minimal working example
```rst
sf.my_module
============

.. currentmodule:: strawberryfields.my_module

.. automodapi:: strawberryfields.my_module
    :no-heading:
    :include-all-objects:
```

### Pitfalls and fixes
- Editing wrong template directory: map issue to `autosummary_core/*` vs `autosummary/*` first.
- Missing module/package docstring: autodoc/autosummary output appears empty.
- New API page not discoverable: add it to `doc/index.rst` API toctree.
- Docs dependencies missing: install `doc/requirements.txt` before `make docs`.
- Jinja indentation or block mismatch: keep block names/indentation aligned with existing templates.

### Convergence/validation checks
- `make docs` completes successfully.
- Generated page heading and prefix (`sf.<...>`) match template expectation.
- Autosummary sections render expected classes/functions/exceptions.
- Added module/package page appears in API docs navigation.

## Scope
- Handle questions about documentation grouped under the 'templates' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/_templates/autosummary_core/module.rst`
- `doc/_templates/autosummary_core/base.rst`
- `doc/_templates/autosummary/module.rst`
- `doc/_templates/autosummary/base.rst`
- `doc/development/development_guide.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `doc/development/example_module_rst.txt`
- `doc/development/example_package_rst.txt`
- `doc/development/example_module_autosummary.txt`

## Test references
- `tests`

## Optional deeper inspection
- `strawberryfields`

## Source entry points for unresolved issues
- `doc/_templates/autosummary_core/module.rst` (module page rendering skeleton)
- `doc/_templates/autosummary_core/base.rst` (class/object page rendering skeleton)
- `doc/_templates/autosummary/module.rst` (autosummary module table structure)
- `doc/_templates/autosummary/base.rst` (autosummary object rendering)
- `strawberryfields/__init__.py` (top-level export/docstring surface consumed by docs)
- `strawberryfields/backends/base.py` (core backend class docstrings and API objects)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields doc/_templates`).
