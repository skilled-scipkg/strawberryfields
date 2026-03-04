# strawberryfields source map: Getting Started

Use this map after `doc_map.md` when first-run behavior needs source-level validation.

## Fast source navigation
- `rg -n "def (context|params|compile)" strawberryfields/program.py`
- `rg -n "def (_run|run)" strawberryfields/engine.py`
- `rg -n "def (__or__|apply)" strawberryfields/ops.py`
- `rg -n "def samples|def state" strawberryfields/result.py`

## Source entry points (function-level)
- `strawberryfields/program.py` | `Program.context`, `Program.params`, `Program.compile`
- `strawberryfields/engine.py` | `BaseEngine._run`, `LocalEngine.run`, shot/feed-forward guards
- `strawberryfields/ops.py` | `Operation.__or__`, `Measurement.apply`, gate application flow
- `strawberryfields/result.py` | `Result.samples`, `Result.samples_dict`, `Result.state`
- `strawberryfields/backends/states.py` | base state-method contracts
- `strawberryfields/backends/fockbackend/backend.py` | `FockBackend.state`, `FockBackend.measure_fock`
- `strawberryfields/backends/gaussianbackend/backend.py` | `GaussianBackend.state`, `GaussianBackend.measure_homodyne`
- `strawberryfields/backends/bosonicbackend/backend.py` | `BosonicBackend.state`, `BosonicBackend.measure_fock`
- `strawberryfields/backends/tfbackend/backend.py` | `TFBackend.state`, `TFBackend.measure_fock`
- `tests/integration/test_engine_integration.py` | first-run integration checks
- `tests/frontend/test_program.py` | context/program lifecycle checks
