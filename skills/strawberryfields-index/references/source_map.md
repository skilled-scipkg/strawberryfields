# strawberryfields source map: Index

Use this map when triage needs fast code-level grounding before selecting a topic skill.

## Fast source navigation
- `rg -n "class Program|def compile|def params" strawberryfields/program.py`
- `rg -n "class LocalEngine|class RemoteEngine|def run_async" strawberryfields/engine.py`
- `rg -n "class Result|def samples|def state" strawberryfields/result.py`
- `rg -n "class Compiler|def compile" strawberryfields/compilers/compiler.py`

## Source entry points (function-level)
- `strawberryfields/program.py` | `Program.context`, `Program.params`, `Program.compile`
- `strawberryfields/engine.py` | `LocalEngine.run`, `RemoteEngine.run`, `RemoteEngine.run_async`
- `strawberryfields/result.py` | `Result.samples`, `Result.samples_dict`, `Result.state`
- `strawberryfields/ops.py` | `Operation.__or__`, `Operation.apply`, `Operation.decompose`
- `strawberryfields/compilers/compiler.py` | `Compiler.compile`, `Compiler.decompose`
- `strawberryfields/backends/base.py` | `BaseBackend.begin_circuit`, `BaseBackend.state`
- `strawberryfields/apps/sample.py` | `sample`, `postselect`
- `tests/integration/test_engine_integration.py` | cross-backend run behavior baseline
- `tests/integration/test_measurement_integration.py` | measurement contract baseline
