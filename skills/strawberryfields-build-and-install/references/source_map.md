# strawberryfields source map: Build and Install

Use this map after `doc_map.md` when install or compile claims need code-level verification.

## Fast source navigation
- `rg -n "install_requires|classifiers|version" setup.py`
- `rg -n "def (_init_backend|run)" strawberryfields/engine.py`
- `rg -n "class Compiler|def (compile|decompose|update_params|add_loss)" strawberryfields/compilers/compiler.py`

## Source entry points (function-level)
- `setup.py` | `requirements`, `classifiers`, `setup(...)` arguments | package/dependency policy source
- `strawberryfields/__init__.py` | `version`, `about` | import and dependency-surface smoke checks
- `strawberryfields/engine.py` | `BaseEngine._init_backend`, `LocalEngine.run` | runtime backend initialization behavior
- `strawberryfields/compilers/compiler.py` | `Compiler.compile`, `Compiler.decompose`, `Compiler.update_params`, `Compiler.add_loss`
- `strawberryfields/device.py` | `Device.validate_target`, `Device.validate_parameters` | device/compile parameter constraints
- `tests/backend/test_tf_import.py` | optional TensorFlow import behavior
- `tests/frontend/compilers/test_compiler.py` | compiler behavior regression checks
- `tests/integration/test_engine_integration.py` | end-to-end engine run smoke coverage
