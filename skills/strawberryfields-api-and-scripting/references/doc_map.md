# strawberryfields documentation map: API and Scripting

Use docs/examples/tests below before source inspection.

## Core docs
- `doc/code/sf_program.rst` | program lifecycle and compilation API
- `doc/code/sf_ops.rst` | operation and gate API
- `doc/code/sf_engine.rst` | execution API (`Engine`, local/remote run behavior)
- `doc/code/sf_parameters.rst` | symbolic and measured parameter API
- `doc/introduction/circuits.rst` | practical circuit-authoring semantics
- `doc/introduction/ops.rst` | operation usage patterns
- `doc/development/migration_guides.rst` | migration caveats for older API usage

## Runnable examples
- `examples/teleportation.py`
- `examples/custom_operation.py`
- `examples/optimization.py`

## Behavior checks
- `tests/integration/test_engine_integration.py`
- `tests/integration/test_parameters_integration.py`
- `tests/frontend/test_program.py`
- `tests/frontend/test_engine.py`
- `tests/frontend/test_parameters.py`
