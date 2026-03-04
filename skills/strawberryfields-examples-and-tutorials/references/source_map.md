# strawberryfields source map: Examples and Tutorials

Use this map after `doc_map.md` when adapting examples needs function-level checks.

## Fast source navigation
- `rg -n "def run|def _run|def _combine_and_sort_samples" strawberryfields/engine.py`
- `rg -n "def (__or__|apply|decompose|merge)" strawberryfields/ops.py`
- `rg -n "class Result|def samples|def state" strawberryfields/result.py`
- `rg -n "def sample|def postselect|def to_subgraphs" strawberryfields/apps/sample.py`

## Source entry points (function-level)
- `examples/teleportation.py` | measured-parameter feed-forward pattern
- `examples/boson_sampling.py` | Fock sampling baseline
- `examples/gaussian_boson_sampling.py` | Gaussian-state probability workflow
- `examples/bosonic_tutorial_sampling.py` | bosonic backend sampling and marginals
- `examples/optimization.py` | parameterized optimization loop pattern
- `strawberryfields/engine.py` | `LocalEngine.run`, `LocalEngine._combine_and_sort_samples`
- `strawberryfields/ops.py` | `Operation.__or__`, `Measurement.apply`, decomposition behavior
- `strawberryfields/result.py` | `Result.samples`, `Result.samples_dict`, `Result.state`
- `strawberryfields/utils/post_processing.py` | `samples_expectation`, `samples_variance`
- `strawberryfields/apps/sample.py` | `sample`, `postselect`, `to_subgraphs`
- `strawberryfields/apps/similarity.py` | `prob_orbit_exact`, `prob_event_exact`, `feature_vector_events`
- `tests/integration/test_measurement_integration.py` | measurement behavior checks
- `tests/integration/test_engine_integration.py` | run/result shape checks
