# strawberryfields documentation map: Build and Install

Use this map for install, dependency, and environment setup questions.

## Core docs and metadata
- `README.md` | install routes and project-level setup notes
- `doc/install.rst` | official install instructions
- `doc/development/development_guide.rst` | contributor setup, tests, and tooling
- `doc/code/sf_compilers.rst` | compiler overview for compile-related setup context
- `doc/requirements.txt` | docs dependency pins
- `requirements.txt` | runtime dependency pins
- `requirements-dev.txt` | dev/test tooling pins
- `Makefile` | standard test/docs command entry points

## Runnable smoke check
- `examples/teleportation.py`

## Behavior checks
- `tests/backend/test_tf_import.py`
- `tests/frontend/compilers/test_compiler.py`
- `tests/integration/test_engine_integration.py`
