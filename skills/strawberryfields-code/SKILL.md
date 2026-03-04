---
name: strawberryfields-code
description: This skill should be used when users ask about code in strawberryfields; it prioritizes documentation references and then source inspection only for unresolved details.
---

# strawberryfields: Code

## High-Signal Playbook
### Route conditions
- Use this skill for codebase-level navigation, cross-module behavior tracing, and implementation-level questions.
- Route newcomer workflow questions to `strawberryfields-getting-started`.
- Route install/build/tooling issues to `strawberryfields-build-and-install`.
- Route direct API-usage questions to `strawberryfields-api-and-scripting`.

### Triage questions
- Which symbol or behavior is being questioned (class/function/error path)?
- Is the issue frontend (`Program`, `ops`, and `Engine`) or backend-specific (`fock`, `gaussian`, `bosonic`, `tf`)?
- Is this a compile path issue (`Program.compile`, compilers) or run path issue (`Engine.run`)?
- Is the discrepancy in samples, state object, or parameter binding?
- Is there an existing test covering the behavior?
- Does the user need explanation, debugging, or a code patch?

### Canonical workflow
1. Start from API docs in `doc/code/sf*.rst` to identify owning module.
2. Resolve exact symbol in source using `rg -n "<symbol>" strawberryfields`.
3. Read call chain across `strawberryfields/program.py -> strawberryfields/ops.py -> strawberryfields/engine.py -> strawberryfields/result.py` and backend files.
4. Check compiler/backend hooks if behavior depends on target backend or device.
5. Validate assumptions against tests (especially integration/frontend tests).
6. Return a minimal behavior explanation or patch with file-level evidence.

### Minimal working example
```bash
rg -n "class Program|def params|def compile" strawberryfields/program.py
rg -n "def run\(|def _run\(" strawberryfields/engine.py
rg -n "class Operation|class Gate|class Measurement" strawberryfields/ops.py
rg -n "class FreeParameter|class MeasuredParameter" strawberryfields/parameters.py
```

### Pitfalls and fixes
- Jumping into backend files before checking frontend contracts: start with `strawberryfields/program.py`, `strawberryfields/ops.py`, and `strawberryfields/engine.py` first.
- Ignoring compiled-vs-uncompiled program behavior: inspect `Program.compile_info` and the compile path in `strawberryfields/program.py`.
- Misreading parameter lifecycle: verify binding/evaluation in `strawberryfields/parameters.py` and `Program.bind_params`.
- Assuming all run options are forwarded to backends: check `eng_run_keys` filtering in `strawberryfields/engine.py`.
- Diagnosing without tests: confirm with the nearest test module before changing logic.

### Convergence/validation checks
- Symbol-level trace from docs to source is explicit and reproducible.
- Proposed behavior matches at least one existing test or a minimal reproduction.
- For numerical/state issues, check backend-specific invariants (for example Fock trace).
- Any patch identifies the precise module boundary it changes.

## Scope
- Handle questions about documentation grouped under the 'code' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/code/sf.rst`
- `doc/code/sf_program.rst`
- `doc/code/sf_ops.rst`
- `doc/code/sf_engine.rst`
- `doc/code/sf_parameters.rst`
- `doc/code/sf_backends.rst`
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
- `examples/boson_sampling.py`

## Test references
- `tests/integration/test_engine_integration.py`
- `tests/frontend`

## Optional deeper inspection
- `strawberryfields`

## Source entry points for unresolved issues
- `strawberryfields/program.py` (program construction, locking, compilation)
- `strawberryfields/engine.py` (execution pipeline, run options, backend interaction)
- `strawberryfields/ops.py` (operation grammar, apply/decompose/merge)
- `strawberryfields/parameters.py` (symbolic/free/measured parameter lifecycle)
- `strawberryfields/result.py` (samples/state metadata model)
- `strawberryfields/program_utils.py` (register/command graph utilities)
- `strawberryfields/compilers/compiler.py` and `strawberryfields/compilers/*.py` (compile templates)
- `strawberryfields/backends/*` (backend-specific operation/state behavior)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields`).
