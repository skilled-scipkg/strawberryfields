---
name: strawberryfields-analysis-and-output
description: This skill should be used when users ask about Strawberry Fields results, plotting, sample post-processing, and simulation output validation.
---

# strawberryfields: Analysis and Output

## High-Signal Playbook
### Route conditions
- Use this skill for `Result` interpretation, sample statistics, plotting utilities, and output quality checks.
- Route circuit construction/API semantics to `strawberryfields-api-and-scripting`.
- Route runnable script selection to `strawberryfields-examples-and-tutorials`.
- Route backend internals to `strawberryfields-code`.

### Triage questions
- Do they need raw samples, per-mode sample history, or a state object?
- Are they validating statistical moments or visualizing states/distributions?
- Which backend generated the output (`gaussian`, `fock`, `bosonic`, `tf`)?
- Do they need post-processing for photon-number data or GBS-specific runtime analysis?

### Canonical workflow
1. Confirm output container first: `result.samples`, `result.samples_dict`, `result.state`.
2. Choose analysis primitive: `samples_expectation`, `samples_variance`, or Fock probability helpers.
3. For visualization, use `sf.plot` utilities with explicit modes and ranges.
4. Validate numeric plausibility (state trace, shape checks, mode alignment) before interpretation.
5. Cross-check behavior against tests in `tests/frontend` and `tests/apps`.

### Minimal working example
```python
import strawberryfields as sf
from strawberryfields import ops
from strawberryfields.utils.post_processing import samples_expectation

prog = sf.Program(1)
with prog.context as q:
    ops.Sgate(0.2) | q[0]
    ops.MeasureFock() | q[0]

res = sf.Engine("fock", backend_options={"cutoff_dim": 8}).run(prog, shots=20)
print(res.samples.shape)
print(samples_expectation(res.samples, modes=[0]))
```

### Pitfalls and fixes
- Assuming `result.state` always exists: it is omitted for some run configurations.
- Aggregating over wrong axes: verify sample shape and selected `modes` first.
- Plotting with inconsistent `xvec`/`pvec` grids: ensure both vectors match expected resolution.
- Comparing outputs across backends without checking backend-specific semantics.

### Validation checkpoints
- Sample array shape matches `(shots, measured_modes)`.
- For Fock/TF states, trace stays close to 1 when state is requested.
- Post-processing outputs match targeted frontend tests.

## Primary documentation references
- `doc/introduction/data.rst`
- `doc/introduction/states.rst`
- `doc/code/sf_plot.rst`
- `doc/code/sf_utils.rst`
- `doc/code/sf_apps.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md`.
- If ambiguity remains after docs, inspect `references/source_map.md`.
- Cite exact file paths in responses.

## Source entry points for unresolved issues
- `strawberryfields/result.py` (`Result.samples`, `Result.samples_dict`, `Result.state`)
- `strawberryfields/utils/post_processing.py` (`samples_expectation`, `samples_variance`, `all_fock_probs_pnr`)
- `strawberryfields/plot.py` (`plot_wigner`, `plot_fock`, `plot_quad`)
- `strawberryfields/utils/gbs_analysis.py` (`gbs_runtime`, `gbs_sample_runtime`)
- `strawberryfields/apps/plot.py` (`graph`, `subgraph`, `points`, `spectrum`)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" strawberryfields`).
