---
name: strawberryfields-build-and-install
description: This skill should be used when users ask about build and install in strawberryfields; it prioritizes documentation references and then source inspection only for unresolved details.
---

# strawberryfields: Build and Install

## High-Signal Playbook
### Route conditions
- Use this skill for package installation, editable dev setup, dependency/version conflicts, and docs/test environment prep.
- Route first circuit/API usage to `strawberryfields-getting-started` or `strawberryfields-api-and-scripting`.
- Route docs template rendering issues to `strawberryfields-templates`.

### Triage questions
- Is the user installing stable, preview (GitHub), or editable source?
- Which Python version/interpreter is active (`python --version`, venv/conda)?
- Is TensorFlow backend support required?
- Is the goal runtime usage, local development, or docs build?
- Are failures from dependency resolution, import-time errors, or test failures?
- Are pinned requirements required for reproducibility?

### Canonical workflow
1. Confirm Python compatibility and interpreter isolation (`README.md`, `doc/install.rst`, `setup.py`).
2. Choose install route:
   - Stable: `pip install strawberryfields --upgrade`.
   - Preview: `pip install git+https://github.com/XanaduAI/strawberryfields.git#egg=strawberryfields`.
   - Source/editable: `git clone ... && pip install -e .`.
3. For contributors, install dev dependencies (`requirements-dev.txt`, `doc/development/development_guide.rst`).
4. For docs contributors, install docs dependencies (`doc/requirements.txt`).
5. Run a minimal import + engine smoke test.
6. Run targeted tests before broad suite (`make test-[component]`).

### Minimal working example
```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e .
python - <<'PY'
import strawberryfields as sf
from strawberryfields import ops
p = sf.Program(1)
with p.context as q:
    ops.Sgate(0.2) | q[0]
r = sf.Engine("gaussian").run(p)
print(type(r.state).__name__)
PY
```

### Pitfalls and fixes
- Python mismatch across docs/metadata: verify against `setup.py` classifiers and local env before install.
- Missing TensorFlow when using `tf` backend: install `tensorflow` explicitly (`doc/introduction/circuits.rst`, `doc/development/development_guide.rst`).
- Expecting source edits to reflect without editable mode: reinstall with `pip install -e .`.
- Test tools missing: install `requirements-dev.txt` before running `make test`.
- Docs build failures from missing Sphinx stack: install `doc/requirements.txt` then run `make docs`.
- Overly broad full-suite runs during triage: start with targeted `pytest`/`make test-[component]`.

### Convergence/validation checks
- `python -c "import strawberryfields as sf; print(sf.__version__)"` succeeds.
- Minimal circuit run returns a non-`None` state on local backend.
- Targeted integration test passes (for example `tests/integration/test_engine_integration.py`).
- For reproducibility-sensitive setups, ensure pinned versions from `requirements*.txt` are installed.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/install.rst`
- `README.md`
- `doc/development/development_guide.rst`
- `doc/code/sf_compilers.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/teleportation.py`

## Test references
- `tests/integration/test_engine_integration.py`

## Optional deeper inspection
- `strawberryfields`

## Source entry points for unresolved issues
- `setup.py` (`install_requires`, supported Python classifiers, package data)
- `requirements.txt` (runtime dependency pins used in this repo)
- `requirements-dev.txt` (test/lint/dev tooling)
- `doc/requirements.txt` (docs build dependency stack)
- `strawberryfields/engine.py` (backend loading and runtime option behavior)
- `strawberryfields/compilers/compiler.py` (compile strategy base behavior)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields`).
