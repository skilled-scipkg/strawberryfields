# strawberryfields source map: Developer Guide

Use this map after `doc_map.md` when contributor guidance requires code-level verification.

## Fast source navigation
- `rg -n "class Compiler|def (compile|decompose|update_params|add_loss)" strawberryfields/compilers/compiler.py`
- `rg -n "class BaseBackend|def (begin_circuit|state|measure_homodyne|measure_fock)" strawberryfields/backends/base.py`
- `rg -n "class Device|def (validate_target|validate_parameters|create_program)" strawberryfields/device.py`
- `rg -n "def (context|unroll|assert_modes)" strawberryfields/tdm/program.py`

## Source entry points (function-level)
- `strawberryfields/compilers/compiler.py` | `Compiler.compile`, `Compiler.decompose`, `Compiler.update_params`, `Compiler.add_loss`
- `strawberryfields/compilers/gaussian_merge.py` | `get_qumodes_operated_upon`, `get_op_name`, `GaussianMerge`
- `strawberryfields/compilers/xunitary.py` | `list_duplicates`, `Xunitary`
- `strawberryfields/backends/base.py` | `BaseBackend.begin_circuit`, `BaseBackend.state`, mode/measurement contract methods
- `strawberryfields/backends/fockbackend/backend.py` | `FockBackend.begin_circuit`, `FockBackend.state`
- `strawberryfields/backends/gaussianbackend/backend.py` | `GaussianBackend.measure_fock`, `GaussianBackend.measure_threshold`, `GaussianBackend.state`
- `strawberryfields/backends/bosonicbackend/backend.py` | `BosonicBackend.run_prog`, `BosonicBackend.prepare_cat`, `BosonicBackend.state`
- `strawberryfields/backends/tfbackend/backend.py` | `TFBackend.begin_circuit`, `TFBackend.measure_fock`, `TFBackend.state`
- `strawberryfields/device.py` | `Device.validate_target`, `Device.validate_parameters`, `Device.create_program`
- `strawberryfields/tdm/program.py` | `TDMProgram.context`, `TDMProgram.unroll`, `TDMProgram.space_unroll`, `TDMProgram.assert_modes`
- `strawberryfields/io/blackbird_io.py` | `from_blackbird`, `to_blackbird`
- `strawberryfields/logger.py` | `create_logger`, `logging_handler_defined`
- `tests/frontend/compilers/test_compiler.py` | compiler extension behavior checks
- `tests/backend/test_states.py` and `tests/frontend/test_tdmprogram.py` | backend/TDM behavior checks
