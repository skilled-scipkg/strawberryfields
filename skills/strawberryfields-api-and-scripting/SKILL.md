---
name: strawberryfields-api-and-scripting
description: This skill should be used when users ask about api and scripting in strawberryfields; it prioritizes documentation references and then source inspection only for unresolved details.
---

# strawberryfields: API and Scripting

## High-Signal Playbook
### Route conditions
- Use this skill for `Program`, `ops`, symbolic parameters, `Engine.run`, compile options, and result-access patterns.
- Route installation/environment blockers to `strawberryfields-build-and-install`.
- Route user-facing runnable script selection/adaptation to `strawberryfields-examples-and-tutorials`.
- Route deep backend internals or cross-module implementation tracing to `strawberryfields-code`.

### Triage questions
- Local simulator or remote device run?
- Which backend (`gaussian`, `fock`, `bosonic`, `tf`) and which backend options?
- Are parameters free (`prog.params`) or measured (`q[i].par`)?
- Is compilation required (`compiler`/`device`) before run?
- Is `shots > 1` needed, and does the circuit include feed-forward/postselection?
- Is full state required, or just selected modes/samples?

### Canonical workflow
1. Define `sf.Program(N)` and add operations via `with prog.context as q:` (`doc/introduction/circuits.rst`).
2. Encode operations from `strawberryfields.ops` and parameter expressions (`doc/code/sf_ops.rst`).
3. Create free parameters with `prog.params(...)` and bind through `eng.run(..., args=...)`.
4. Initialize engine with explicit backend/backend options.
5. Run with `eng.run(program, args=..., compile_options=..., shots=..., modes=...)`.
6. Inspect `result.samples`, `result.samples_dict`, and `result.state` as needed.
7. For device constraints, compile via `Program.compile(device=..., compiler=...)` before execution.

### Minimal working example
```python
import strawberryfields as sf
from strawberryfields import ops

prog = sf.Program(2)
a = prog.params("a")

with prog.context as q:
    ops.Dgate(a) | q[0]
    ops.MeasureX | q[0]
    ops.Sgate(1 - sf.math.sin(q[0].par)) | q[1]

eng = sf.Engine("fock", backend_options={"cutoff_dim": 8})
res = eng.run(prog, args={"a": 0.3}, shots=1)
print(res.samples)
print(res.state.trace())
```

### Pitfalls and fixes
- Unbound free parameter error: ensure every `prog.params` symbol is bound through `args` (or has default) (`strawberryfields/parameters.py`).
- Using raw register refs instead of measured parameters: use `q[i].par` for feed-forward (`doc/introduction/circuits.rst`).
- `shots > 1` with feed-forward/postselection: unsupported in `LocalEngine.run`; use `shots=1` for those circuits (`strawberryfields/engine.py`).
- Expecting state for `modes=[]`: `Result.state` is intentionally omitted (`strawberryfields/engine.py`).
- Wrong subsystem count for operations: check operation arity (`strawberryfields/ops.py`).
- Calling `Program.compile()` without `compiler` or `device`: raises `ValueError` (`strawberryfields/program.py`).

### Convergence/validation checks
- Parameterized runs: validate no `ParameterError` and that bound values propagate to outputs.
- Fock/TF runs: verify `result.state.trace()` is near 1.
- Check returned sample shape matches measured modes and `shots`.
- Validate run-options behavior against `tests/integration/test_engine_integration.py`.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/code/sf_program.rst`
- `doc/code/sf_ops.rst`
- `doc/code/sf_engine.rst`
- `doc/code/sf_parameters.rst`
- `doc/introduction/circuits.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples/teleportation.py`
- `examples/custom_operation.py`
- `examples/optimization.py`

## Test references
- `tests/integration/test_engine_integration.py`

## Optional deeper inspection
- `strawberryfields`

## Source entry points for unresolved issues
- `strawberryfields/program.py` (`Program.context`, `Program.params`, `Program.bind_params`, `Program.compile`)
- `strawberryfields/engine.py` (`BaseEngine._run`, `LocalEngine.run`, `RemoteEngine.run`, `RemoteEngine.run_async`)
- `strawberryfields/ops.py` (`Operation`, `Gate`, `Measurement`, apply/decompose/merge behavior)
- `strawberryfields/parameters.py` (`FreeParameter`, `MeasuredParameter`, `par_evaluate`)
- `strawberryfields/result.py` (`Result` data model and metadata behavior)
- `strawberryfields/program_utils.py` (command/register graph utilities)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields`).
