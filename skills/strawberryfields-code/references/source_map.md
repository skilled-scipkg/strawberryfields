# strawberryfields source map: Code

Use this map after `doc_map.md` when tracing behavior across modules.

## Fast source navigation
- `rg -n "def (context|compile|params|bind_params)" strawberryfields/program.py`
- `rg -n "def (_run|run|run_async|_combine_and_sort_samples)" strawberryfields/engine.py`
- `rg -n "def (__or__|apply|decompose|merge)" strawberryfields/ops.py`
- `rg -n "class Compiler|def (compile|decompose|update_params)" strawberryfields/compilers/compiler.py`
- `rg -n "class BaseBackend|def (begin_circuit|state|measure_homodyne|measure_fock)" strawberryfields/backends/base.py`

## Source entry points (function-level)
- `strawberryfields/program.py` | `Program.context`, `Program.compile`, `Program.params`, `Program.bind_params`
- `strawberryfields/engine.py` | `BaseEngine._run`, `LocalEngine.run`, `RemoteEngine.run`, `RemoteEngine.run_async`
- `strawberryfields/ops.py` | `Operation.__or__`, `Operation.apply`, `Operation.decompose`, `Operation.merge`
- `strawberryfields/parameters.py` | `par_convert`, `par_evaluate`, `FreeParameter`, `MeasuredParameter`
- `strawberryfields/result.py` | `Result.samples`, `Result.samples_dict`, `Result.state`
- `strawberryfields/program_utils.py` | `optimize_circuit`, `program_equivalence`, `validate_gate_parameters`
- `strawberryfields/compilers/compiler.py` | `Compiler.compile`, `Compiler.decompose`, `Compiler.update_params`, `Compiler.add_loss`
- `strawberryfields/backends/base.py` | `BaseBackend.begin_circuit`, `BaseBackend.state`, `BaseBackend.measure_homodyne`, `BaseBackend.measure_fock`
- `strawberryfields/backends/fockbackend/backend.py` | `FockBackend.state`, `FockBackend.measure_fock`
- `strawberryfields/backends/gaussianbackend/backend.py` | `GaussianBackend.state`, `GaussianBackend.measure_fock`, `GaussianBackend.measure_threshold`
- `strawberryfields/backends/bosonicbackend/backend.py` | `BosonicBackend.run_prog`, `BosonicBackend.state`, `BosonicBackend.measure_fock`
- `strawberryfields/backends/tfbackend/backend.py` | `TFBackend.begin_circuit`, `TFBackend.state`, `TFBackend.measure_fock`
- `strawberryfields/tdm/program.py` | `TDMProgram.context`, `TDMProgram.unroll`, `TDMProgram.space_unroll`, `TDMProgram.assert_modes`
- `strawberryfields/io/blackbird_io.py` | `from_blackbird`, `to_blackbird`
- `tests/frontend/test_program.py` and `tests/frontend/test_engine.py` | frontend behavior contracts
- `tests/integration/test_engine_integration.py` and `tests/integration/test_ops_integration.py` | integration behavior contracts
