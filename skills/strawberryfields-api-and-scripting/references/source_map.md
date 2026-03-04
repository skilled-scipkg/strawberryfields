# strawberryfields source map: API and Scripting

Use this map after `doc_map.md` when API behavior needs function-level verification.

## Fast source navigation
- `rg -n "def (context|append|params|bind_params|compile)" strawberryfields/program.py`
- `rg -n "def (_run|run|run_async|_combine_and_sort_samples)" strawberryfields/engine.py`
- `rg -n "def (__or__|apply|decompose|merge)" strawberryfields/ops.py`
- `rg -n "par_evaluate|par_convert|class FreeParameter|class MeasuredParameter" strawberryfields/parameters.py`

## Source entry points (function-level)
- `strawberryfields/program.py` | `Program.context`, `Program.append`, `Program.params`, `Program.bind_params`, `Program.compile`
- `strawberryfields/engine.py` | `BaseEngine._run`, `LocalEngine.run`, `RemoteEngine.run`, `RemoteEngine.run_async`, `LocalEngine._combine_and_sort_samples`
- `strawberryfields/ops.py` | `Operation.__or__`, `Operation.apply`, `Operation.decompose`, `Operation.merge`, `Measurement.apply`
- `strawberryfields/parameters.py` | `par_evaluate`, `par_convert`, `FreeParameter`, `MeasuredParameter`
- `strawberryfields/result.py` | `Result.samples`, `Result.samples_dict`, `Result.state`
- `strawberryfields/device.py` | `Device.validate_parameters`, `Device.create_program`
- `strawberryfields/io/blackbird_io.py` | `from_blackbird`, `to_blackbird`
- `tests/integration/test_engine_integration.py` | run semantics and result-shape contracts
- `tests/integration/test_parameters_integration.py` | parameter binding/evaluation contracts
- `tests/frontend/test_program.py` | frontend program lifecycle checks
