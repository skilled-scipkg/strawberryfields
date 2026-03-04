---
name: strawberryfields-getting-started
description: This skill should be used when users ask about getting started in strawberryfields; it prioritizes documentation references and then source inspection only for unresolved details.
---

# strawberryfields: Getting Started

## High-Signal Playbook
### Route conditions
- Use this skill for first runnable circuits, backend choice, and first `Program -> Engine -> Result` runs.
- Route installation and dependency breakages to `strawberryfields-build-and-install`.
- Route API-deep questions (symbolic parameters, compiler behavior, run options) to `strawberryfields-api-and-scripting`.
- Route worked script adaptation to `strawberryfields-examples-and-tutorials`.

### Triage questions
- Which backend is needed: `gaussian`, `fock`, `bosonic`, or `tf`? (`doc/introduction/circuits.rst`)
- Do they need only samples, or also a `Result.state` object?
- Are free parameters (`prog.params`) or measured parameters (`q[i].par`) involved?
- Is `shots > 1` required, and is there feed-forward or postselection in the circuit?
- For Fock/TF runs, what `cutoff_dim` is being used?
- Do they need a local simulator workflow or remote/device compilation?

### Canonical workflow
1. Confirm environment and install route from `doc/install.rst`.
2. Create `sf.Program(N)` and populate with `with prog.context as q:` (`doc/introduction/circuits.rst`).
3. Apply operations from `strawberryfields.ops` (`doc/introduction/ops.rst`).
4. Instantiate `sf.Engine(<backend>, backend_options=...)` with backend-specific options.
5. Execute `eng.run(prog, args=..., shots=...)` (`doc/introduction/circuits.rst`, `strawberryfields/engine.py`).
6. Inspect `result.samples` and optionally `result.state` (`doc/introduction/circuits.rst`, `doc/introduction/states.rst`).
7. Validate numerics (especially Fock trace) before scaling experiments.

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

eng = sf.Engine("fock", backend_options={"cutoff_dim": 7})
result = eng.run(prog, args={"a": 0.9}, shots=1)
print(result.samples)
print(result.state.trace())
```

### Pitfalls and fixes
- `Program` not populated inside `with prog.context`: use context manager form from `doc/introduction/circuits.rst`.
- Fock/TF numeric drift (`trace << 1`): increase `cutoff_dim` (`doc/introduction/circuits.rst`).
- `shots > 1` with feed-forward/postselection: unsupported; reduce to `shots=1` (`strawberryfields/engine.py`).
- Expecting `result.state` while passing `modes=[]`: no state is returned (`strawberryfields/engine.py`, tests in `tests/integration/test_engine_integration.py`).
- TensorFlow backend errors: install TensorFlow explicitly (`doc/introduction/circuits.rst`, `doc/development/development_guide.rst`).

### Convergence/validation checks
- For Fock/TF workflows, verify `result.state.trace()` remains close to 1.
- Check sample shape is consistent with measured modes and `shots` (`tests/integration/test_engine_integration.py`).
- Confirm measured modes carry values and unmeasured modes remain `None` in register refs.
- Run one shot first, then increase shots after behavior is correct.

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/introduction/introduction.rst`
- `doc/install.rst`
- `doc/introduction/circuits.rst`
- `doc/introduction/ops.rst`
- `doc/introduction/states.rst`

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
- `examples/gaussian_boson_sampling.py`

## Test references
- `tests/integration/test_engine_integration.py`

## Optional deeper inspection
- `strawberryfields`

## Source entry points for unresolved issues
- `strawberryfields/program.py` (`Program.context`, `Program.params`, `Program.compile`)
- `strawberryfields/engine.py` (`LocalEngine.run`, `_run`, shot/feed-forward/postselection guards)
- `strawberryfields/ops.py` (`Operation.__or__`, `Measurement.apply`)
- `strawberryfields/result.py` (`Result.samples`, `Result.state`, `Result.samples_dict`)
- `strawberryfields/backends/states.py` (state method contracts)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields`).
