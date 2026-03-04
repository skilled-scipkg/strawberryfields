---
name: strawberryfields-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in strawberryfields; it prioritizes documentation references and then source inspection only for unresolved details.
---

# strawberryfields: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use this skill when users want a runnable script to adapt quickly.
- Route package setup issues to `strawberryfields-build-and-install`.
- Route API semantics/details to `strawberryfields-api-and-scripting`.
- Route deep output/post-processing interpretation to `strawberryfields-analysis-and-output`.

### Triage questions
- Is the goal teleportation, boson sampling, state inspection, optimization, or ML-style training?
- Which backend best matches the circuit class: Gaussian-only, general Fock, or bosonic representations?
- Is non-Gaussian behavior required during evolution?
- Do they need probabilities/state access or only measurement samples?
- What scale constraints exist (modes, shots, cutoff, runtime)?
- Is feed-forward/postselection needed?

### Canonical workflow
1. Pick the closest script from `examples/` as baseline.
2. Preserve the skeleton: `Program` creation, `with prog.context`, `Engine`, `run`.
3. Choose backend by circuit type (`doc/introduction/circuits.rst`).
4. Modify only one axis at a time (operations, parameters, backend, or measurements).
5. For Fock-like simulations, set/adjust `cutoff_dim` early.
6. Validate outputs against integration-test expectations (sample shape/state availability).
7. Scale shots/modes after the one-shot run is correct.

### Minimal working example
```python
import strawberryfields as sf
from strawberryfields import ops

prog = sf.Program(2)
with prog.context as q:
    ops.S2gate(0.4) | (q[0], q[1])
    ops.MeasureFock() | q

res = sf.Engine("gaussian").run(prog, shots=5)
print(res.samples.shape)
```

### Pitfalls and fixes
- Backend/circuit mismatch: Gaussian backend cannot represent arbitrary non-Gaussian evolution (`doc/introduction/circuits.rst`).
- Fock truncation too small: increase `cutoff_dim` and re-check trace.
- Copying examples without understanding output type: confirm whether script uses `result.state` or only `result.samples`.
- Assuming arbitrary `shots > 1` works with feed-forward/postselection: check `LocalEngine.run` constraints.
- Changing many knobs at once while debugging: keep edits incremental from a known-good example.

### Convergence/validation checks
- Sample arrays have expected `(shots, measured_modes)` shape (`tests/integration/test_engine_integration.py`).
- Where state is requested, `result.state` is present and supports expected methods.
- Fock/TF traces remain close to 1 before scaling.
- Adapted example still reproduces qualitative behavior from the original script.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/introduction/circuits.rst`
- `doc/introduction/ops.rst`
- `doc/introduction/states.rst`
- `doc/introduction/introduction.rst`

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
- `examples/bosonic_tutorial_sampling.py`
- `examples/optimization.py`

## Test references
- `tests/integration/test_engine_integration.py`

## Optional deeper inspection
- `strawberryfields`

## Source entry points for unresolved issues
- `examples/teleportation.py` (feed-forward via measured parameters)
- `examples/boson_sampling.py` (Fock sampling workflow)
- `examples/gaussian_boson_sampling.py` (Gaussian-state probability evaluation)
- `examples/bosonic_tutorial_sampling.py` (bosonic backend sampling + marginal checks)
- `strawberryfields/engine.py` (shot semantics, run guards, result construction)
- `strawberryfields/ops.py` (operation application/decomposition semantics)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields`).
